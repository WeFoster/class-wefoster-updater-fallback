# WeFoster Updater Fallback Class

This class provides fallback logic when the WeFoster Dashboard plugin is not active. Require this class to register plugins and themes. When the dashboard is present, using `wefoster_updater()->add_theme|plugin()` will handle the actual updating, but without it, this will display a notice to install or activate the dashboard plugin.

NOTE: Adding your product should happen BEFORE the `'init'` hook! So use `'plugins_loaded'` for plugins and `'after_setup_theme'` for themes.

### Example:

PLUGIN: Add your plugin to the updatable WeFoster queue
```
<?php
    function wefoster_update_my_plugin() {
       // Load fallback file when without WeFoster Dashboard
       if ( ! function_exists( 'wefoster' ) ) {
            require_once( '{...}/class-wefoster-updater-fallback.php' );
       }

       // Add Plugin
       wefoster_updater()->add_plugin( __FILE__ );
    }
    add_function( 'plugins_loaded', 'wefoster_update_my_plugin' );
?>
```

THEME: Add your theme to the updatable WeFoster queue
```
<?php
    function wefoster_update_my_theme() {
       // Load fallback file when without WeFoster Dashboard
       if ( ! function_exists( 'wefoster' ) ) {
            require_once( '{...}/class-wefoster-updater-fallback.php' );
       }

       // Add Theme
       wefoster_updater()->add_theme( 'my-theme' );
    }
    add_function( 'after_setup_theme', 'wefoster_update_my_theme' );
?>
```