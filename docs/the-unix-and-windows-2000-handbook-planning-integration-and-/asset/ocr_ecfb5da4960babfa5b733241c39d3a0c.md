See Chapter 5, "Upgrades, Patches, Service Packs, and Hot Fixes", for instructions on installing packages with rpm or GNU rpm on a Red Hat Linux workstation.

# Apache Configuration

The Apache configuration files are located under the /etc/httpd directory. The conf directory contains the main configuration files for the Web server. Table 16.1 contains the name and content of each file.

The logs directory contains the error logging file (error_logs) and the access logging file (access_log). The error logging level is set to warn. The warn level logs information on emergencies, alerts, critical conditions, errors, and warning conditions. The access logging file logs all requests to the Web server. The access log is written in the Common Log Format (CLF). The CLF writes a separate line of information for each request to the log file in the following format (each field is separated by spaces):

```
Host ident authuser date request status bytes
```

The modules directory contains shared object module files. The Apache Web Server package includes Dynamic Shared Object (DSO) support. DSOs are loaded at runtime and are not compiled into the Web server executable, thereby saving memory. All of the standard modules are implemented as DSOs in Red Hat.

The Apache Web Server serves pages from the /home/httpd/html directory. This is specified in the /etc/httpd/conf/httpd.conf file. The cgi-bin directory is located at /home/httpd/cgi-bin. The cgi-bin is important in maintaining a secure Web site. The system administrator or webmaster can exercise greater control over this directory to ensure scripts do not have an adverse effect on the rest of the Web directories.

| Table 16.1 Apache Web Server Configuration Files |
| File | Content |
| httpd.conf | Contains directives controlling operation of Web server daemon (httpd) |
| srm.conf | Contains directives controlling specification of documents Web server can provide |
| access.conf | Contains directives controlling access to documents |