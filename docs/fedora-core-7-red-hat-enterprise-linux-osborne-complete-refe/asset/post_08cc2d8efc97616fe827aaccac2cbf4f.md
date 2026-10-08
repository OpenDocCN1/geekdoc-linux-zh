
## Apache Web Server Files and Directories (RPM Installation)

| Web Site Directories | Description |
|---|---|
| `/var/www/html` | Web site Web files |
| `/var/www/cgi-bin` | CGI program files |
| `/var/www/html/manual` | Apache Web server manual |

| Configuration Files | Description |
|---|---|
| `.htaccess` | Directory-based configuration files; an `.htaccess` file holds directives to control access to files within the directory in which it is located |
| `/etc/httpd/conf` | Directory for Apache Web server configuration files |
| `/etc/httpd/conf/httpd.conf` | Apache Web server configuration file |
| `/etc/httpd/conf.d` | Directory holding module configuration files like `ssl.conf` for SSL and `php.conf` for PHP |

| Service Scripts | Description |
|---|---|
| `/etc/rc.d/init.d/httpd` | Service script for Web server daemon |
| `/etc/sysconfig/httpd` | Red Hat and Fedora configuration options for Web server daemon, as used by the httpd service script |

| Application and Module Files | Description |
|---|---|
| `/usr/sbin` | Location of the Apache Web server program file and utilities |
| `/usr/share/doc/` | Apache Web server documentation |
| `/var/log/http` | Location of Apache log files |
| `/etc/httpd/modules` | Directory holding Apache modules |
| `/etc/httpd/run` | Directory holding Apache process IDs |

The Web server called `httpd` is in the `/etc/rc.d/init.d` directory. Symbolic links through which this script is run are located in corresponding runlevel directories. You will usually find the `$85$httpd` link to `/etc/rc.d/init.d/httpd` in the runlevel 3 and 5 directories, `/etc/rc.d/rc3.d` and `/etc/rc.d/rc5.d`. You can use the `chkconfig` command or the System V Init Editor to set the runlevels at which the httpd server will start, creating links in appropriate runlevel directories. The following command will set up the Web server (httpd) to start up at runlevels 3 and 5 (see Chapters 21 and 27 for more details on runlevels):

```bash
# chkconfig --level 35 httpd on
```

You can also use the `service` command to start and stop the httpd server manually. This may be helpful when you are testing or modifying your server. The `httpd` script with the `start` option starts the server, the `stop` option stops it, and `restart` will restart it. Simply killing the Web process directly is not advisable.

```bash
# service httpd restart
```

The **service** command uses the `/etc/sysconfig/httpd` configuration file to set options for the **httpd** service script. Here you can specify such options as whether to use the worker or prefork Apache MPM modules.

Apache also provides a control tool called `apachecl` (Apache control) for managing your Web server. With `apachecl`, you can start, stop, and restart the server from the command line. The `apachecl` command takes several arguments: `start` to start the server, `stop` to stop it, `restart` to shut down and restart the server, and `graceful` to shut down and restart gracefully. In addition, you can use `apachecl` to check the syntax of your configuration files with the `configtest` argument. You can also use `apachecl` as a system service file for your server in the `/etc/rc.d` directory.

Remember, `httpd` is a script that calls the actual `httpd` daemon. You could call the daemon directly using its full pathname. This daemon has several options. The `-d` option enables you to specify a directory for the `httpd` program if it is different from the default directory. With the `-f` option, you can specify a configuration file different from `httpd.conf`. The `-v` option displays the version.

```bash
# /usr/sbin/httpd -v
```

To check your Web server, start your Web browser and enter the Internet domain name address of your system. For the system `turtle.mytrek.com`, the user enters `http://turtle.mytrek.com`. This should display the home page you placed in your Web root directory. A simple way to do this is to use Lynx, the command line Web browser. Start Lynx, and type `g` to open a line where you can enter a URL for your own system. Lynx displays your Web site’s home page. Be sure to place an `index.html` file in the `/var/www/html` directory first.

Once you have your server running, you can check its performance with the `ab` benchmarking tool, also provided by Apache; `ab` shows you how many requests at a time your server can handle. Options include `-v`, which enables you to control the level of detail displayed, `-n`, which specifies the number of requests to handle (default is 1), and `-t`, which specifies a time limit.

> **NOTE** Currently there is no support for running Apache under xinetd. In Apache 2.0, such support is determined by choosing an MPM module designed to run on xinetd.

## Apache Configuration Files

Configuration directives are placed in the `httpd.conf` configuration file. A documented version of the `httpd.conf` configuration file is installed automatically in `/etc/httpd/conf`. It is strongly recommended that you consult this file on your system. It contains detailed descriptions and default entries for Apache directives.

Any of the directives in the main configuration files can be overridden on a per-directory basis using a `.htaccess` file located within a directory. Although originally designed only for access directives, the `.htaccess` file can also hold any resource directives, enabling you to tailor how Web pages are displayed in a particular directory. You can configure access to `.htaccess` files in the `httpd.conf` file.

In addition, many of the modules provided for Apache have their own configuration files. These are located in the `/etc/httpd/conf.d` directory.

## Apache Configuration and Directives

Apache configuration operations take the form of directives entered into the Apache configuration files. With these directives, you can enter basic configuration information, such as your server name, or perform more complex operations, such as implementing virtual hosts. The design is flexible enough to enable you to define configuration features for particular directories and different virtual hosts. Apache has a variety of different directives performing operations as diverse as controlling directory access, assigning file icon formats, and creating log files. Most directives set values such as **DocumentRoot**, which holds the root directory for the server's Web pages, or **Port**, which holds the port on the system that the server listens on for requests. The syntax for a simple directive is shown here:

```text
directive option option ...
```

Certain directives create blocks able to hold directives that apply to specific server components (also referred to as sectional directives). For example, the **Directory** directive is used to define a block within which you place directives that apply only to a particular directory. Block directives are entered in pairs: a beginning directive and a terminating directive. The terminating directive defines the end of the block and consists of the same name beginning with a slash. Block directives take an argument that specifies the particular object to which the directives apply. For the **Directory** block directive, you must specify a directory name to which it will apply. The `<Directory mydir>` block directive creates a block whose directives within it apply to the *mydir* directory. The block is terminated by a `</Directory>` directive. The `<VirtualHost hostaddress>` block directive is used to configure a specific virtual Web server and must include the IP or domain name address used for that server. `</VirtualHost>` is its terminating directive. Any directives you place within this block are applied to that virtual Web server. The `<Limit method>` directive specifies the kind of access method you want to limit, such as GET or POST. The access control directives located within the block list the controls you are placing on those methods. The syntax for a block directive is as follows:

```text
<block-directive option ... >
    directive option ... 
    directive option ...
    </block-directive>
```

Usually, directives are placed in one of the main configuration files. Directory directives in those files can be used to configure a particular directory. However, Apache also makes use of directory-based configuration files. Any directory may have its own .htaccess file that holds directives to configure only that directory. If your site has many directories, or if any directories have special configuration needs, you can place their configuration directives in their .htaccess files, instead of filling the main configuration file with specific Directory directives for each one. You can control what directives in a .htaccess file take precedence over those in the main configuration files. If your site allows user- or client-controlled directories, you may want to carefully monitor or disable the use of .htaccess files in them. (It is possible for directives in a .htaccess file to override those in the standard configuration files unless disabled with AllowOverride directives.)
