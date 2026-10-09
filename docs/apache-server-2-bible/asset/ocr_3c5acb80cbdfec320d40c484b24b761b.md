```
# Do not forget to change the IP address, ServerName, 
# DocumentRoot, ScriptAlias,
# TransferLog, and ErrorLog directive values with whatever is
# appropriate for your
# actual configuration setup.
<VirtualHost 206.171.50.5:1080>
ServerName www.mycompany.com
DocumentRoot "www/mycompany/staging/htdocs"
ScriptAlias /cgi-bin/ "/www/mycompany/staging/cgi-bin/"
TransferLog logs/staging-server.access.log
ErrorLog logs/staging-server.error.log
</VirtualHost>

<VirtualHost 206.171.50.5:8080>
ServerName www.mycompany.com
DocumentRoot "www/mycompany/developer/htdocs"
ScriptAlias /cgi-bin/ "/www/mycompany/developer/cgi-bin/"
TransferLog logs/developer-server.access.log
ErrorLog logs/developer-server.error.log
</VirtualHost>
```

![](bbox=[0.13, 0.6, 0.22, 0.72])

In the preceding example, the same IP address is used in both virtual hosts, but different ports are specified in the <VirtualHost . . . > container. The IP address is the same as the main server, www.mycompany.com. The ServerName directive is set to the main server name as well. Your main server configuration will be as usual.

The http://www.mycompany.com:1080 URL can be used to access the staging site; to access the developer site, this URL can be used: http://www.mycompany.com:8080.

# Using multiple Apache (main) server processes

You should use more than one (main) server process if you plan to experiment with Apache itself as part of your Web development phase. Create three sets of configuration files, with each set pointing to a different DocumentRoot and ScriptAlias. After you have done that, you can start up the three Apache (main) server processes as follows from the main directory where you installed Apache (e.g. /usr/local/apache):

```
httpd -f conf/httpd.conf
httpd -f conf/staging/httpd.conf
httpd -f conf/developer/httpd.conf
```

When you decide to compile a new version of Apache and run it under the developer server, you can simply feed it the configuration file for the developer server. For example, if you’ve decided to add a new module and want to see the effect of the module on