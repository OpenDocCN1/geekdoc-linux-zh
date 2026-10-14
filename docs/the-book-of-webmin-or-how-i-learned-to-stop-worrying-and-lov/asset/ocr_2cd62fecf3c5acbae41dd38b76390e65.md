# Address and Port

If your system has multiple interfaces, Apache will answer on any of them by default on port 80. However, you can configure your virtual server to only answer on one address using this option. You can also configure a different port here.

# Document Root

This is the root directory, from whence the paths to access objects on your server will begin. This option configures the DocumentRoot [http://httpd.apache.org/docs/mod/core.html#documentroot] directive.

# Server Name

When using name based virtual servers, this name should match the name under which this server should answer. This is also used when creating redirection URLs. If not specified Apache will try to deduce it from the IP address, which isn't always reliable. This option correlates to the ServerName [http://httpd.apache.org/docs/mod/core.html#servername] directive.

# Tutorial: A Basic Apache Configuration

Apache is an extremely large and feature-rich piece of software. Approaching it for the first time can be daunting. Luckily, it is extremely easy to install, configure, and maintain as long as you proceed with care and pay attention to the documentation relevant to your installation and environment. Installation of Apache is not covered here, as it is well documented on the Apache website, and it is also very likely that your OS vendor provides a suitable package to make installation automatic. What will be covered is the initial hurdle of setting up Apache to serve HTML web pages. The next section will take the configuration one step further to configuring a virtual hosting service. Later, a section in the BIND module chapter will cover adding /usr/w service for your web server.

# Configuring Apache Paths

> **NOTE** *If you've installed Apache from a package from your OS vendor or if your vendor does not provide a package and it has been installed in the default location selected by the program, you can probably skip this section and proceed to the next section covering initial module selection. For any supported OS, Webmin has a configuration file that includes sensible default paths for the programs that it administers. These configurations assume an installation in the default location for your operating system. So, for example, on a Red Hat Linux system, Webmin will expect to find the httpd.conf file in the /etc/httpd/conf directory, while on Solaris it is expected to be in /usr/local/apache/conf.*

Webmin works directly with the Apache configuration files, and so must know where to find them. When you browse to the Apache module of Webmin for the first time you may be greeted with an error stating that the configuration file could not be found. You'll need to locate the configuration files, as well as the Apache binary, and possibly startup and shutdown scripts for your system, and