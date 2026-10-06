
## Chapter 16 ✦ Setting Up a Web Site with the Apache Server 447

This chapter covers Apache as a web server in a SUSE environment. Specifically, it explores how to configure and run the Apache web server for hosting one or more web sites on SUSE powered. This chapter also covers some of the basic issues concerning security and access control that you might need to consider.

Of course, most web sites provide dynamic access to information that is not contained within a plain HTML web page. In many cases the information that may seem to the end users to come from one resource has been put together by some web-based application from information that can reside in a database, the web server's scripts, and a text file. In some cases pages, such as a form for processing a customer's shipping information, is using Perl or shell scripts through the Common Gateway Interface (CGI). In others, a computer language embedded within the web server application, such as PHP, takes advantage of system resources already dedicated to the running of the web server. As such, taking a look at how to get a Apache web server up and running, this chapter reviews how to take advantage of CGIs and embedded languages such as PHP with the Apache web server and SUSE.

## Configuring Apache

After you install the Apache web server from the SUSE distribution disks, it's time to set up a working environment for Apache. As Apache is configurable on the command line by editing files or in the YaST GUI tool. however, the YaST tool requires a bit of knowledge about web server in general and common Apache configuration options in particular. The easiest way to pick up this knowledge is to look at the Apache configuration through your text editor.

The main Apache server configuration, located at /etc/apache2/httpd.conf, is a plain text file directives for controlling the behavior of the overall web server, sites, or files. The main configuration file can also incorporate Apache-related directives in other files using the Include directive and changes to the main configuration files are recognized only when the server is started or restarted.

> Apache 2 has been included in versions of SUSE since 9.1, including SLES 9. This chapter contains configuration that will help you get Apache 2 up running.

To configure Apache, to start the service, and so on you must be logged in as root.

To manage the multilayered options the web server provides, the configuration file is broken down into three main sections:

- Global Environment Section — This section contains directives that affect the overall operation of the Apache web server.

- Main Server Section — This section provides configuration options dedicated to the operation of the primary web site.

- Virtual Host Section — Here you can apply the same configuration options available in the main server section to any virtual host.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_492_0.png)

> Virtual hosts are discussed in the chapter.

The syntax itself for the configuration file is pretty straightforward; each line within the file contains one directive and if needed the backslash (\) may be used as the last character on a line to indicate the directive continues onto the next line.

Directives themselves are case insensitive, as many programming languages, the hash character (#) is considered the token to denote the beginning of comments; comments may not be included on a line after a configuration directive. Blank lines and white space occurring before a directive are ignored directives to be spaced for additional clarity. The syntax of a configuration can be checked before invoking the web server process using the apache2ctl tool provided by the ASF.

For example following command-line argument tests the configuration file at /etc/apache/httpd.conf. Note that if the configuration is valid, apache2ctl returns Syntax OK.

```
apache2ctl configtest
Syntax OK
```

However, if an error has been made — for example, the DocumentRoot directive, which points to where of all the main directives the web server serves for client requests are kept, is not defined — then the configuration test returns the proper error message.

```
apache2ctl configtest
Syntax error on 449 of /etc/apache2/httpd.conf:
DocumentRoot takes one argument, Root directory of the document tree
```

Should apache2ctl not be available on the system, the httpd binary itself can also be used to verify the syntax of a configuration file:

```
/usr/sbin/httpd2 -t
Syntax OK
```

## Global Directives

As mentioned, the directives within this section affect the overall operation of the Apache web server; the most important of these options include controls for the number of concurrent requests the server will handle and how to treat those requests after they have been accepted, all of which directly relate to the performance of the web server at large, including a number of options for controlling the management of Apache processes during runtime.

The traditional processing model for Apache on Linux is known as Prefork. Within this method, upon startup the Apache parent process, running as root, creates a number of child processes, the number of which and user type is defined in the configuration file using the user directive. The child processes handle requests on a one-to-one basis for resources managed by the web server. If a spike of requests is beyond the allotment of the currently running child process, the parent process will fork off more processes to catch up. The root parent process, however, is limited to a predefined maximum number of child processes, creating additional processes is a resource-expensive exercise. Since forking a process is a time-and resource-consuming exercise, the goal behind the Prefork model is to have the child processes ready before they are needed.

There are a number of directives for controlling the Prefork processing module, including:

- StartServers — The number of server processes the parent process is to start with
- MinSpareServers — The minimum number of server processes to keep available
- MaxSpareServers — The maximum number of server processes to be kept available
- MaxClients — The maximum number of server processes allowed running at any given time
- MaxRequestsPerChild — The maximum number of requests a server process handles

The following shows a typical Apache server configuration:

```
StartServers 5
MinSpareServers 5
MaxSpareServers 10
MaxClients 150
MaxRequestsPerChild 0
```

In this example configuration the Apache root process forks off five child processes to handle any initial request server may encounter. The parent process then monitors the pool of processes, and as it handles a network request for a given resource, adds or subtracts processes to the waiting pool, keeping a minimum of five child processes and no more than ten processes. The parent process will create no more than 150 processes, should the web site see a peak in traffic. This limit is used to keep the incoming requests from overwhelming the resources on which the server is running.

- Webspace — The view of the resources as seen by the client. For example the path /dir/ in the webspace might correspond to the path /srv/htdocs/dir/ in the filesystem. Of course, the webspace need not map directly to the filesystem, since web pages may be generated dynamically.

## Chapter 16 ✦ Setting Up a Web Site with the Apache Web Server 451

The <Directory> and <Files> containers, however, are batches of directives that apply to resources as seen from the filesystem. Directives enclosed in a <Directory> container apply to the named filesystem directory and all subdirectories. For example, in the following configuration, directory indexes will be enabled for /srv/www/htdocs/dir.

```
<Directory>/srv/www/htdocs/dir
Options +Indexes
</Directory>
```

Directives enclosed in the <Files> container apply to any file with the specified name, regardless of what directory it resides in. For example, the configuration denies access to any file named private.html regardless of where it is found.

```
<Files private.html>
Order allow,deny
Deny from all
</Files>
```

If, a directive needs to focus on a file in a particular part of the filesystem, the <Files> and <Directory> containers can be nested, allowing for granular control of resources within the configuration file.

```
<Directory>/srv/www/htdocs/dir
<Files private.html>
Order allow,deny
Deny from all
</Files>
</Directory>
```

In the preceding example, the configuration will deny access to /srv/www/htdocs/dir/private.html and any files named private.html within any subdirectories within /srv/www/htdocs/dir.

In the area of webpage, the <Location> directive operates on the configuration of resources found from this point of view. The following configuration example prevents access to any URL-path that begins with /private, such as <http://www.suse.com/private>

```
<Location>/private>
Order Allow,Deny
Deny from all
</Location>
```

Unlike the <Directory> or <Files> containers, the <Location> directive need not have anything to do with a resource located on the filesystem. This is useful for dynamically generated content that has no physical location on the filesystem.
