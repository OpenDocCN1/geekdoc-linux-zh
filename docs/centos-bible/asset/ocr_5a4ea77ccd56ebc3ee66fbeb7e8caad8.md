# **Part IV**

Networking

Zope Corporation (www.zope.org). Zope is now available as an Open Source project covered under the GPL. Zope is not included with the current version of CentOS. You can get Zope from the Zope development site (http://zope.sourceforge.net). Zope is Python-based.

■ **CERN (W3C) Jigsaw 2.2.6** — The latest HTTP/1.1 reference server, written completely in Java and freely available, can be found at www.w3.org/Jigsaw. It features extensive caching, an improved mechanism for executing external programs (although CGI is also supported), and a graphical administration tool.

# # Quick-Starting the Apache Web Server

If Apache wasn’t installed during the CentOS installation, you can install it later from the DVD or CD that comes with this book. You will need the `httpd` package and optionally the `httpd-manual` package (named `apache` and `apache-manual` in earlier versions).

Here’s a quick way to get your Apache Web Server going. From here, you’ll want to customize it to match your needs and your environment (as described in the section that follows):

+   1.  Make sure that Apache is installed by typing the following from a Terminal window:
+       ```bash
+       $ rpm -qa | grep httpd
+       system-config-httpd-1.3.3-31.el5
+       httpd-2.2.3-22.el5.centos
+       httpd-devel-2.2.3-31.el5.centos.2
+       httpd-manual-2.2.3-31.el5.centos.2
+       ```
+       The version number you see may be different. You need only the `httpd` package to get started. I recommend `httpd-manual` because it has excellent information on the whole Apache setup. The `httpd-devel` package includes the `apxs` tool for building and installing extension modules.
+       The `system-config-httpd` package contains a GUI-based Apache Configuration tool. Depending on the type of content you are serving, you might also add packages containing modules to run that code within the Apache server (such as `mod_perl`, `mod_python`, and `mod_mono`).

+   2.  A valid hostname is recommended if it is a public Apache server. If you don’t have a real, fully qualified domain name, you can edit the `/etc/httpd/conf/httpd.conf` file and define the `ServerName` as your computer’s IP address. Open the `httpd.conf` file (as the `root` user) in any text editor, search for the line containing `ServerName www.example1.com:80`, and uncomment it. It should appear as follows:
+       ```text
+       ServerName www.example.com:80
+       ```
+       To make the Web Server available to your LAN, you can use your IP address instead of `www.example.com` (e.g., `ServerName 10.0.0.1`). The `:80` represents the port number (`which` is the default). For a public Web Server, get a real DNS hostname. (Refer to Chapter 24 for information on DNS and making a server public.) No changes are required to this file to make Apache available on the local host.