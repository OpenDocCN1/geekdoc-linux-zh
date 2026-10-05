
## Configuring Apache

For a complete list of standard modules, see http://apache.org/docs-2.2/mod.

Although the default set of modules is reasonable, you may also want to enable the modules shown in Table 23.5.

### Table 23.5 Useful Apache modules that are not enabled by default

| Module | Function |
| -- | -- |
| authn_dbm | Uses a Dbm database to manage user/group access (recommended if you need per-user, password-based access to all of your web site) |
| rewrite | Rewrites URLs with regular expressions |
| expires | Lets you attach expiration dates to documents |
| proxy | Uses Apache as a proxy server |
| mod_ssl | Enables support for the Secure Sockets Layer* for HTTPS |

* Also known as Transport Layer Security or TLS; see page 971.

Likewise, you may want to disable the modules listed in Table 23.6. For security and performance, it's a good idea to disable modules that you know will not be using.

### Table 23.6 Apache modules we suggest removing

| Module | Function |
| -- | -- |
| asis | Allows designated file types to be sent without HTTP headers |
| autoindex | Displays the contents of directories that don't have a default HTML file |
| env | Lets you set special environment variables for CGI scripts |
| userdir | Allows users to have their own HTML directories |

When configure has finished executing, run make and then make install to actually compile and install the appropriate files.

Compiling Apache on AIX is unfortunately not so straightforward. See the tips and tricks at people.apache.org/~twick/apache-2-on-aix.

Once you've installed the server, configure it for your environment. The config files are kept in the conf directory of the installation directory. Examine and customize the httpd.conf file, which is divided into three sections.

The first section deals with global settings such as the server pool, the TCP port on which the HTTP server listens for queries (usually port 80, although you can choose another—and yes, you can run multiple HTTP servers on different ports on a single machine), and the settings for dynamic module loading.

![](img/579efec8c67772f31ecf34844bbb71a2_1013_0.png)

The second section configures the "default" server, the server that handles any requests that aren't answered by VirtualHost definitions (see page 971). Configuration parameters in this section include the user and group of whom the server will run (something other than root!) and the all-important DocumentRoot state, which defines the root of the directory tree from which documents are served. This also addresses issues such as the handling of "special" URLs like that include the -user syntax to access a user's home directory.

You manage security concerns in the second section of the configuration file as well. Directives control access on a per-file basis (the <File> directive) or per-directory basis (the <Directory> directive). These permissions prevent access to sensitive files through httpd. You should specify who has access to two controls: one that covers the entire filesystem and one that applies to the main document folder. The defaults with Apache are sufficient, although we recommend that you remove the AllowSymLinks option to prevent httpd from following symbolic links in your directory tree. (We wouldn't want someone to accidentally create a symbolic link to /etc, now would we?) For Apache security tips,

```
httpd.apache.org/docs-2.2/misc/security_tips.html
```

The third and final section of the config sets up virtual hosts. We discuss this topic in more detail on page 971.

Once you have made your configuration changes, check the syntax of the configuration file by running httpd -t. If Apache reports "Syntax OK," then you're good to go. If not, check the httpd.conf file for typos.

## Running Apache

You can start httpd by hand or from your startup scripts. The latter is preferable, since this configuration ensures that the server restarts whenever the machine reboots. To start the server by hand, type something like:

```
$ apachectl start
```

See Chapter 3 for more information about startup scripts.

## Analyzing log files

With your site in production, you're likely to want to gather statistics about the use of the site, as the number of requests per page, the average requests per day, the percentage of failed requests, and the amount of data transferred. Make sure you're using the "combined" log format (your CustomLog directives should have the word combined instead of common). The combined log format includes each request's referrer (the page from which the URL was linked) and user agent (the client's browser and operating system).

Your access and error logs appear in Apache's directory. The files are human readable, but they contain so much information that you really need a separate program to extract useful data from them. There are literally hundreds of different analyzers, both free and commercial. Two analyzers worth taking a look at are Analog (analog) and AWStats (sourceforge.net). These provide fairly basic information. If you're looking for information about traffic and usage patterns for a web site, check out Google Analytics at analytics.google.com. This service requires a small stub on each page you want to track, but then provides all data gathering and analysis for free.

## Optimizing for high-performance hosting

The hosting community has learned over the last few years that one of the easiest ways to create high-performance hosting platform is to optimize some servers for static content. One way to address this need is through the use of in-kernel cache. Because these systems do not copy data to or from user space before returning to it, they achieve some performance gains. However, because the solutions operate in kernel space, they entail additional security risk. We recommend using them with extreme caution.

A kernel-based web server TUX runs in conjunction with a traditional web server as Apache is available for some Linux distributions. Although TUX was developed by Red Hat (Red Hat now calls it Content Accelerator), it is released under the GPL and can be used. Unfortunately, configuring TUX can be some challenge. The system was popular in the early 2000s, but its popularity has dwindled. For details, see redhat.com/docs/manual.

On the Solaris platform, Sun has released the Solaris Network Cache (NCA) to provide in-kernel content caching. NCA intercepts the traffic going to and caches static pages. When subsequent requests arrive for the same content, they're served from cache without http.

## 23.3 VIRTUAL INTERFACES

In the early years, a UNIX machine typically acted as the server for a single web site (e.g., acme.com). As the web's popularity grew, everybody wanted to have a web site, and thousands of companies became hosting providers. Providers realized that they could achieve significant economies of scale if were able to host more than one site on a single server. This trick would allow acme.com, ajax.com, ad ranch.com, and many other sites to be transparently served by the same hardware. Of course, this arrangement also gives Google access to your traffic data, which may or not be a good thing.

![](img/579efec8c67772f31ecf34844bbb71a2_1015_0.png)

In response to this business need, virtual interfaces were born. The idea is simple: a single machine responds to the network with more IP addresses than it has physical network interfaces. Each of the resulting "virtual" network interfaces can be associated with a corresponding domain name that users on the Internet might want to connect to. Thus, a single machine can serve hundreds of web sites.

Virtual interfaces allow a daemon to identify connections not only on the destination port number (e.g., port 80 for HTTP) but also on the connection's IP address. Today, virtual interfaces are in widespread use and have proved to be useful for applications other than web hosting.

## Using name-based virtual hosts

The HTTP 1.1 protocol also defines a form of virtual-interface-like functionality (officially called "name-based virtual hosts") that eliminates the need to assign unique IP addresses to web servers or to configure a special interface at the OS level. This approach conserves IP addresses and is useful for some sites, especially (such as universities) at which a single server is home to hundreds or thousands of pages.

Unfortunately, the scheme isn't very practical for commercial sites. It reduces ability (you must change the IP address of the site to move it to a different server) and may also have a negative impact on security (if you access a site at your firewall according to IP addresses). Additionally, name-based virtual hosts require browser support to use SSL. Given these limitations of name-based virtual hosts, it appears that virtual interfaces will be around for a while.

## Configuring virtual interfaces

Setting up a virtual interface involves two steps. First, you must create the virtual interface at the TCP/IP level. The exact way to do this depends on your version of UNIX; the next few sections provide instructions for each of our example systems. Second, you must tell the Apache server about the virtual interfaces you have installed. We cover this step starting on page 971.

## Linux virtual interfaces

Virtual interfaces are named with the notation interface:instance. For example, if your Ethernet interface is eth0, then the virtual interfaces associated with it could be eth0:0, eth0:1, and so on. All interfaces are configured with the `ifconfig` command.

```
$ sudo ifconfig eth0:0 128.138.243.150 netmask 255.255.255.192
configs eth0:0 and assigns an address on the 128.138.243.128/26 network.
```

*   3. A relatively new featured Server Name Indication (SNI) enables the use of the SSL with virtual hosts, but older browsers do not support it.

![](img/579efec8c67772f31ecf34844bbb71a2_1016_0.png)
