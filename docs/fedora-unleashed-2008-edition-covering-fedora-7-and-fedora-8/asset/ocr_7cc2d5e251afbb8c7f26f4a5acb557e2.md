```
Server's Module Magic Number: 20051115:4
Architecture: 32-bit
Server MPM: Prefork
threaded: no
forked: yes (variable process count)
Server compiled with... 
```

The output displays the version number, build date and time, platform, and various options used during the build. You can use the -v option to see terser version information.

# # Installing the Apache Server

You can install Apache through Pirut, from your own RPMs, or build it yourself from source code. The Apache source builds on just about any Unix-like operating system and on Win32. If you elect to install the Web Server group of files when first installing Fedora, Apache and related software and documentation in 17 packages are installed automatically.

If you're about to install a new version of Apache, you should shut down the old server. Even if it's unlikely that the old server will interfere with the installation procedure, shutting it down ensures that there will be no problems. If you don't know how to stop Apache, see the “Starting and Stopping Apache” section later in this chapter.

# ## Installing Through Pirut

Although the “Web Server” category was available during install, it's often best to install Fedora clean of any services so that you minimize your attack vectors out of the box. As soon as Fedora is installed, you can use Pirut to add Apache by choosing Web Server from the Servers category.

However, you might find it useful to use the List tab rather than the Browse tab, because all the Apache modules start with “mod” to help you find them easily. Fedora ships with many Apache modules, some of which are discussed in the following sections. However, only a handful are enabled by default—you need to use Pirut to install and activate them.

# ## Installing from the RPM

You can find the Apache RPM on the Fedora installation media, on the Fedora FTP server, or at one of its many mirror sites. Check the Fedora site as often as possible to download updates as they become available. Updated RPM files usually contain important bug and security fixes. When an updated version is released, install it as quickly as possible to keep your system secure.

> > NOTE
> > Check the Apache site for security reports. Browse to http://httpd.apache.org/security_report.html for links to security vulnerabilities for Apache 1.3, 2.0, and 2.2. Subscribe to a support list or browse through up-to-date archives of all Apache mailing lists at http://httpd.apache.org/mail/ (for various articles) or http://httpd.apache.org/lists.html (for comprehensive and organized archives).