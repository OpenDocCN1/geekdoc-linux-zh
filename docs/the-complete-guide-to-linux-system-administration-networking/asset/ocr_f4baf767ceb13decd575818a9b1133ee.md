# Creating a Linux Web Server with Apache

The most widely used Web server in the world is Apache. Apache is included with Red Hat Linux and is installed as part of Fedora if you selected the software categories listed in Table 8–4. Some of the features of Apache that make it popular include:

+   - A regular development cycle that keeps up with Web technology and provides a very reliable product
+   - Virtual hosting, which allows a single Web server to provide documents for multiple Web sites (multiple domain names)
+   - A modular design that lets Web administrators add and remove functionality to meet their site’s needs
+   - Many security options and performance tuning settings
+   - A broad support base, despite being free software (for example, see www.apacheweek.com)

The Apache server runs as a daemon named httpd. Although you can control it using the service utility, the preferred method is to use the apachectl program. For example, after you have configured Apache as described in this section, you can check that the syntax of your configuration file is valid by entering this command:

```
# apachectl -t
```

Start the server using this command:

```
# apachectl -k start
```

Apache configuration files are stored in /etc/httpd.conf. The main configuration file, /etc/httpd/conf/httpd.conf, contains hundreds of configuration options, along with comments describing most of them. Each configuration option in this file is called a directive. Whenever you change the configuration file, you should restart Apache using this command:

```
# apachectl -k restart
```

Because the configuration file contains examples of all the directive types you are likely ever to need for Apache, exploring that file and reading the comments it contains can give you a solid understanding of what Apache is capable of and how to take advantage of those capabilities. The online documentation provided at www.apache.org is also worth researching when you have questions about specific directives that you are considering using. But more immediately, you can start your Web browser, choose Open File on the File menu, and browse to the directory /var/www/manual/. Within that directory, the files ending with the .en file extension are English language documentation files that you can view directly in your browser.

The DocumentRoot directive in httpd.conf defines where the server looks for documents that are returned to clients. If a client requests a document from the root of the server (without giving a path name in the URL), that document actually comes from the directory