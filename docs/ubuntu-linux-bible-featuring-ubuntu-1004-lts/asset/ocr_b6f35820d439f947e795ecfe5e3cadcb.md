# Chapter 29: Setting Up a Web Server

Suppose then that you also wanted to make the Apache documentation explicitly available through the URI /doc/manual/. Although there is no such directory, it's easy enough to make an entry in the server's configuration file defining a re-direct to an existing directory. So let's make one. Inside the <VirtualHost block, create something like the entry for the /doc/ directory that's shown in lines 32 through 39, but simplify it a bit:

+   1. Alias /manual/ "/usr/share/doc/apache2-doc/manual/"
2. <Directory> "/usr/share/doc/apache2-doc/manual/"
3. Order deny,allow
4. Deny from all
5. Allow from 192.168.16 127.0.0.1
6. </Directory>

# Note

Again, the line numbers are not actually present in the file—I'm just using them in the example to make it easier to refer to specific lines.

Line 1 defines alias /manual/ which actually points to the directory /usr/share/doc/apache2-manual/, which is Apache's online manual lives. The rest of the lines define who has access to directory and under what circumstances. Line 2 defines the naming of directives related to the directory /usr/share/doc/apache2-doc/manual/, and line 6 identifies the end of a block of directives for a specific directory. Lines 3, 4, and 5 specify how authentication works. Line 3 says that any statements denying access to the directory are processed before any allow access to the directory. Line 4 denies all access to that directory, while line 5 allows access to that directory from any host whose first octets are 192.168.6 (the subnet on which this Web server is running), and the loopback address for that host. After adding these changes to the file (they must come before the </VirtualHost> directive shown in line 39 of the previous example because they are part of the definition for this host on this Web server), you can restart the Web server using the same command as:

```
$ sudo /etc/init.d/apache2 restart
```

Because the startup script Apache runs the apache2ctl utility (Apache's main administrative utility), you could also restart the Apache server by executing the following command:

```
$ sudo apache2ctl restart
```

Visiting the same URI as before and trying to access the Apache documentation hyperlink now shows the page shown in Figure 29-2.