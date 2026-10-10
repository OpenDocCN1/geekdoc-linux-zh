+   %t The time, in common log time format.  
+   %{format}t The time, in the form given by format, which should be in strftime(3) format.  
+   %T The seconds taken to serve the request.  
+   %u Remote user from auth; this might be bogus if the return status (%s) is 401.  
+   %U The URL path requested.  
+   %v The server name according to the UseCanonicalName directive.  
+   %V The canonical ServerName of the server serving the request.

You can put a conditional in front of each variable to determine whether the variable is displayed. If the variable isn’t displayed, ‘-’ is displayed instead. These conditionals are in the form of a list of numerical return values. For example, %{401}u displays the value of REMOTE_USER unless the return code is 401.

You can then specify the location and format of a log file by using the CustomLog directive:

```
CustomLog logs/access_log common
```

If it isn’t specified as an absolute path, the location of the log file is assumed to be relative to the ServerRoot.

# Related Fedora and Linux Commands

You will use these commands when managing your Apache web server in Fedora:

+   ▶  **apachectl**—Server control shell script included with Apache
+   
+   ▶  **system-config-httpd**—Red Hat’s graphical web server configuration tool
+   
+   ▶  **httpd**—The Apache web server
+   
+   ▶  **konqueror**—KDE’s graphical web browser
+   
+   ▶  **elinks**—A text-based, graphical menu web browser
+   
+   ▶  **firefox**—The premier open source web browser

# Reference

+   ▶  http://news.netcraft.com/archives/web_server_survey.html—A statistical graph of web server usage points out that Apache is, by far, the most widely used server for Internet sites.
+   
+   ▶  http://www.apache.org/—Extensive documentation and information about Apache are available at The Apache Project website.