second URL above would retrieve /home/httpd/html/artists/sur-real/dali.html).

+   2. Where are the configuration files? Typically /etc/httpd/conf, /home/httpd/conf/, /usr/local/etc/httpd/conf, or something similar is used for this

+   3. Is the server running? Depending on how the server was configured when Linux was installed, the http daemon may start automatically at boot time. You can use the ps command to check if httpd is running: ps -waux | grep httpd. If it is not, you need to invoke it as root and tell it where to find the directory containing the configuration files. For example, if your configuration directory is /etc/httpd/conf, you would type something like httpd -d /etc/httpd. If the directory containing your httpd binary is not in your path, you will need to use the absolute path to invoke it. Typically httpd lives in one of the sbin directories:/usr/local/sbin, /usr/sbin, or on rare occasions/sbin.

Aside from the various modules that can be used to extend Apache at compile time, there are many items that can be specified at run time in the config files: httpd.conf and srm.conf. These two control parameters, such as aliases for directories, aliases for icons, CGI scripts/virtual host directories, the document root, the file to be served from a directory if no other file is specified in the URL, and various access control and authentication directives.

# <Directory> and .htacces

These tools are used to modify access of all types for directory trees. <Directory> directives typically reside in the srm.conf or httpd.conf files. It can also occur in the <Virtualhost> directive (more on this later). The .htacces file resides somewhere in a directory tree of HTML documents. In both instances, instances placed in the directories are recursively effective for all the files and subdirectories in that directory. For example, to enforce basic authorization for a directory and all its contents, you could put the following in a .htacces file in that directory (say /home/web):

```
AuthType Basic
AuthFile /home/cary/etc/passwd
AuthGroupFile /dev/null
AuthName Realm of the Kazoos
```