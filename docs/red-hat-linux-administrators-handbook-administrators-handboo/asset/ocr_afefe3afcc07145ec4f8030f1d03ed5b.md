# Compiling the proxy module

If you are using the APACI interface to compile and install Apache, then building a new Apache executable with the proxy module is as easy as performing the following steps in your Apache source distribution directory:

+   1. If you are running the configure script for the first time, enter the following command:
+   
+       ./configure \
+           --prefix=/dir/where/you/want/to/install/apache \
+           --enable-module=proxy
+   
+       Conversely, if you have already run the configure script to compile Apache, enter the following:
+   
+       ./config.status --enable-module=proxy
+   
+       Your previous configuration options will be applied when creating a new configuration file.
+   
+   2. Run the make command. If it returns no error messages, run the make install command to install the newly compiled Apache executable in the appropriate directory.

# Proxy module directives

The proxy module for Apache comes with the set of directives that you need to use the module. All of these directives are usable in both the main server configuration and any virtual server configuration context.

ProxyRequests on | off

This directive allows you to enable or disable the caching proxy service. However, it does not affect the functionality of the ProxyPass directive. The default value is off.

ProxyRemote match remote-proxy-server-URL

This directive enables you to interface your proxy server with another proxy server. The value of match can be either the name of a URL scheme (http, ftp, and so on) or a partial URL.

remote-proxy-server-URL can be http://remote-proxy-hostname:port. Currently, only the HTTP protocol is supported. In other words, you