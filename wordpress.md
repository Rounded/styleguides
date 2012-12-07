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
1. Don't mess this file up.
2. Wrap the database connection details in an ```if``` statement so that there is difference between local and production. For example:
  
  ```php
  if($_SERVER['HTTP_HOST']=='localhost:8888'){
      define('DB_NAME', 'mirra');
	  define('DB_USER', 'root');
	  define('DB_PASSWORD', 'root');
	  define('DB_HOST', 'localhost');
	  define('DB_CHARSET', 'utf8');
	  define('DB_COLLATE', '');
  } else {
	  define('DB_NAME', 'db118166_dbname');
	  define('DB_USER', 'db118166_administrator');
	  define('DB_PASSWORD', 'password123!');
	  define('DB_HOST', 'internal-db.s118166.gridserver.com');
	  define('DB_CHARSET', 'utf8');
  	  define('DB_COLLATE', '');	
  }
  ```
3. If it's a multi-site install, do the same thing:
  ```php
  if($_SERVER['HTTP_HOST']=='bitpressco.dev'){
    	define( 'DOMAIN_CURRENT_SITE', 'bitpressco.dev' );
  } else {
	  define( 'DOMAIN_CURRENT_SITE', 'bitpress.co' );
  }
  ```
4. Once the database name and multi-site url has been established, try not to change it. It will mess things up for people pulling it down on Github.


## Understand the Template Hierarchy
1. Read this entire document: http://codex.wordpress.org/Template_Hierarchy
2. Make sure you understand what it means to override certain files. For example a general ```page.php``` will be overriden by ```page-about.php```
	This means: don't make files like "the_header.php" because:
	1. header.php is a reserved file for Wordpress and is best to be overriden. The function ```get_header();``` won't work when the file is called something different.

## Plugins and Taxonomies
1. Create all custom taxonomies and plugins in the ```wp-content/plugins``` folder. Do NOT put in the functions.php file or in the theme directory.

  This is done to ensure plugins and taxonomies work across multiple themes.
2. Plugins should be unique but overtly obvious as to what they accomplish.
3. Do not use underscores in filenames.
4. Don't install bloatware plugins for clients. If it's something simple, consider building it yourself. If it's something complicated, customize their plugin to your needs.
5. Don't use ```echo``` ever in a plugin file. Always return the data.