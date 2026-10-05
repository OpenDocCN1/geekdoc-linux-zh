# The Apache Web Server • 137

servlets, Perl, FastCGI (a.k.a. persistent CGI), HTTP cookies, server-side includes, and Secured Sockets Layer.

The parade of modules doesn't stop there, however. The Apache HTTP server was designed to take full advantage of the power of modular programming, which resulted in an easily extensible and customizable server. Anyone can extend the Apache HTTP server by creating a custom Apache module.

Sometimes, after a particular custom module becomes heavily used and well regarded, the Apache Group will add it to the core set of modules included in the Apache download. Many frequently used and recommended third-party modules are freely available from http://modules.apache.org.

# The Apache Code

The add-on Apache modules can be statically or dynamically bound to the HTTP server program. As mentioned, you dynamically bind an Apache module by specifying the AddModule directive and the module name in a configuration file. For speed, you can statically bind Apache modules to the Apache HTTP server by recompiling the server program. The server program is called httpd (which stands for “Hypertext Transfer Protocol Daemon”). You can think of httpd as a demon that hides in the background, waiting for requests from people trying to gain Web-based access to your host via TCP/IP and HTTP. The Apache HTTP server is delivered with the binary executable httpd program, the complete C source code for httpd, and the C code for all of the standard Apache module extensions.

# Apache Startup

The Apache Web server can be started by invoking the httpd command from a terminal session, but most distributions have a startup script that simplifies Apache. Red Hat’s script is also called httpd, and it exists in the /etc/rc.init.d/ directory. If you attempt to invoke the script without any options, you’ll receive the following message:

```
$ /etc/rc.init.d/httpd
Usage: httpd [start|stop|restart|reload|condstart|status]
```

This helpful message tells you the arguments required by the httpd script. The status option will tell you whether or not Apache is active, and the other options are obvious.

When Apache is started, it looks for the httpd.conf file in /etc/httpd/conf. You might be a little overwhelmed the first time you look at that httpd.conf, so we’ve supplied a minimal version in Figure 9.1 Apache expects a particular directory structure:

+   - A directory for the httpd.conf file
- A directory called htmldocs to hold the hypertext documents Apache is to serve
- A directory called logs to hold various pieces of information that Apache can be configured to log