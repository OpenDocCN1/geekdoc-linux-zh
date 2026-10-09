Apache’s configuration file httpd.conf separates virtual host configuration from the main server configuration using the `<VirtualHost>` container. For example, look at the httpd.conf file in Listing 6-1.

# Listing 6-1: httpd.conf

```
# httpd.conf file

ServerName main.server.com
Port 80
ServerAdmin mainguy@server.com
DocumentRoot "/www/main/htdocs"

ScriptAlias /cgi-bin/ "/www/main/cgi-bin/"
Alias /images/ "/www/main/htdocs/images/"

<VirtualHost 192.168.1.100>
ServerName vhost1.server.com
ServerAdmin vhost1_guy@vhost1.server.com
DocumentRoot "/www/vhost1/htdocs"
ScriptAlias /cgi-bin/ "/www/vhost1/cgi-bin/"
</VirtualHost>

<VirtualHost 192.168.1.110>
ServerName vhost2.server.com
ServerAdmin vhost2_guy@vhost2.server.com
DocumentRoot "/www/vhost2/htdocs"
ScriptAlias /cgi-bin/ "/www/vhost2/cgi-bin/"
Alias /images/ "/www/vhost2/htdocs/images/"
</VirtualHost>
```

Listing 6-1 shows two virtual Web sites called vhost1.server.com and vhost2. server.com, which are defined in their own `<VirtualHost>` containers. All the directives included in each of the `<VirtualHost>` containers apply only to the virtual host it serves. So, when a Web browser requests http://vhost1.server.com/index.html, the Apache Web server looks for the index.html page in /www/ vhost1/htdocs directory. Similarly, when a Web browser requests http://vhost2. server.com/cgi-bin/hello.pl, the script is run from the /www/vhost2/ cgi-bin directory.

However, many directives in the main server configuration (that is, any directive outside of the `<VirtualHost>` container) still apply to virtual hosts that do not override them. For example, the vhost1.server.com in Listing 6-1 does not have an Alias directive for the /images/ directory alias. So, when a Web browser requests http://vhost1.server.com/images/prett_y_pic.gif file the picture is served from /www/main/htdocs/images directory. Because the vhost2. server.com does override the /images/ alias with its own, a similar request is served from /www/vhost2/htdocs/images directory instead.