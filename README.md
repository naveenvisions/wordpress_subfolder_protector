# wordpress_subfolder_protector

Exclude a path from WordPress using .htaccess redirects (Apache)

Directory structure:

    -otherfiles
    ---public_html
    ---.htaccess
    -----sub-folder
    ---.htaccess

Wordpress root .htaccess file, which is under public_html folder i.e "/home/user/public_html/.htaccess"

    # BEGIN WordPress
    # The directives (lines) between "BEGIN WordPress" and "END WordPress" are
    # dynamically generated, and should only be modified via WordPress filters.
    # Any changes to the directives between these markers will be overwritten.
    <IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]
    RewriteBase /

    RewriteCond %{REQUEST_URI} !^/(sub-folder|sub-folder/.*)$ 
    ErrorDocument 401 default

    RewriteRule ^index\.php$ - [L]
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule . /index.php [L]
    </IfModule>

The sub-folder .htaccess has password the protect feature, so similar to this:

    AuthType Basic
    AuthName "restricted area"
    AuthUserFile /home/user/public_html/sub-folder/.htpasswd
    require valid-user


save the user user name and password under the file .htpasswd

    demo:$2y$10$7CiBmbZAgl4bcVs0LL6Ce.8iZ2Czy72RLhbZpa/Zkk2DHj2ABKsWq #demo:Demo@123

