# The LAMP Stack

One of the powers of Apache as a web server is the way it can be integrated with other software components. The most common version of such is known as the LAMP stack, which refers to its components: Linux, Apache, MySQL, and one of three scripting languages (Perl, Python, or PHP).

There's no expectation from the RHCE objectives that you'll have to install a Structured Query Language database system such as MySQL (My Structured Query Language), or any scripting language. However, they do explain many of the modules available as part of the Apache configuration files. And of course, Apache works with other SQL databases along with other scripting languages.

# Installation

The RPM packages required by Apache are included in the Web Server package group. The simplest way to install Apache after installation is with the following command:

```
# yum install httpd
```

But additional packages are required. It may be simpler to install the mandatory and default packages associated with the Web Server package group with the following command:

```
# yum groupinstall "Web Server"
```

If you don't remember the names of available groups, run the yum grouplist command. The standard method to start Linux services is with a script in the /etc/init.d directory. It contains an httpd script. However, you can stop and start Apache, as well as reload the configuration file gracefully with the following commands:

```
# apachectl stop
# apachectl start
# apachectl graceful
```

No configuration is required for the most basic operation. Once Apache is running, start a web browser and enter a URL of https://localhost. For example, Figure 14-1 displays the default home page for Apache, based on the default configuration, in the elinks web browser. The web page is based on the contents of the /etc/httpd/conf.d/welcome.conf file, which refers to the /var/www/error/noindex.html file for more information.