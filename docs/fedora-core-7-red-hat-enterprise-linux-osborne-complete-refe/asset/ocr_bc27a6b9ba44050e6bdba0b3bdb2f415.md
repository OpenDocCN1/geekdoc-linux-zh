**serverport** is the port Tux will use—80 if it is the primary Web server. **clientport** is the port used by the user-space Web server coordinates with, like Apache. **documentroot** specifies the root directory for your Web documents (*var/www/html* on Red Hat and Fedora). Ideally, Tux is run as the primary Web server and Apache as the secondary Web server. To configure Apache to run with Tux, the port entry in the Apache **httpd.conf** file needs to be changed from 80 to 8080.

Port 8080

You can start, stop, and restart the server with the **service** command and the **/etc/rd.d/init.d/tux** script. Several parameters like **DOCROOT** can be specified as arguments to this Tux command. You can enter them in the **/etc/sysconfig/tux** file.

> **NOTE** You can also run Tux as an FTP server. In the **/proc/sys/net/tux** directory, you change the contents of the file **serverport** to 21, **application_protocol** to 1, and **nonagle** to 0, and then restart Tux. Use the **generatetuxlist** command in the document root directory to generate FTP directory listings.

# ## Alternate Web Servers

Other Web servers available for Linux include the Stronghold Enterprise Server and the Apache-SSL server. A listing is provided here.

+   - Apache-SSL ([www.apache-ssl.org](www.apache-ssl.org)) is an encrypting Web server based on Apache and OpenSSL ([www.openssl.org](www.openssl.org)).
- lighttpd ([www.lighttpd.net](www.lighttpd.net)) is a small, very fast, Web server, included with Fedora.
- Sun Java System Web server ([www.sun.com](www.sun.com)) features Java development support and security.
- Zope application server ([www.zope.org](www.zope.org)) is an open source Web server with integrated security, Web-based administration and development, and database interface features. It was developed by the Zope Corporation, which also developed the Python programming language.
- Stronghold Enterprise Server ([www.redhat.com/software/stronghold](www.redhat.com/software/stronghold)) is a commercial version of the Apache Web server featuring improved security and administration tools.
- Netscape Enterprise Server ([enterprise.netscape.com](enterprise.netscape.com)), part of Netscape security solutions, features open standards with high performance.
- You can also use the original NCSA Web server, though it is no longer under development and is not supported ([hoohoo.ncsa.uiuc.edu](hoohoo.ncsa.uiuc.edu)).