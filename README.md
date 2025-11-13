# OpenCart 4 Sample Extension - Plugin Boilerplate

A comprehensive boilerplate for OpenCart 4 extension development. This sample extension provides a solid foundation with examples of essential functions, file structure, and configurations required to build a fully functional OpenCart extension.

## 📋 Overview

This repository contains a complete example of an OpenCart 4 extension (module) named "Example Plugin" with proper directory structure, language files, controllers, views, and OCMOD modifications. It demonstrates best practices for extension development in OpenCart 4.

## 📁 Directory Structure

```
Opencart-4-sample-extension---plugin-boilerplate/
├── install.json                 # Extension metadata and configuration
├── LICENSE                      # License file
├── admin/                       # Admin panel components
│   ├── controller/
│   │   └── module/
│   │       └── example_plugin.php    # Admin controller with install/uninstall
│   ├── language/
│   │   └── en-gb/
│   │       └── module/
│   │           └── example_plugin.php    # Admin language file
│   └── view/
│       └── template/
│           └── module/
│               └── example_plugin.twig   # Admin settings template
├── catalog/                     # Frontend (customer-facing) components
│   ├── controller/
│   │   └── extension/
│   │       └── module/
│   │           └── example_plugin.php    # Frontend controller
│   ├── language/
│   │   └── en-gb/
│   │       └── extension/
│   │           └── module/
│   │               └── example_plugin.php    # Frontend language file
│   ├── model/
│   │   └── extension/
│   │       └── module/
│   │           └── example_plugin.php    # Database model
│   └── view/
│       └── template/
│           └── extension/
│               └── module/
│                   └── example_plugin.twig   # Frontend template
└── ocmod/                       # OCMOD XML modifications
    └── install.ocmod.xml        # File modifications for core OpenCart files
```

## 🚀 Features

### Core Functionality

- **Admin Controller**: Complete settings management with save, validate, install, and uninstall methods
- **Frontend Module**: Catalog-side implementation with controller, model, and view
- **Database Integration**: Example SQL table creation in the install method
- **Event System**: Integration with OpenCart's event system
- **Permission Management**: User group permissions setup
- **Language Support**: Multi-language ready with language file examples

### OCMOD Modifications

The extension includes example OCMOD XML modifications that demonstrate:
- Replacing controller methods
- Modifying file structures
- Multiple file path patterns
- Safe file modification without core edits

## 📦 Installation

1. **Extract the extension** to your OpenCart 4 installation:
   ```
   cp -r Opencart-4-sample-extension---plugin-boilerplate /path/to/opencart/admin/view/javascript/
   ```

2. **Install via OpenCart Admin Panel**:
   - Navigate to `Extensions → Installer`
   - Upload the extension or install from the directory
   - Verify the installation in `Extensions → Modules`

3. **Enable the Module**:
   - Go to `Extensions → Modules`
   - Find "Example Plugin"
   - Click "Install" to set up database and permissions
   - Configure settings as needed

## 📝 Key Files Explained

### `install.json`
Contains extension metadata:
```json
{
  "name": "Example Plugin",
  "version": "1.0",
  "code": "example_plugin",
  "author": "Gemini",
  "link": "Saqib Ashraf saqibashraf.net"
}
```

### Admin Controller (`admin/controller/module/example_plugin.php`)

**Methods:**
- `index()` - Displays admin settings page with breadcrumbs
- `save()` - Handles form submission and settings storage
- `validate()` - Validates user permissions
- `install()` - Creates database tables, adds events, sets permissions
- `uninstall()` - Removes database tables and events

### Frontend Controller (`catalog/controller/extension/module/example_plugin.php`)

Handles customer-facing functionality and logic.

### Database Model (`catalog/model/extension/module/example_plugin.php`)

Manages database operations and queries for the frontend.

### OCMOD XML (`ocmod/install.ocmod.xml`)

Demonstrates safe modifications to core OpenCart files:
- Controllers manipulation
- View file modifications
- Pattern-based file targeting

## 🔧 Development Guide

### Adding Custom Functionality

1. **Extend the Controller**:
   ```php
   public function customMethod() {
       // Your custom logic here
   }
   ```

2. **Add Database Tables** in `install()`:
   ```php
   $this->db->query("CREATE TABLE IF NOT EXISTS `" . DB_PREFIX . "example_plugin_custom` (...)")
   ```

3. **Create Language Strings** in language files:
   ```php
   $_['heading_custom'] = 'Custom Heading';
   ```

4. **Add Event Hooks** for triggering actions:
   ```php
   $this->model_setting_event->addEvent($event_data);
   ```

### OCMOD Modifications

Edit `ocmod/install.ocmod.xml` to modify core files safely:

```xml
<file path="path/to/file.php">
    <operation>
        <search><![CDATA[original code]]></search>
        <add position="replace"><![CDATA[replacement code]]></add>
    </operation>
</file>
```

## 🎯 Extension Lifecycle

### Installation Process
1. System calls `install()` method
2. Database tables are created
3. Events are registered
4. User permissions are assigned

### Uninstallation Process
1. System calls `uninstall()` method
2. Database tables are dropped
3. Events are removed
4. Settings are cleaned up

## 📚 Best Practices

- ✅ Always validate user permissions in admin operations
- ✅ Use OpenCart's model system for database operations
- ✅ Store configuration values in the settings table
- ✅ Use language files for all text content (multi-language support)
- ✅ Follow OpenCart 4 namespace conventions
- ✅ Clean up database tables and events on uninstall
- ✅ Use OCMOD for safe core file modifications
- ✅ Implement proper error handling and validation

## 🔐 Security Considerations

- User permissions are checked before allowing admin modifications
- Token-based authentication for admin actions
- SQL queries use proper prefixing with `DB_PREFIX`
- Input validation in the `validate()` method
- OCMOD provides safe modification without editing core files directly

## 🌐 Language Support

The extension is ready for multi-language support:
- Admin language file: `admin/language/en-gb/module/example_plugin.php`
- Frontend language file: `catalog/language/en-gb/extension/module/example_plugin.php`

Add language variants by creating additional directories for different locales.

## 📄 Configuration

Settings are stored in the OpenCart settings table with the prefix `module_example_plugin_`:
- `module_example_plugin_status` - Module enable/disable status

Additional settings can be added in the admin form and saved to the same prefix.

## 🐛 Troubleshooting

**Module not appearing after installation:**
- Clear OpenCart cache
- Verify `install.json` is present
- Check file permissions
- Review error logs in `system/log/`

**Database errors:**
- Ensure install() method is executed
- Check database user has CREATE/DROP table permissions
- Verify table prefix configuration

**Permission denied errors:**
- Verify user group permissions were added
- Check admin user role permissions
- Clear session data

## 📖 OpenCart 4 Documentation

For more information:
- [OpenCart 4 Documentation](https://docs.opencart.com/)
- [Extension Development Guide](https://docs.opencart.com/development/extension/)
- [OCMOD Documentation](https://docs.opencart.com/development/ocmod/)

## 👨‍💻 Author

Created by Saqib Ashraf  
Website: [saqibashraf.net](http://www.saqibashraf.net)

## 📄 License

See the LICENSE file for license information.

## 🤝 Contributing

This is a sample boilerplate for learning and development purposes. Feel free to modify and extend it for your specific needs.

---

**Version**: 1.0  
**Last Updated**: November 2025  
**OpenCart Version**: 4.x
