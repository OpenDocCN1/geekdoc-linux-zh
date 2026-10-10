number of custom logs containing a variety of information (see the “Logging” section later in this chapter). The default location for Apache’s logs as installed by Fedora is `/var/log/httpd`.

# A Quick Guide to Getting Started with Apache

Setting up, testing a web page, and starting Apache with Fedora can be accomplished in just a few steps. First, make sure that Apache is installed on your system. Either select it during installation or install the server and related RPM files.

Next, set up a home page for your system by editing (as root) the file named `index.html` under the `/var/www/html` directory on your system. Make a backup copy of the original page or www directory before you begin so that you can restore your web server to its default state if necessary.

Start Apache (again, as root) by using the service command with the keywords `httpd` and `start`, like this:

```
# service httpd start
```

You can also use the `httpd` script under the `/etc/rc.d/init.d/` directory, like this:

```
# /etc/rc.d/init.d/httpd start
```

You can then check your home page by running a favorite browser and using `localhost`, your system’s hostname, or its Internet Protocol (IP) address in the URL. For example, with the `links` text browser, use a command line like this:

```
# links http://localhost/
```

For security reasons, you shouldn’t start and run Apache as root if your host is connected to the Internet or a company intranet. Fortunately, Apache is set to run as the user and group `apache` no matter how it’s started (by the `user` and `group` settings in `/etc/httpd/httpd.conf`). Despite this safe default, Apache should be started and managed by the user named `apache`, defined in `/etc/passwd` as:

```
apache:x:48:48:Apache:/var/www:/sbin/nologin
```

After you are satisfied with your website, use the `setup` (select Services) or `ntsysv` (select httpd) command to ensure that Apache is started properly.