Apache uses external modules, called dynamic shared objects (DSOs), for basic and advanced functions; there is not much to Apache without these modules. Apache also uses modules to extend its functionality. For example, modules can process scripts written in Perl, PHP, Python, and other languages; use several different methods to authenticate users; facilitate publishing content; and process nontextual content, such as audio. The list of modules written by the ASF and third-party developers is constantly growing. For more information refer to “Modules” on page 968.

![](bbox=[0.11, 0.24, 0.2, 0.28])

You can use the HTTP Server Configuration window (system-config-httpd package) to configure Apache graphically. Open this window by giving the command system-config-httpd from an Enter a Command window (Alt+F2) or a terminal emulator. Click Help in this window for more information.

# # More information

+   - **Local**  
+   
+   Apache documentation: With Apache running and the `httpd-manual` package installed, point a browser at `server/manual`. On the server system, substitute `localhost` for *server*; from a remote system, substitute the name or IP address of the Apache server for *server*. If Apache is not running, point a browser on the server system only at `/usr/share/httpd/manual/index.html`.
+   
+   `apachectl` and `httpd` man pages
+   
+   Apache directives: `server/manual/mod/directives.html`
+   
+   SSI directives: `server/manual/howto/ssi.html`
+   - **Web**
+   
+   Apache documentation: httpd.apache.org/docs/2.4
+   
+   Apache directives: httpd.apache.org/docs/2.4/mod/directives.html
+   
+   Apache Software Foundation (newsletters, mailing lists, projects, module registry, and more): www.apache.org
+   
+   `webalizer`: www.webalizer.org
+   
+   `awstats`: awstats.sourceforge.net
+   
+   `mod_perl`: perl.apache.org
+   
+   `mod_php`: www.php.net
+   
+   `mod_python`: www.modpython.org; see `mod_wsgi`
+   
+   `mod_ssl`: www.modssl.org
+   
+   `mod_wsgi`: wsgi.readthedocs.org/en/latest, code.google.com/p/modwsgi
+   
+   MR TG: oss.oettiker.ch/mrtg
+   
+   SNMP: net-snmp.sourceforge.net
+   
+   SSI directives: httpd.apache.org/docs/2.4/howto/ssi.html

# # Notes

+   - **Terms: Apache and httpd**  
+   
+   *Apache* is the name of a server that serves HTTP and other content. The Apache daemon is named *httpd* because it is an HTTP server daemon. This chapter uses the terms *Apache* and *httpd* interchangeably.
+   - **Terms: server and process**
+   
+   An Apache *server* is the same thing as an Apache *process*. An Apache child process exists to handle incoming client requests; hence it is referred to as a server.