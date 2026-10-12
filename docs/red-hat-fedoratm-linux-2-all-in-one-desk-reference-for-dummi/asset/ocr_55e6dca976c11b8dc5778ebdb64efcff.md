With this syntax, you use <VirtualHost> and </VirtualHost> to enclose a group of directives that applies only to the particular virtual host identified by the hostaddr parameter. The hostaddr can be an IP address or the fully qualified domain name of the virtual host.

You can place almost any Apache directives within the <VirtualHost> block. At a minimum, Webmasters include the following directives in the <VirtualHost> block:

+   * DocumentRoot, which specifies where this virtual host's documents reside
+   * ServerName, which identifies the server to the outside world (this name is a registered domain name DNS supports)
+   * ServerAdmin, the e-mail address of this virtual host's Webmaster
+   * Redirect, which specifies any URLs to be redirected to other URLs
+   * ErrorLog, which specifies the file where errors related to this virtual host are to be logged
+   * CustomLog, which specifies the file where accesses to this virtual host are logged

When the server receives a request for a document in a particular virtual host's DocumentRoot directory, it uses the configuration parameters within that server's <VirtualHost> block to handle that request.

Here is a typical example of a <VirtualHost> directive that sets up the virtual host www.lnbssoft.com:

```
<VirtualHost www.lnbssoft.com>
 DocumentRoot /home/naba/httpd/htdocs
 ServerName www.lnbssoft.com
 ServerAdmin webmaster@lnbssoft.com
 ScriptAlias /cgi-bin/ /home/naba/httpd/cgi-bin/
 ErrorLog /home/naba/httpd/logs/error_log
 CustomLog /home/naba/httpd/logs/access_log common
 </VirtualHost>
```

Here the name common in the CustomLog directive refers to the name of a format defined earlier in the httpd.conf file by the LogFormat directive, as follows:

```
LogFormat "%h %l %u %t "%>r" %s> %s" common
```