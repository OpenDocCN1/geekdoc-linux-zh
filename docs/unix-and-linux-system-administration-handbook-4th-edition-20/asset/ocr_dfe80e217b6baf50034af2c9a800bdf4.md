The second section configures the "default" server, the server that handles any requests that aren't answered by VirtualHost definitions (see page 971). Configuration parameters in this section include the user and group of whom the server will run (something other than root!) and the all-important DocumentRoot state, which defines the root of the directory tree from which documents are served. This also addresses issues such as the handling of "special" URLs like that include the -user syntax to access a user's home directory.

You manage security concerns in the second section of the configuration file as well. Directives control access on a per-file basis (the <File> directive) or per-directory basis (the <Directory> directive). These permissions prevent access to sensitive files through httpd. You should specify who has access to two controls: one that covers the entire filesystem and one that applies to the main document folder. The defaults with Apache are sufficient, although we recommend that you remove the AllowSymLinks option to prevent httpd from following symbolic links in your directory tree. (We wouldn't want someone to accidentally create a symbolic link to /etc, now would we?) For Apache security tips,

```
httpd.apache.org/docs-2.2/misc/security_tips.html
```

The third and final section of the config sets up virtual hosts. We discuss this topic in more detail on page 971.

Once you have made your configuration changes, check the syntax of the configuration file by running httpd -t. If Apache reports "Syntax OK," then you're good to go. If not, check the httpd.conf file for typos.

# Running Apache

You can start httpd by hand or from your startup scripts. The latter is preferable, since this configuration ensures that the server restarts whenever the machine reboots. To start the server by hand, type something like:

```
$ apachectl start
```

See Chapter 3 for more information about startup scripts.

# Analyzing log files

With your site in production, you're likely to want to gather statistics about the use of the site, as the number of requests per page, the average requests per day, the percentage of failed requests, and the amount of data transferred. Make sure you're using the "combined" log format (your CustomLog directives should have the word combined at the end instead of common). The combined log format includes each request's referrer (the page from which the URL was linked) and user agent (the client's browser and operating system).

Your access and error logs appear in Apache's logs directory. The files are human readable, but they contain so much information that you really need a separate