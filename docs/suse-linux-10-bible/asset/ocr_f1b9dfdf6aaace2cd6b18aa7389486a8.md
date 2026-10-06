# Chapter 16 ✦ Setting Up a Web Site with the Apache Server 447

This chapter covers Apache as a web server in a SUSE environment.
Specifically, it explores how to configure and run the Apache web server for hosting one or more web sites on SUSE powered. This chapter also covers some of the basic issues concerning security and access control that you might need to consider.

Of course, most web sites provide dynamic access to information that is not contained within a plain HTML web page. In many cases the information that may seem to the end users to come from one resource has been put together by some web-based application from information that can reside in a database, the web server'sにつき, and a text file. In some cases pages, such as a form for processing a customer's shipping information, is using Perl or shell scripts through the Common Gateway Interface (CGI). In others, a computer language embedded within the web server application, such as PHP, takes advantage of system resources already dedicated to the running of the web server. As such, taking a look at how to get a Apache web server up and running, this chapter reviews how to take advantage of CGIs and embedded languages such as PHP with the Apache web server and SUSE.

# Configuring Apache

After you install the Apache web server from the SUSE distribution disks, it's time to set up a working environment for Apache. As Apache is configurable on the command line by editing files or in the YaST GUI tool. however, the YaST tool requires a bit of knowledge about web server in general and common Apache configuration options in particular. The easiest way to pick up this knowledge is to look at the Apache configuration through your text editor.

The main Apache server configuration, located at /etc/apache2/httpd.conf, is a plain text file directives for controlling the behavior of the overall web server, sites, or files. The main configuration file can also incorporate Apache-related directives in other files using the Include directive and changes to the main configuration files are recognized only when the server is started or restarted.

> Apache 2 has been included in versions of SUSE since 9.1, including SLES 9. This chapter contains configuration that will help you get Apache 2 up running.

To configure Apache, to start the service, and so on you must be logged in as root.

To manage the multilayered options the web server provides, the configuration file is broken down into three main sections:

+   Global Environment Section — This section contains directives that affect the overall operation of the Apache web server.