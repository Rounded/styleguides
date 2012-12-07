# Wordpress and You

Wordpress is very confusing, but here are some conventions that everyone must abide by or Brian will break yo' legs.

## Filenames and Directory Structure
1. Do not use underscores in filenames in the wp-content folder. It doesn't make any sense and ends up causing a headache when trying to search for files. 
  
  Bad: ```"_something.php"```

  Good: ```"something.php"```  

2. Keep EVERYTHING in the wp-content folder. Do not modify, move, add anything outside of this. NO EXCEPTIONS.
3. The following should be used for folder names. Do not stray from these. This has been done to ensure consistency between Rails and Wordpress. 

  Stylesheets should be in folder ```stylesheets``` (not css)
  
  Scripts should be in folder ```javascripts``` (not scripts, js)
  
  Images should be in folder ```images``` (not imgs, img)
4. Use the ```style.css``` file found the in the wp-content folder as the primary CSS style sheet. Do NOT create an application.css file in the ```stylesheets``` folder.
5. 