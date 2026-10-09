
# Apache Configuration Files

Apache’s configuration information is contained in a select bunch of configuration files:

- The `/etc/httpd/httpd.conf` file is Apache’s main configuration file.
- The `/etc/httpd/conf.d` directory contains configuration files for any installed modules (such as PHP, SSL, and so on).
- The `/etc/httpd/logs` directory is a symbolic link to `/var/log/httpd` directory, which contains all the Apache log files.
- The `/etc/httpd/modules` directory is a symbolic link to `/usr/lib/httpd/modules` directory, which contains all the Apache modules configured as dynamic shared objects.

Dynamic shared objects (or DSOs) are modules that are compiled separately from the Apache `httpd` binary. They are so-called because they can be loaded on demand. There’s more information on DSOs at http://httpd.apache.org/docs-2.0/mod.

- The `/etc/httpd/run` directory is a symbolic link to `/var/run`, which contains the process ID file (`httpd.pid`) of the `httpd` process.
- `/etc/rc.d/init.d/httpd` is a shell script, used for starting and stopping the Apache web server.

## Starting Apache for the First Time

You can start Apache using the Red Hat Service Configuration GUI dialog, or via the command line. Here’s how to start Apache from the Service Configuration dialog:

- First, you need to fire up the GUI. To do this, click on **Main Menu | System Settings | Server Settings | Services** or type the following at the command line:

```bash
$ redhat-config-services
```

It will ask for root password if you started it as a normal user. When you do this, you get the Service Configuration dialog:

![](img/b852150740856958b10aff9e8c9d2adc_351_0.png)

This dialog contains a list of all the services that are supported on your computer. The checkboxes indicate which of these services are started automatically when the machine boots up (as part of the *cron*). There are also **Start**, **Stop**, and **Restart** buttons so that we can start and stop services manually.

- Scroll down the list on the left of the dialog, and select the entry for **httpd**. As we said, the `httpd` service is the Apache web server service. Check the status of the `httpd` service, in the bottom-right of the dialog; if it is **stopped** (as above), then click the **Start** button to start it.

If you want it to start automatically next time you reboot your machine, check the checkbox too. Then select **File | Save Changes** to save the new settings. That's it; you can close the **Service Configuration** dialog by selecting **File | Quit**.

To control the Apache web server from the command line, we can use the **service** command to fire the **httpd** script. Here's how we use it to start the web server:

```bash
# service httpd start
Starting httpd:                                     [ OK ]
```

If there are difficulties in starting the web server, then you'll find out about it here. For example, if you attempt to do this without root privileges, then you'll get a message telling you that permission is denied. And here's another example:

```bash
# service httpd start
Starting httpd: httpd: Could not determine the server's fully qualified
domain name, using 192.168.0.99 for ServerName
                                                         [ OK ]
```

Here, the message explains that the server's fully qualified domain name (FQDN) couldn't be determined, and that it's using the IP address (192.168.0.99) instead. If you get this message, it's because you have neither setup a FQDN for your Linux server, nor configured the *ServerName* configuration directive in the **httpd.conf** configuration file.

> An FQDN is a unique name, consisting of hostname and domain name, which can be resolved to an IP address. For example, www.linux4biz.net is a fully qualified domain name.

Returning to the **httpd** script itself, there are similar switches for stopping or restarting the service:

```bash
# service httpd restart
Stopping httpd:                                    [ OK ]
Starting httpd:                                    [ OK ]
# service httpd stop
Stopping httpd:                                    [ OK ]
```

There are a few other options you can use with the `httpd` script. If you run the script without an option, the resulting usage message reveals all the available options:

```bash
# service httpd
Usage: httpd
{start|stop|restart|condrestart|reload|status|fullstatus|graceful|
help|configtest}
```

The `configtest` option is a particularly useful one. The configuration file is quite complex, and so it’s useful to check it for errors after you make changes to it. To do this, you use the `configtest` option:

```bash
# service httpd configtest
Syntax OK
```

# Testing the Apache Web Server

Once you’ve started the Apache web server, you should test it to see if it’s working properly. To do that, we’ll use a web browser to request a web page from our server! There’s a page provided by default for this purpose, and you can request it via the URL `http://localhost`. So, launch a web browser (**Main Menu | Internet | Mozilla Web Browser**), and type this URL into the address box:

![](img/b852150740856958b10aff9e8c9d2adc_353_0.png)

# Configuring your Web Server

It’s a good idea to configure your web server. Red Hat does provide a GUI tool, `apacheconf`, for configuring Apache, but it does not format the configuration file very well. Webmin (http://www.webmin.com – see Chapter 13) is an alternative web-based software that can be used to manage most of the Linux services, including the Apache web server. However, in this section we’ll show you how to do some basic configuration by editing the `httpd.conf` Apache configuration file directly.

## Try It Out Configuring Your Web Server

We’re going to configure the web server by adjusting a couple of the settings to suit our needs.

1. Launch the gedit text editor (by selecting **Main Menu | Accessories | Text Editor**), or your favorite text editor. Use it to open the file `/etc/httpd/conf/httpd.conf`.

2. Select **Search | Find** and use the resulting dialog to find the word `ServerAdmin` in the file. The first occurrence should be the `ServerAdmin` directive, which looks like this:

```text
# ServerAdmin: Your server address, where problems with the server should be
# e-mailed. This address appears on some server-generated pages, such
# as error documents. e.g. admin@your-domain.com
ServerAdmin root@localhost
```

As you can see, the configuration file describes this directive very well. Change the email address to your own email address, or an address that you may have set up for web site administration. For example:

```text
# ServerAdmin: Your server address, where problems with the server should be
# e-mailed. This address appears on some server-generated pages, such
# as error documents. e.g. admin@your-domain.com
ServerAdmin webmaster@linux4biz.net
```

3. Now use the same technique to find the `ServerName` directive (you’ll probably find that it’s right after the `ServerAdmin` directive). Change this directive first by removing the leading # character. Then, if you have a registered DNS name, add it here (in place of the DNS name `test.linux4biz.net`, which I’m using here to demonstrate):

```text
# ServerName gives the name and port that the server uses to identify itself.
# ...
ServerName test.linux4biz.net
```
