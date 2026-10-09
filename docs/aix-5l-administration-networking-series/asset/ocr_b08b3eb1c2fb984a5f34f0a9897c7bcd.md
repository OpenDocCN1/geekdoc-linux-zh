# **IBM HTTP Web Server Version 1.3.12.2**

```
```bash
DEFAULT_BROWSER = netscape
DOCUMENTATION_SERVER_MACHINE_NAME = yogi
DOCUMENTATION_SERVER_PORT = 80
CGI_DIRECTORY = /usr/HTTPServer/cgi-bin
DOCUMENT_DIRECTORY = /usr/HTTPServer/htdocs
```
```

As a final step, the **/etc/initab** file needs to have an entry to start the Web server on system restart. To check the **/etc/initab** file to ensure an entry for the Web server, enter either of the following commands:

```
```bash
# lsitab ih:ishtpd
```
```

or

```
```bash
# grep ihshtpd /etc/inittab
```
```

If a Web server entry is not found, then insert the following line to restart the server from the boot:

```
```bash
# mkitab ihshtpd:2:wait:/usr/HTTPServer/bin/httpd >/dev/console 2>&l # HTTP Server
```
```

If you have migrated from 4.3.3 to 5.1.0, you will need to follow this procedure to get DocSearch working because of the **oslevel**-specific nature of the product.

The installation is complete.

# **USING DOCSEARCH**

DocSearch must be executed from a graphical environment such as X Window System or CDE. Accessing the Documentation Library Service is as easy as pointing the Web browser to the documentation directory on the server.

On the documentation server, you can enter **docsearch** in an X environment and the browser will open with the collapsible tree listing each of the books registered with the Documentation Library Service. For both local and remote users with a Web browser, the URL for the documentation server should look like the following entry:

```
```bash
http://<Server-Hostname>/cgi-bin/ds_form
```
```

where `<Server-Hostname>` is the hostname, or IP address, of the documentation Web server.

If you do not have a local Web browser or if you have a telnet session to the remote documentation server, you will need to allow the remote system access to your X environment and export the display back to your local machine:

```
```bash
# xhost <remote_machine>
```
```

or