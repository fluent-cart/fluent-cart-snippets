# Custom Subscription Intervals

Extend FluentCart's default subscription intervals with custom billing cycles.

## 1. Add Interval Option (Required)

**This is the most important filter** - it adds your custom interval to the subscription options.

**Each option must contain three required fields:**
- `label` - Display name shown in dropdown (required)
- `value` - Unique key saved in database (required)
- `map_value` - Formal/readable version of the interval (required)

```php
/**
 * Extend interval options
 * 
 * @param array $intervalOptions Existing interval options
 * @return array Modified interval options
 */
add_filter('fluent_cart/available_subscription_interval_options', function ($intervalOptions) {
    return array_merge($intervalOptions, [
        [
            'label' => __('Every 10th day', 'fluent-cart'),      // Display name
            'value' => 'every_tenth_day',                        // Database key
            'map_value' => '10th Day',                           // Readable format
        ],
    ]);
});
```

## 2. Define Equivalent Days

```php
/**
 * Convert interval to days
 * 
 * @param int   $days Default days
 * @param array $args Contains 'interval' key
 * @return int Number of days
 */
add_filter('fluent_cart/subscription_interval_in_days', function($days, $args) {
    $interval = $args['interval'];
    
    if ($interval == 'every_tenth_day') {
        return 10;
    }
    
    return $days;
}, 10, 2);
```

## 3. Set Max Trial Days (Optional)

```php
/**
 * Maximum trial days for custom interval
 * 
 * @param int   $days Default max trial days
 * @param array $args Contains: repeat_interval, existing_trial_days, interval_in_days
 * @return int Maximum allowed trial days
 */
add_filter('fluent_cart/max_trial_days_allowed', function($days, $args) {
    $interval = $args['repeat_interval'];
    $existingTrialDays = $args['existing_trial_days'];
    $intervalInDays = $args['interval_in_days'];
    
    if ($interval == 'every_tenth_day') {
        return min($existingTrialDays + $intervalInDays, 10);
    }
    
    return $days;
}, 10, 2);
```

## 4. Configure Gateway Billing Period

**Note:** Only use this hook if you're using FluentCart's built-in gateways or third-party gateway addons. If you own the payment gateway code, handle the billing period directly in your gateway processor instead.

```php
/**
 * Format billing period for payment gateways
 * 
 * @param array $billingPeriod Contains: interval_unit, interval_frequency
 * @param array $args Contains: payment_method, subscription_interval
 * @return array Modified billing period
 */
add_filter('fluent_cart/subscription_billing_period', function ($billingPeriod, $args) {
    $paymentMethod = $args['payment_method'];
    $subscriptionInterval = $args['subscription_interval'];
    
    if ($paymentMethod == 'stripe') {
        if ($subscriptionInterval == 'every_tenth_day') {
            $billingPeriod['interval_unit'] = 'day';
            $billingPeriod['interval_frequency'] = 10;
        }
    }
    
    if ($paymentMethod == 'paypal') {
        if ($subscriptionInterval == 'fortnightly') {
            $billingPeriod['interval_unit'] = 'week';
            $billingPeriod['interval_frequency'] = 2;
        }
    }
    
    return $billingPeriod;
}, 10, 2);
```

## 5. Configure License Validity (For Licensed Products)

If your product variation includes licensing features, configure the license expiration based on your custom interval.

### Default License Validity by Variation

```php
/**
 * Set default license validity for custom interval
 * 
 * @param array $validityUnit Default validity configuration
 * @param array $args Contains: variation
 * @return array License validity with 'unit' and 'value' keys
 */
add_filter('fluent_cart/license/default_validity_by_variation', function($validityUnit, $args) {
    $variation = $args['variation'];
    $otherInfo = $variation->other_info;

    if (Arr::get($otherInfo, 'repeat_interval') == 'every_tenth_day') {
        return [
            'unit' => 'day',
            'value' => 10
        ];
    }
    
    return $validityUnit;
}, 10, 2);
```

### License Validity by Variation (Alternative)

**Note:** Only use this if `fluent_cart/license/default_validity_by_variation` is not already handling your case.

```php
/**
 * Modify license validity for custom interval
 * 
 * @param array $validity Current validity configuration
 * @param array $args Contains: variation
 * @return array Modified validity
 */
add_filter('fluent_cart/license/validity_by_variation', function ($validity, $args) {
    $variation = $args['variation'];
    $otherInfo = $variation->other_info;

    if (Arr::get($otherInfo, 'repeat_interval') == 'every_tenth_day') {
        $validity['unit'] = 'day';
        $validity['value'] = 10;
    }
    
    return $validity;
}, 10, 2);
```

### License Expiration Date by Variation

```php
/**
 * Calculate license expiration timestamp for custom interval
 * 
 * @param int   $timestamp Default expiration timestamp
 * @param array $args Contains: variation, trial_days
 * @return int Modified expiration timestamp
 */
add_filter('fluent_cart/license/expiration_date_by_variation', function ($timestamp, $args) {
    $variation = $args['variation'];
    $otherInfo = $variation->other_info;
   
    $trialDays = $args['trial_days'];

    if (Arr::get($otherInfo, 'repeat_interval') == 'every_tenth_day') {
        return strtotime('+ 10 days', time()) + ($trialDays * DAY_IN_SECONDS);
    }

    return $timestamp;
}, 10, 2);
```

## Gateway Compatibility

- **Stripe**: Supports `day`, `week`, `month`, `year` with any positive frequency
- **PayPal**: Supports `day`, `week`, `month`, `year` with frequency limitations
- **Custom Gateways**: Format billing period directly in your gateway processor

