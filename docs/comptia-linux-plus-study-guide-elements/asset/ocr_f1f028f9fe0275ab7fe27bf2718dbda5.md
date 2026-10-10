The first couple of lines in this configuration simply load the PHP module and handler. The **DirectoryIndex** and **AddType** lines help Apache manage the PHP files. The **DirectoryIndex** line will replace existing lines in your configuration—or more precisely, you should ensure that *index.php* appears on the **DirectoryIndex** line along with any other filenames you use for index files.

In addition to these global options, directories that hold PHP scripts may include files called *php.ini*, which set various PHP interpreter options. There are quite a few options, such as **user_dir**, **include_path**, and **extension**. If you need to tweak your PHP settings, I recommend starting from a sample file, such as the global *php.ini* file in */etc*.

The final Web server scripting solution is Tomcat (http://tomcat.apache.org), which enables Apache to run Java servlets on the server computer. Tomcat is conceptually similar to PHP. As with PHP, you must begin by installing appropriate Tomcat packages on your system. The main Tomcat package is likely to be called *tomcat5*, *tomcat6*, or something similar. (Version 6 is the latest version of Tomcat as I write, but version 5 is still available in many distributions.) High-level package tools, such as Yum or APT, will help you locate the appropriate packages.

With Tomcat installed, you must tell Apache how to use it. Typically, Tomcat packages install their own configuration files with options to enable support in Apache. To use them, you need add only one line to your Apache configuration file, such as this one:

```
include /tomcat/conf/mod_jk.conf-auto
```

The precise file you reference may vary from one distribution to another, so you should check your own Tomcat package to see what configuration files it’s installed.

Whatever scripting tool you use, you can restart Apache via its SysV startup script to have it enable scripting support. It’s then up to you or your Web developers to create appropriate scripts to manage dynamic content on your site. This is a very complex topic that’s not covered on the Linux+ exam.

# Configuring Virtual Hosting

Another Web server feature that’s handy on large systems is *virtual hosting*—one server that hosts multiple Web sites. Suppose two organizations with two domains (say, *example.com* and *pangea.edu*) both want to host Web sites, but to reduce costs, they decide to share a single computer to do the job. Both point hostnames in their domains to this computer’s IP address. Virtual hosting enables the computer with this IP address to respond differently depending on the hostname the user enters in a remote Web browser. Web hosting ISPs make heavy use of this feature, supporting many domains on a single computer. It can also be handy if you’ve changed your company name—you can run a single server that responds to both old and new domain names, with a notice about the change on the old name.

Implementing virtual hosting can be done in a couple of ways. One is to create a block with the **VirtualHost** directive:

```
<VirtualHost *>  
    ServerName www.example.com
```