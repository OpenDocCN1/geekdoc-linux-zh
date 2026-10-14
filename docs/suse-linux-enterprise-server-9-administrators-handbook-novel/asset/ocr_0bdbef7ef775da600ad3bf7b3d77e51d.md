# Web Services

The Apache2 web server is an available configuration option for your SLES server. The Apache2 server is a fully functional and very versatile environment. In a default configuration, Apache2 offers web pages using the HTTP protocol on port 80. If required, a certificate can be incorporated to offer secure web pages using HTTPS on port 443. The following options are available under Apache2:

+   - Access controls
+   - Server-side includes
+   - CGI scripting
+   - Per-user websites
+   - Virtual servers (by name or by IP address)

You access the Apache2 configuration menus by selecting the Network Service, HTTP Server options in YaST. In a typical environment, a web server offers content housed in a single structure of directories.

By default, Apache2 on SLES points to /srv/www/htdocs as the repository for all centralized web information (see Figure 8.10). Web page requests are pointed to this directory for resolution. Subdirectories can be added within this directory to further segregate content. The directory names then become an integral portion of the requesting URLs. The structure of the website beyond that point is left to the webmaster responsible for the site.

For more dynamic content, you can find a system-wide CGI environment in /srv/www/cgi-bin. The web server configuration file defines how documents placed in directories are processed. This specific location is configured to pre-process the requested item through the appropriate scripting engine. Output from the script is then passed back to the requesting client as standard HTML. This allows the website in question to generate dynamic content not normally accessible through raw HTML.

SLES and Apache2 also allow users to publish their own web content. When users are added to a system, they are automatically given a public_html directory in their home directory. Web pages in these directories can be accessed by adding ~username to the default web server path.

An out-of-the-box installation of the HTTP server environment provides a great deal of what a typical website would require. Apache2, however, can provide significantly more functionality. The installed version of Apache2 supports *virtual servers*, which come in two flavors: IP based and name based.