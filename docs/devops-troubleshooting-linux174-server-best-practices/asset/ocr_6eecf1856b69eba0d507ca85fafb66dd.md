# Solve Common Web Server Problems

Although it's difficult to document how to solve any and all web server problems, you are likely to run into a few general classes of problems that have identifiable symptoms. This section will highlight some of the common types of problems you may find, their symptoms, and how to remedy them.

# Configuration Problems

One common and relatively simple problem to identify in a web server is a configuration problem. Since web servers need to be reloaded to take on changes in their configuration, it can be tempting to make many changes without reloading the web server; however, if you do so, you are likely to find out during a server maintenance (or when you need to restart the server to load new SSL certificates) that there's some syntax error in your configuration files and your server will refuse to start.

Both Apache and Nginx validate their configuration files when you start, restart, or reload the service, so that's one way to find configuration errors—unfortunately, it also means that in the case of a problem, the server is down while you fix the errors. Fortunately, both web servers provide means to test configuration syntax and highlight any syntax errors while the server is still running.

In the case of Apache, the command is `apache2ctl configtest`. Be sure to run this command as a user who can read all of the configuration files (probably the root user). A successful run looks like this:

```
$ sudo apache2ctl configtest
Syntax OK
```

When there is a syntax error, this command will identify the file and line number of the error so it's easy to find:

```
$ sudo apache2ctl configtest
apache2: Syntax error on line 233 of /etc/apache2/apache2.conf: Could not open configuration
->file /etc/apache2/conf/: No such file or directory
```