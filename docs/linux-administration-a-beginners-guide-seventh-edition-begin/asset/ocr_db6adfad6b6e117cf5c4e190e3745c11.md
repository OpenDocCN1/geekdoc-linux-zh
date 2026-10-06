# 496 Linux Administration: A Beginner's Guide

Suppose, for example, that we wanted to set up a virtual host configuration for a host named www.another-example.org. To do this, we can create a VirtualHost entry in the httpd.conf file (or use the Include directive to specify a separate file), like this:

```
<VirtualHost www.another-example.org>
ServerAdmin webmaster@another-example.org
DocumentRoot /www/docs/another-example.org
ServerName www.another-example.org
ErrorLog logs/another-example-error_log
</VirtualHost>
```

On Debian-like distros, we can use another set of utilities (a2ensite and a2dissite) to enable virtual hosts and sites quickly under Apache. For example, assuming we created the configuration file named www.another-example.org for the virtual web site and stored it under the /etc/apache2/sites-available/ directory, we can enable the virtual web site using the following command:

```
master@ubuntu-server:~ sudo a2ensite www.another-example.org
```

Similarly, to the virtual site, we can run this:

```
master@ubuntu-server:~ sudo a2dissite www.another-example.org
```

After running any of the previous commands (a2ensite and a2dissite), we should make Apache reload its configuration files by running the following:

```
master@ubuntu-server:~ sudo /etc/init.d/apache2 reload
```

Finally, don't forget that it is not enough to configure a virtual host using Apache's VirtualHost directive—the value of the ServerName in the VirtualHost container must be a value that is resolvable via DNS (or any other means) to the web server machine.

![](bbox=[0.14, 0.733, 0.256, 0.803])

> NOTE Apache's options/directives are too numerous to be covered in this section. But the software comes with its own extensive online manual, which is written in HTML so that you can access it in a browser. If you installed the software via RPM, you might find documentation for Apache has been packaged into a separate RPM binary, and as a result, you will need to install the proper package have access to it. If you downloaded and built the software from source code, you will find the documentation in the manual directory of your installation prefix (for example, /usr/local/httpd/manual). Depending on the Apache version, the documentation is available online at the project's web site at http://apache.org/docs/.