# Wordpress and You

Wordpress is very confusing, but here are some conventions that everyone must abide by or Brian will break yo' legs.

## Filenames and Directory Structure
1. Do not use underscores in filenames.
  
  Bad: ```"_something.php"```

  Good: ```"something.php"```  

2. Keep EVERYTHING in the wp-content folder. Do not modify, move, add anything outside of this. NO EXCEPTIONS.
3. The following should be used for folder names. Do not stray from these. This has been done to ensure consistency between Rails and Wordpress. 

  Stylesheets should be in folder ```stylesheets``` (do not call it css)
  
  Scripts should be in folder ```javascripts``` (do not call it scripts, js)
  
  Images should be in folder ```images``` (do not call it imgs, img)
4. Use the ```style.css``` file found the in the wp-content folder as the primary CSS style sheet. Do NOT create an application.css file in the ```stylesheets``` folder.


## OMG THERE'S AN ERROR. WTF?!
1. There is a .htaccess file at the root of the Wordpress directory. The file should look something like this:
  ```php
  # BEGIN WordPress   
  <IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /mirra/
  RewriteRule ^index\.php$ - [L]  
  RewriteCond %{REQUEST_FILENAME} !-f  
  RewriteCond %{REQUEST_FILENAME} !-d  
  RewriteRule . /mirra/index.php [L]  
  </IfModule>
  # END WordPress
  ```
  
  If you need to turn on Error Reporting just add ```php_flag display_errors on``` to the top of the file. This goes for PHP in general. If you're working on a PHP project and need to see errors, make a .htaccess file and put the display_errors flag in. 

**Warning:** Make sure you turn display_errors off in production.


## wp-config.php file
1. Don't fuck this file up.


## Plugins and Taxonomies
1. Create all custom taxonomies and plugins in the ```wp-content/plugins``` folder. Do NOT put in the functions.php file or in the theme directory.

  This is done to ensure plugins and taxonomies work across multiple themes.
2. Plugins should be unique but overtly obvious as to what they accomplish.
3. Do not use underscores in filenames.
4. Don't install bloatware plugins for clients. If it's something simple, consider building it yourself. If it's something complicated, customize their plugin to your needs.
