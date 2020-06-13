# Block access on wp-config.php

<IfModule mod_headers.c>
  Header set X-XSS-Protection "1; mode=block"
  Header always append X-Frame-Options SAMEORIGIN
  Header set X-Content-Type-Options nosniff
</IfModule>
<files wp-config.php>
order allow,deny
deny from all
</files>

# Enable automatic updates for WordPress core
     in wp-config.php
     add_filter( 'auto_update_theme', '\__return_true' );

# Enable automatic upgrades plugins for WordPress  
     in wp-config.php
     add_filter( 'auto_update_plugin', '\__return_true' );

# Enable automatic upgrade themes for WordPress core
     in wp-config.php
     add_filter( 'auto_update_theme', '\__return_true' );



# wp-security-audit-log

# Change the Login Error Messages

    functions.php

    function custom_wordpress_error_message(){
        return 'That was not quite correct...';
    }
    add_filter( 'login_errors', 'custom_wordpress_error_message' );

# Add Salt Keys in wp-config.php
     [salt key](https://api.wordpress.org/secret-key/1.1/salt/)

# Disable the Theme and Plugin Editor
     goto wp-config.php and paste the following line

     define('DISALLOW_FILE_EDIT', true);

# Disable PHP Error Reporting
     goto wp-config.php

        error_reporting(0);
        @ini_set(‘display_errors’, 0);

# Remove the WordPress Version
     functions.php

    function remove_wordpress_version_number() {
        return '';
    }
    add_filter('the_generator', 'remove_wordpress_version_number');

    function remove_version_from_scripts( $src ) {
         if ( strpos( $src, 'ver=' . get_bloginfo( 'version' ) ) )
            $src = remove_query_arg( 'ver', $src );
            return $src;
        }
    add_filter( 'style_loader_src', 'remove_version_from_scripts');
    add_filter( 'script_loader_src', 'remove_version_from_scripts');

# Core Directories Permissions
    - Files 640
         find /path/to/your/wordpress/install/ -type f -exec chmod 640 {} \;
    - Folders 750       
         find /path/to/your/wordpress/install/ -type d -exec chmod 750 {} \;

# Prevent Directory Listing
    Options All -Indexes


# Lock Out Specific IP Addresses
    order allow,deny
    deny from 456.123.8.9
    allow from all

# Restrict Admin Access to Specific IP Address
    ErrorDocument 401 default
    ErrorDocument 403 default

    <Files wp-login.php>
    Order deny,allow
    Deny from all
    Allow from 198.101.159.98
    </Files>

# Secure wp-include
    <IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteBase /
    RewriteRule ^wp-admin/includes/ - [F,L]
    RewriteRule !^wp-includes/ - [S=3]
    RewriteRule ^wp-includes/[^/]+\.php$ - [F,L]
    RewriteRule ^wp-includes/js/tinymce/langs/.+\.php - [F,L]
    RewriteRule ^wp-includes/theme-compat/ - [F,L]
    </IfModule>

# Disable Script Injection
    Options +FollowSymLinks
    RewriteEngine On
    RewriteCond %{QUERY_STRING} (<|%3C).\*script.\*(>|%3E) [NC,OR]
    RewriteCond %{QUERY_STRING} GLOBALS(=|[|%[0-9A-Z]{0,2}) [OR]
    RewriteCond %{QUERY_STRING} \_REQUEST(=|[|%[0-9A-Z]{0,2})
    RewriteRule ^(.\*)$ index.php [F,L]

# Prevent PHP code execution from uploads folder
    <Directory "/var/www/wp-content/uploads/">
    <Files "\*.php">
    Order Deny,Allow
    Deny from All
    </Files>
    </Directory>

# Restrict Access to PHP files
    RewriteCond %{REQUEST_URI} !^/wp-content/plugins/file/to/exclude\.php
    RewriteCond %{REQUEST_URI} !^/wp-content/plugins/directory/to/exclude/
    RewriteRule wp-content/plugins/(.*\.php)$ - [R=404,L]
    RewriteCond %{REQUEST_URI} !^/wp-content/themes/file/to/exclude\.php
    RewriteCond %{REQUEST_URI} !^/wp-content/themes/directory/to/exclude/
    RewriteRule wp-content/themes/(.*\.php)$ - [R=404,L]

# Restrict Access to .htaccess, php.ini, wp-config.php

    <FilesMatch "^.\*(error_log|wp-config\.php|php.ini|\.[hH][tT][aApP].\*)$">
    Order deny,allow
    Deny from all
    </FilesMatch>

Adjust the name of your php.ini file if needed (e.g. php5.ini or php7.ini). Be sure to place the code outside the #BEGIN WordPress and #END WordPress brackets. Everything inside that space can be edited by WordPress and might cause you to lose your changes.


# WordPress Manual backup
- https://websitesetup.org/wordpress-backup/

# WordPress change table prefix
- https://www.wpbeginner.com/wp-tutorials/how-to-change-the-wordpress-database-prefix-to-improve-security/
- https://www.developerdrive.com/2018/03/how-to-change-the-wordpress-database-prefix-to-improve-security/



# How to fix a hacked website
- https://www.wpbeginner.com/beginners-guide/beginners-step-step-guide-fixing-hacked-wordpress-site/


# 2FA
- https://wordpress.org/plugins/miniorange-2-factor-authentication/
- duo

# Disable TLS 1.0 and 1.1
- https://www.globalsign.com/en-in/blog/disable-tls-10-and-all-ssl-versions/


# Reference
[1](https://websitesetup.org/wordpress-security/)
[2](https://www.wpbeginner.com/wordpress-security/)
[3](https://www.wordfence.com/learn/wordpress-security-checklist/)
[4](https://wpsecuritychecklist.org/items/)
