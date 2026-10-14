and to disable it I can use `a2dissite`:

```
$ sudo a2dissite mysite
```

The default site is a special case in that it prepends `000` to its symlink under sites-enabled to make sure that it loads first and works properly as the default virtual host.

+   - **/var/www/**
+     This is the default document root for Apache. Any HTML file that is readable by Apache and placed in this directory will be available once you point a Web browser at the server. There is already a default index.html in that directory.
+   - **/usr/lib/cgi-bin/**
+     This is the default location for CGI scripts. Any scripts referenced on the Web server by /cgi-bin will point here.
+   - **/var/log/apache2/**
+     This is the standard directory where Apache logs are stored. The access.log file contains information about what files have been accessed on the Web server, and the error.log file lists any Apache errors. If, for instance, you have trouble starting Apache, look in error.log for clues.

# apache2ctl

The `/usr/sbin/apache2ctl` program is the primary command-line program you will use to manage Apache under Ubuntu. The syntax for the command is fairly straightforward. Run apache2ctl from the command line and pass a single command to it as an argument. The simple commands start, stop, and restart will, as you might imagine, start, stop, and restart the Apache process respectively. You could also achieve the same functionality with the apache2 init script, so three commands that do the same thing are

```
$ sudo apache2ctl restart
$ sudo /etc/init.d/apache2 restart
$ sudo service apache2 restart
```