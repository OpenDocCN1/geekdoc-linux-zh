# Hosting Virtual Web Sites

Apache’s httpd.conf configuration file separates virtual host configuration from the main server configuration using the <VirtualHost> container. For example, look at the following httpd.conf file:

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

In the preceding file, two virtual Web sites called vhost1.server.com and vhost2.server.com are defined in their own <VirtualHost> containers. All the directives included in each of the <VirtualHost> containers apply only to the virtual host it serves. So, when a Web browser requests http://vhost1.server.com/index.html the Apache Web server looks for the index.html page in /www/vhost1/htdocs directory. Similarly,