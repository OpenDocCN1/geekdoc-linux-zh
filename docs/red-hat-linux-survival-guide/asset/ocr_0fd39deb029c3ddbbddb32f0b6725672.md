```
|   +--vhosts
| 
+---icons
|   |
|   +---small
| 
+---logs
+---cgi-bin
```

The following list gives a brief description of each of the directories in the Apache directory structure:

+   - `/include` — Contains all the C header (include) files that are needed only if you develop Web applications that integrate with Apache, or if you want to use third-party software with Apache that require the header files. On a production server you can remove this directory after installation.
+   - `/lib` — Houses the Apache Portable Run-Time (APR) library files. These files are required for running Apache, as well as other support utilities such as ab.
+   - `/bin` — Contains the programs shown in Table 12-3.
+   - `/conf` — Houses the configuration files for Apache, which are listed in Table 12-4.
+   - `/htdocs` — The default document root directory for the main Apache server. The httpd.conf file sets the DocumentRoot directive to this directory. By default the htdocs directory also has the entire Apache manual installed in a subdirectory.
+   - `/icons` — Used to store various Apache icons that are needed for displaying the directory listing.
+   - `/logs` — Used to store the Apache server logs, the CGI daemon socket (cgisock), and the PID file (httpd.pid).
+   - `/cgi-bin` — The default CGI script directory, which is set by using the ScriptAlias directive in httpd.conf. By default, Apache comes with two simple CGI scripts — printenv and test-cgi. Each of these scripts prints out CGI environment variables when requested via the http://server_name/cgi-bin/script_name URL.