# Table 22-3: Apache Modules (Apache 2.0)

| Module | Description |
|---|---|
| mod_rewrite | Powerful URI-to-filename mapping using regular expressions |
| mod_setenvif | Sets environment variables according to client information |
| mod_so | Support for loading modules at runtime |
| mod_spelling | Automatically corrects minor typos in URLs |
| mod_ssl | Interface for SSL encryption supported by OpenSSL |
| mod_status | Server status display |
| mod_userdir | User home directories |
| mod_unique_id | Generates unique request identifier for every request |
| mod_usertrack | User tracking using cookies (replacement for mod_cookies.c) |
| mod_vhost_alias | Support for dynamically configured mass virtual hosting |

# Starting and Stopping the Web Server

On most systems, Apache is installed as a standalone server, continually running. As noted in Chapter 20, in the discussion of init scripts, your system automatically starts up the Web server daemon, invoking it whenever you start your system. On Red Hat, a startup script for the Web server called httpd is in the /etc/rc.d/init.d directory. Symbolic links through which this script is run are located in corresponding runlevel directories. You will usually find the S85httpd link to /etc/rc.d/init.d/httpd in the runlevel 3 and 5 directories, /etc/rc.d/rc3.d and /etc/rc.d/rc5.d. You can use the chkconfig command or the System V Init Editor to set the runlevels at which the httpd server will start, creating links in appropriate runlevel directories. The following command will set up the Web server (httpd) to start up at runlevels 3 and 5 (see Chapters 20 and 27 for more details on runlevels).

```
chkconfig --level 35 httpd on
```

On Red Hat, you can also use service command to start and stop the httpd server manually. This may be helpful when you are testing or modifying your server. The httpd script with the start option starts the server, the stop option stops it, and restart will restart it. Simply killing the Web process directly is not advisable.

```
service httpd restart
```

Apache also provides a control tool called apachectl (Apache control) for managing your Web server. With apachectl, you can start, stop, and restart the server from the command line. apachectl takes several arguments: start to start the server, stop to stop it, restart to shut down and restart the server, and graceful to shut down and restart gracefully. In addition, you can use apachectl to check the syntax of your configuration files with the config argument. You can also use apachectl as a system startup file for your server in the /etc/rc.d directory.

Remember, httpd is a script that calls the actual httpd daemon. You could call the daemon directly using its full pathname. This daemon has several options. The -d option enables you to specify a directory for the httpd program if it is different from the default directory. With the -f option, you can specify a configuration file different from httpd.conf. The -v option displays the version.

```
/usr/sbin/httpd -v
```

To check your Web server, start your Web browser and enter the Internet domain name address of your system. For the system turtle.mytrek.com, the user enters http://turtle.mytrek.com. This should display the home page you placed in your Web root directory. A simple way to do this is to use Lynx, the command line Web browser. Start Lynx, and type g to open a line where you can enter a URL for your own system. Lynx displays your Web site's home page. Be sure to place an index.html file in the