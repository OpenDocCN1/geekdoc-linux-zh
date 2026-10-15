
For a complete list of standard modules, see httpd.apache.org/docs-2.2/mod.

Although the default set of modules is reasonable, you may also want to enable the modules shown in Table 23.5.

**Table 23.5 Useful Apache modules that are not enabled by default**

| Module | Function |
|---|---|
| authn_dbm | Uses a DBM database to manage user/group access (recommended if you need per-user, password-based access to areas of your web site) |
| rewrite | Rewrites URLs with regular expressions |
| expires | Lets you attach expiration dates to documents |
| proxy | Uses Apache as a proxy server |
| mod_ssl | Enables support for the Secure Sockets Layer* for HTTPS |

* Also known as Transport Layer Security or TLS; see page 971.

Likewise, you may want to disable the modules listed in Table 23.6. For security and performance, it's a good idea to disable modules that you know you will not be using.

**Table 23.6 Apache modules we suggest removing**

| Module | Function |
|---|---|
| asis | Allows designated file types to be sent without HTTP headers |
| autoindex | Displays the contents of directories that don't have a default HTML file |
| env | Lets you set special environment variables for CGI scripts |
| userdir | Allows users to have their own HTML directories |

When configure has finished executing, run make and then make install to actually compile and install the appropriate files.

![](img/14d78e3cecac4581d37024baf1e94cca_1013_0.png)

Compiling Apache on AIX is unfortunately not so straightforward. See the tips and tricks at people.apache.org/~trawick/apache-2-on-aix.html.

## Configuring Apache

Once you've installed the server, configure it for your environment. The config files are kept in the conf subdirectory of the installation directory. Examine and customize the httpd.conf file, which is divided into three sections.

The first section deals with global settings such as the server pool, the TCP port on which the HTTP server listens for queries (usually port 80, although you can choose another—and yes, you can run multiple HTTP servers on different ports on a single machine), and the settings for dynamic module loading.

The second section configures the "default" server, the server that handles any requests that aren't answered by VirtualHost definitions (see page 971). Configuration parameters in this section include the user and group as which the server will run (something other than root!) and the all-important DocumentRoot statement, which defines the root of the directory tree from which documents are served. This section also addresses issues such as the handling of "special" URLs like those that include the ~user syntax to access a user's home directory.

You manage global security concerns in the second section of the configuration file as well. Directives control access on a per-file basis (the <Files> directive) or on a per-directory basis (the <Directory> directive). These permission settings prevent access to sensitive files through httpd. You should specify at least two access controls: one that covers the entire filesystem and one that applies to the main document folder. The defaults that come with Apache are sufficient, although we recommend that you remove the FollowSymLinks option to prevent httpd from following symbolic links in your document tree. (We wouldn't want someone to accidentally create a symbolic link to /etc, now would we?) For more Apache security tips, see httpd.apache.org/docs-2.2/misc/security_tips.html.

The third and final section of the config file sets up virtual hosts. We discuss this topic in more detail on page 971.

Once you have made your configuration changes, check the syntax of the configuration file by running httpd -t. If Apache reports "Syntax OK," then you're good to go. If not, check the httpd.conf file for typos.

## Running Apache

You can start httpd by hand or from your system's startup scripts. The latter is preferable, since this configuration ensures that the web server restarts whenever the machine reboots. To start the server by hand, type something like:

```
$ apachectl start
```

See Chapter 3 for more information about startup scripts.

## Analyzing log files

With your web site in production, you're likely to want to gather statistics about the use of the site, such as the number of requests per page, the average number of requests per day, the percentage of failed requests, and the amount of data transferred. Make sure you're using the "combined" log format (your CustomLog directives should have the word combined at the end instead of common). The combined log format includes each request's referrer (the page from which the URL was linked) and user agent (the client's browser and operating system).

Your access and error logs appear in Apache's logs directory. The files are human readable, but they contain so much information that you really need a separate
