covered under the GPL. Zope is not included with the current version of Fedora or RHEL. You can get Zope from the Zope development site (`zope.sourceforge.net`). Zope is python-based.

+   - **CERN (W3C) Jigsaw 2.2.6** — The latest HTTP/1.1 reference server, written completely in Java and freely available, can be found at `www.w3c.org/Jigsaw`. It features extensive caching, an improved mechanism for executing external programs (although CGI is also supported), and a graphical administration tool.

# ## Quick Starting the Apache Web Server

If Apache wasn’t installed during the Fedora installation, you can install it later from the DVD or CDs that come with this book. You will need the httpd package and optionally the httpd-manual package (named apache and apache-manual in earlier versions).

Here’s a quick way to get your Apache Web server going. From here, you’ll want to customize it to match your needs and your environment (as described in the section that follows).

+   1. Make sure that Apache is installed by typing the following from a Terminal window:

```
```
$ rpm -qa | grep httpd
system-config-httpd-1.4.4-1.fc8
httpd-tools-2.2.6-3
httpd-devel-2.2.6-3
httpd-2.2.6-3
httpd-manual-2.2.6-3
```
```

The version number you see may be different. You need only the httpd package to get started. I recommend httpd-manual because it has excellent information on the whole Apache setup. The httpd-devel package includes the `apxs` tool for building and installing extension modules. The httpd-tools package includes tools for running benchmarks and managing passwords for Apache.

The `system-config-httpd` package contains a GUI-based Apache Configuration tool. Depending on the type of content you are serving, you might also add packages containing modules to run that code within the Apache server (such as `mod_perl`, `mod_python`, and `mod_mono`).

+   2. A valid host name is recommended if it is a public Apache server (for example, `abc.handsonhistory.com`). If you don’t have a real, fully qualified domain name, you can edit the `/etc/httpd/conf/httpd.conf` file and define the `ServerName` as your computer’s IP address. Open the `httpd.conf` file (as the root user) in any text editor, search for the line containing `ServerName www.example.com:80`, and uncomment it. It should appear as follows:

```
```
ServerName www.example.com:80
```
```

To make the Web server available to your LAN, you can use your IP address instead of `www.example.com` (for example, `ServerName 10.0.0.1`). The `:80` represents the