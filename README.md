# FluentCart Code Snippets 🎯

A curated collection of custom code snippets to extend and enhance [FluentCart](https://github.com/fluent-cart/fluent-cart) functionality.

[![FluentCart](https://img.shields.io/badge/FluentCart-Compatible-brightgreen.svg)](https://fluentcart.com)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-orange.svg)](https://github.com/fluent-cart/fluent-cart-snippets/issues)

---

> **🚧 Repository in Progress**  
> This repository is actively being built! We're adding new code snippets regularly. Have a useful FluentCart snippet? add it here and share to [https://community.wpmanageninja.com/portal/space/fluent-cart/home](#-how-to-contribute) Whether you're a seasoned developer or just getting started, your contributions are welcome here. 🤝

---

## 📖 Overview

Ready-to-use code snippets to customize and extend FluentCart without modifying core files. Perfect for developers, store owners, and anyone building custom FluentCart solutions.

All snippets follow WordPress and FluentCart coding standards.

### 🎯 Get Involved

**Community-driven project** – we need your help!

- 📝 **Share Your Snippets** - [Contribute code](#-how-to-contribute)
- 🐛 **Report Issues** - [Found a bug?](https://github.com/fluent-cart/fluent-cart-snippets/issues)
- 💬 **Request Snippets** - [Open an issue](https://github.com/fluent-cart/fluent-cart-snippets/issues) with your idea
- ⭐ **Star the Repo** - Help others discover this resource

## 🚀 How to Use Snippets

### Quick Methods:

**Option 1: Child Theme Functions**
Add code to `your-child-theme/functions.php`

**Option 2: Custom Plugin**
Create `/wp-content/plugins/fluent-cart-custom/fluent-cart-custom.php`:

```php
<?php
/**
 * Plugin Name: FluentCart Custom
 * Description: Custom FluentCart snippets
 * Version: 1.0
 */

// Add snippets here
```

**Option 3: Code Snippets Plugin**
Use [Code Snippets](https://wordpress.org/plugins/easy-code-manager/) or similar plugin

### ⚠️ Important

- Always backup before adding code
- Test on staging first
- Never modify core plugin files

## 📂 Categories

- 🔔 **[Subscriptions](#subscriptions)** - Recurring payments and subscription customizations

_More categories will appear as snippets are added. [Contribute yours!](#-how-to-contribute)_

## 📝 Available Snippets

### Subscriptions
- [Custom Subscription Intervals](./Subscriptions/HOW_TO_ADD_CUSTOM_SUBSCRIPTION_INTERVAL.md) - Add custom billing cycles (every 10 days, fortnightly, etc.)

_More snippets coming soon! [Contribute yours](#-how-to-contribute)_

## 💡 Most Wanted Snippets

**Payments:** Custom gateways, conditional payment methods, checkout validation, multi-currency  
**Email:** Custom templates, SMS integrations, webhook connectors  
**Orders:** Bulk processing, custom product types, inventory automation  
**Integrations:** CRM (HubSpot, Salesforce), Marketing (Mailchimp), Accounting, Analytics

[Suggest more](https://github.com/fluent-cart/fluent-cart-snippets/issues) or contribute yours!

## 🤝 How to Contribute

**Two easy ways:**

### Quick Method
[Open an issue](https://github.com/fluent-cart/fluent-cart-snippets/issues) with your snippet – we'll add it with credit to you

### Standard Method
1. Fork this repository
2. Create branch: `git checkout -b add-snippet-name`
3. Add snippet in appropriate category folder (`.md` or `.php` file)
4. Follow the [snippet template](#snippet-template) below
5. Commit: `git commit -m "Add: [snippet name]"`
6. Push and open Pull Request

**First time?** [Ask for help](https://github.com/fluent-cart/fluent-cart-snippets/issues) – we're friendly! 😊

### Good Snippet Checklist
✅ Solves a real problem  
✅ Well-documented  
✅ Tested with current FluentCart  
✅ Follows WordPress standards

### Snippet Template

```markdown
# Snippet Title

Brief description of what this does and when to use it.

## Code

\`\`\`php
add_action('fluent_cart/example_hook', function($data) {
    // Your code
});
\`\`\`

## Usage

Step-by-step implementation instructions.

## Notes

- Important information
- Compatibility notes
- Related hooks: `fluent_cart/hook_name`
```

## 📚 Resources

- **FluentCart Main Repository**: [github.com/fluent-cart/fluent-cart](https://github.com/fluent-cart/fluent-cart)
- **Developer Documentation**: [dev.fluentcart.com](https://dev.fluentcart.com)
- **User Documentation**: [docs.fluentcart.com](https://docs.fluentcart.com/)
- **Community Forum**: [community.wpmanageninja.com](https://community.wpmanageninja.com/portal/space/fluent-cart/home)
- **FluentCart Website**: [fluentcart.com](https://fluentcart.com)

## 💡 Need Help?

- **Questions?** Open an [issue](https://github.com/fluent-cart/fluent-cart/issues) or ask in the [community forum](https://community.wpmanageninja.com/portal/space/fluent-cart/home)
- **Bug in a snippet?** Please report it in the [issues](https://github.com/fluent-cart/fluent-cart-snippets/issues)
- **Feature request?** We'd love to hear your ideas!
- **Custom development?** Check out [FluentCart Pro](https://fluentcart.com) or reach out to the community

## ⚖️ License

All code snippets in this repository are licensed under **GNU GPLv3**, same as FluentCart and WordPress.

You are free to use, modify, and distribute these snippets in your projects.

## 🌟 Show Your Support

If you find these snippets helpful:
- 🐛 Report bugs and issues
- 💡 Suggest new snippet ideas
- 🤝 Contribute your own snippets
- 📢 Share with the community

---

**Made with ❤️ by the FluentCart Team & community**

*Building the fastest, most developer-friendly WordPress eCommerce platform together!*

