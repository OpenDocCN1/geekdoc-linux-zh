For a site with heavy traffic, configure the Web server so that a single HTTP daemon can serve multiple virtual hosts. Of course, this recommendation implies that there is only one configuration file. In that configuration file, use the VirtualHost directive to configure each virtual host.

Most ISPs use the VirtualHost capability of Apache HTTP server to provide virtual Web sites to their customers. Unless you pay for a dedicated Web host, you typically get a virtual site where you have your own domain name but share the server and the actual host with many other customers.

The syntax of the VirtualHost directive is as follows:

```
<VirtualHost hostaddr>
... directives that apply to this host
</VirtualHost>
```

With this syntax, you use <VirtualHost> and </VirtualHost> to enclose a group of directives that applies only to the particular virtual host identified by the hostaddr parameter. The hostaddr can be an IP address or the fully qualified domain name of the virtual host.

You can place almost any Apache directives within the <VirtualHost> block. At a minimum, Webmasters include the following directives in the <VirtualHost> block:

+   - **DocumentRoot**, which specifies where this virtual host's documents reside
+   - **Servername**, which identifies the server to the outside world (this should be a registered domain name DNS supports)
+   - **ServerAdmin**, the e-mail address of this virtual host's Webmaster
+   - **Redirect**, which specifies any URLs to be redirected to other URLs
+   - **ErrorLog**, which specifies the file where errors related to this virtual host are to be logged
+   - **CustomLog**, which specifies the file where accesses to this virtual host are logged

When the server receives a request for a document in a particular virtual host's DocumentRoot directory, it uses the configuration parameters within that server's <VirtualHost> block to handle that request.