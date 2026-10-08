# Chapter 10. Apache HTTP Server

# 10.2.4.6. The mod_python Module

The configuration for mod_python has been moved from httpd.conf into the file /etc/httpd/conf/mod_python.conf. For this file to be loaded, and hence for mod_python to work, the statement Include conf.d* must be in the httpd.conf as described in Section 10.2.1.3 Dynamic Shared Object (DSO) Support.

# 10.2.4.7. PHP

The configuration for PHP has been moved from httpd.conf into the file /etc/httpd/conf/php.conf. For this file to be loaded, the statement Include conf.d*/conf must be in the httpd.conf as described in Section 10.2.1.3 Dynamic Shared Object Support.

The PHP is now implemented as a filter and must therefore be enabled in a different manner. Section 10.2.4 Modules and Apache HTTP Server 2.0 for more filters.

Under Apache HTTP Server 1.3, PHP was implemented using the following directives:

```
AddType application/x-httpd-php .php
AddType application/x-httpd-php-source .phps
```

Under Apache HTTP Server 2.0, use the following directives:

```
<Files *.php>
SetOutputFilter PHP
SetInputFilter PHP
</Files>
```

In PHP 4.2.0 and the default set of predefined variables which are available in the global scope has changed. Input and server variables are, by default, not placed directly into the global scope. This change may cause scripts to break. Revert to the old behavior by register_globals to On in the file /etc/php.ini.

For on this, refer to the following URL for details concerning the global scope changes:

+   - http://php.net/release_4_1_0.php

# 10.3. After Installation

After installing the httpd package, the Apache HTTP Server’s documentation is available by installing the httpd-manual package and navigating a browser to http://localhost/manual/ or browse the Apache documentation available at http://apache.org/docs-2.0.

The Apache HTTP Server’s documentation contains a full list and complete descriptions of all configuration options. For the convenience, this chapter provides short descriptions of the configuration directives used by Apache HTTP 2.0.

The version of the Apache HTTP Server included with Red Linux includes the ability to set secure web servers using SSL encryption provided by the mod_ssl and openssl packages. When looking through the configuration files, be aware that it includes both a non- and secure web server. The secure web server runs as a virtual host, which is configured in the /etc/httpd/conf/ssl.conf. For more information about virtual hosts, see Section 10.8 Virtual Hosts. For information on configuring a secure virtual host, Section 10.8.1 Setting Up Virtual Hosts. For information on setting up an Apache HTTP Server Secure Configuration see the chapter titled Apache HTTP Server Configuration in the Red Hat Linux Custom Guide.