Go to httpd.conf in Apache folder and find the following lines:

DocumentRoot "c:/wamp/www"
<Directory "c:/wamp/www">
    # ...Stuffs in here
    Options Indexes FollowSymLinks
    # ...Stuffs in here
    AllowOverride All
    #
    # Controls who can get stuff from this server.
    #
    Require all granted
</Directory>
Then replace the last line within <Directory> tag for:

     Order Deny,Allow
     Deny from all
     Allow from 127.0.0.1
     Allow from ::1
     Allow from localhost
</Directory>
Add a virtual host for your laravel application, go to httpd-vhosts.conf and add the following lines:

<VirtualHost *:80>
    DocumentRoot "D:/.../your-laravel-app-path/public"
    ServerName yourservername.dev
    <Directory "D:/.../your-laravel-app-path/public">
        AllowOverride All
        Order deny,allow
        Allow from all
        Require all granted
    </Directory>
</VirtualHost>
Restart all your apache services

This should do it, i'm using wamp on Windows and works for me.
