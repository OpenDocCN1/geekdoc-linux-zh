# ## Why is it called Apache?

According to the information about the Apache Web server project on `www.apache.org/foundation/faq.html`, the Apache group was formed in March 1995 by a number of people who provided patch files that had been written to fix bugs in NCSA HTTPD 1.3. The result after applying the patches to NCSA HTTPD was what they called a *patchy* server (that’s how the name Apache came about). The Apache Group has now evolved into The Apache Software Foundation (ASF), a nonprofit corporation that was incorporated in Delaware, U.S.A., in June 1999. ASF has a number of other ongoing projects. You can read about these projects at `www.apache.org`. In particular, visit `httpd.apache.org` for more information about the Apache Web server project.

According to the April 2004 Netcraft Web Server Survey at `news.netcraft.com/archives/web_server_survey.html`, the Apache Web server is the most popular — 66.99 percent of the 49,750,568 sites reported using the Apache server. Microsoft Internet Information Server (IIS) is a distant second, with 21.49 percent of the sites.

Among the available Web servers, the Apache Web server is the most popular, and it comes with Fedora Core. The Apache Web server started out as an improved version of the NCSA HTTPD server but soon grew into a separate development effort. Like NCSA HTTPD, the Apache server is developed and maintained by a team of collaborators. Apache is freely available over the Internet.

# ### Installing the Apache Web server

Depending on the Fedora Core installation options, the Apache Web server may be already installed in your system. To find out whether it’s installed, type the following command:

```
```bash
rpm -q httpd
```
```

If the Web server is installed, you see an output like this:

```
```bash
httpd-2.0.48-16.1
```
```

If you get a message that `httpd` is not installed, you can install it easily from this book’s companion DVD-ROMs using these steps:

+   1.  **Log in as root and insert the DVD-ROM into the DVD drive.**
+       - If you’re in the GNOME or KDE graphical desktop, the DVD is automatically mounted. If not, type the command `mount /dev/cdrom` to mount the DVD-ROM.