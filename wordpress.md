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
5. Keep filenames all lowercase and hyphenated.

	GOOD: ```page-about-us.php```
	
	BAD: ```page-About_Us.php```
6. Use page-home.php for the Home Page if you are going to override it.
7. Use archive-slug.php for pages with custom post types.
8. Use single-slug.php for individual custom post types.

## Admin
1. Page names on the back-end should be equivalent to the ones in the front-end. Obviously, this will change over time, but atleast for the beginning, keep 'em up to date!
2. Slug should match the page name / only use hyphens!
3. Pages are for PAGE content only. If it's an entity of some sort or something global, make it a custom post-type.
4. Order the menu in the Admin area as Pages > Posts > Comments > Media > Custom Post Types

## Advanced Custom Fields
1. Naming conventions should be:
	1. Custom Post Types (singular item) - [Name] Post, i.e. "Book Post"
	2. Archive Pages - [Names] Archive, i.e. "Books Archive"
	3. Single Pages - [Name] Page, i.e. "Book Page"
	4. Generic Pages - [Name] Page
	
## Functions.php File
1. Custom post types should be in plugins folder, not functions.php
2. Custom Admin UI in a plugins folder called "custom-admin-ui-rounded"
3. The functions.php file should be used more for global helpers / front end manipulation
4. Never echo in functions.php, always return
5. Put custom functions at the TOP of functions.php, and draw a line where everything below is generic WP garbage

## Approved Plugins
1. Advanced Custom Fields
2. Contact Form 7 + Dynamic Text Extension
3. Members (Role editing)
4. The Events Calendar
5. Simple Local Avatars
6. Post Types Order

## Oh no – there's an error!
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

## The Database
1. Do **not** use local databases anymore. If you create a page, or do something locally, it won't necessarily be reflected for all users.
2. Head to media temple and create a database. This way all database changes will be consistent for each user who is working on a project.
3. The dev database should end in "_dev" while the production one can just be the github_name.

Note: This means that you won't be able to develop the site without an internet connection.

### How to Create a Database on Media Temple
3. Head to "Manage Databases" on Media Temple https://ac.mediatemple.net/services/manage/grid/databases/index.mt?id=524593
4. Click "Add a database" and enter the name. Make sure the name reflects which environment it's being used in.
5. Click "Global Settings" and click the permissions button next to your user account. Give yourself read/write permission to the database.
6. You can find database connection details here: https://ac.mediatemple.net/services/guide/gs/index.mt?id=524593



## Understand the Template Hierarchy
1. Read this entire document: http://codex.wordpress.org/Template_Hierarchy
2. Make sure you understand what it means to override certain files. For example a general ```page.php``` will be overriden by ```page-about.php```
	This means: don't make files like "the_header.php" because:
	1. header.php is a reserved file for Wordpress and is best to be overriden. The function ```get_header();``` won't work when the file is called something different.

## Plugins, Taxonomies, Custom Post Types
1. Create all custom taxonomies, post-types, and plugins in the ```wp-content/plugins``` folder. Do NOT put in the functions.php file or in the theme directory.

  This is done to ensure plugins, taxonomies, and post-types work across multiple themes.
2. Don't install bloatware plugins for clients. If it's something simple, consider building it yourself. If it's something complicated, customize their plugin to your needs.
3. Don't use ```echo``` ever in a plugin file. Always return the data.
