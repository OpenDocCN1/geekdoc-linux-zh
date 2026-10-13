Web-accessible Linuxconf interface. This is why you must restrict Web-based Linuxconf access only to your trusted network.

The Web-based Linuxconf is an inetd-run service. When you install the Linuxconf RPM package, a line such as the following gets added to your /etc/inetd.conf file:

```
linuxconf stream tcp wait root /bin/linuxconf \
linuxconf --http
```

Another line such as the next one gets added to your /etc/services file:

```
linuxconf 98/tcp
```

This allows inetd to run Linuxconf in HTTP mode when a request for connection is made on TCP/IP port 98. In other words, when you use a browser on your Linux system to access http://localhost:98/, the inetd daemon starts /bin/linuxconf using the --http option.

> **Caution**
> Linuxconf runs as a setuid root process. Therefore, if a security hole is discovered in Linuxconf, it is likely to allow root privileges to anyone. Linuxconf is over 80,000 lines of C++ code. Frankly, I don't feel too comfortable running a large setuid program via the Web. You have to make your own decision about using it over the Web.

As previously mentioned, by default, Linuxconf allows Web-based access only from the localhost. If you want to enable remote administrative access to Linuxconf via the Web, follow these steps:

+   1. Run linuxconf from your console or X Windows.
+   2. Select the Config menu option and expand its branches either by pressing Enter for text mode or by double-clicking it for GUI mode. Expand the Misc menu and select Linuxconf network access; you should see a tab on the right similar to the one shown in Figure 4-8.
+   3. Select the Enable network access check box.
+   4. Select the Log access in /var/log/htmlaccess.log check box to allow logging of Linuxconf access requests via the network.