the browser should load the test page shown in Figure 29-1:

![](bbox=[0.335, 0.09, 0.715, 0.315])

Figure 29-1

If the desktop environment is unavailable, connect either from another system on the same local network as the server, or use the external IP address assigned to the system if it is hosted remotely.

# 29.7 Configuring the Apache Web Server for Your Domain

The next step in setting up your web server is configuring it for your domain name. To configure the web server, begin by changing directory to /etc/httpd, which, in turn, contains several files and sub-directories. Change directory into the conf sub-directory, where you will find a file named httpd.conf containing the configuration settings for the Apache server.

Edit the httpd.conf file using your preferred editor with super-user privileges to ensure you have permission to access and modify the file. Once loaded, several settings need to be changed to match your environment.

The most common way to configure Apache for a specific domain is to add virtual host entries to the httpd.conf file. This allows a single Apache server to support multiple websites simply by adding a virtual host entry for each site domain. Within the httpd.conf file, add a virtual host entry for your domain as follows:

```
<VirtualHost *:80>
    ServerAdmin feedback@myexample.com
    ServerName www.myexample.com
    DocumentRoot /var/www/myexample
    ErrorLog logs/myexample_error_log
    CustomLog logs/myexample_access_log combined
</VirtualHost>
```

The ServerAdmin directive in the above virtual host entry defines an administrative email address for people wishing to contact the webmaster for your site. Change this to an appropriate email