
Such tests are important because a configuration file error can result in your server shutting down when you try to restart it.

# NOTE

When you build and install Apache from source and don't use Fedora's Apache RPM files, start the server manually from the command line as root (such as when testing). You do this for two reasons:

- The standalone server uses the default HTTP port (port 80), and only the super-user can bind to Internet ports that are lower than 1024.
- Only processes owned by root can change their UID and GID as specified by Apache's User and Group directives. If you start the server under another UID, it runs with the permissions of the user starting the process.

Note that although some of the following examples show how to start the server as root, you should do so only for testing after building and installing Apache. Fedora is set up to run web services as the apache user if you use Fedora RPM files to install Apache.

# Using /etc/rc.d/init.d/httpd

Fedora uses the scripts in the /etc/rc.d/init.d directory to control the startup and shutdown of various services, including the Apache web server. The main script installed for the Apache web service is /etc/rc.d/init.d/httpd, although the actual work is done by the apachectl shell script included with Apache.

# NOTE

/etc/rc.d/init.d/httpd is a shell script and isn't the same as the Apache server located in /usr/sbin. That is, /usr/sbin/httpd is the program executable file (the server); /etc/rc.d/init.d/httpd is a shell script that uses another shell script, apachectl, to control the server. See Chapter 11 for a description of some service scripts under /etc/rc.d/init.d and how the scripts are used to manage services such as httpd.

You can use the /etc/rc.d/init.d/httpd script and the following options to control the web server:

- **start**—The system uses this option to start the web server during bootup. You, as root, can also use this script to start the server.
- **stop**—The system uses this option to stop the server gracefully. You should use this script, rather than the kill command, to stop the server.
- **reload**—You can use this option to send the HUP signal to the httpd server to have it reread the configuration files after modification.
- **restart**—This option is a convenient way to stop and then immediately start the web server. If the httpd server isn't running, it is started.
- **condrestart**—The same as the *restart* parameter, except that it restarts the *httpd* server only if it’s actually running.
- **status**—This option indicates whether the server is running; if it is, it provides the various PIDs for each instance of the server.

For example, to check on the status of your server, use the command

```
# /etc/rc.d/init.d/httpd status
```

This prints the following for me:

```
httpd (pid 15997 1791 1790 1789 1788 1787 1786 1785 1784 1781) is running...
```

This indicates that the web server is running; in fact, 10 instances of the server are currently running in this configuration.

In addition to the previous options, the *httpd* script also offers these features:

- **help**—Prints a list of valid options to the *httpd* script (which are passed onto the server as if called from the command line).
- **configtest**—A simple test of the server’s configuration, which reports Status *OK* if the setup is correct. You can also use *httpd*’s *-t* option to perform the same test, like this:

```
# httpd -t
```

- **fullstatus**—Displays a verbose status report.
- **graceful**—The same as the *restart* parameter, except that the *configtest* option is used first and open connections are not aborted.

Use the *reload* option if you’re making many changes to the various server configuration files. This saves time when you’re stopping and starting the server by having the system simply reread the configuration files.

## Controlling Apache with Fedora’s *service* Command

Instead of directly calling the */etc/rc.d/init.d/httpd* script, you can use Red Hat’s *service* command to start, stop, and restart Apache. The *service* command is used with the name of a service (listed under */etc/rc.d/init.d*) and an optional keyword:

For example, you can use `service` with `httpd` and any option discussed in the previous section, like so:

```
# service httpd restart
```

This restarts Apache if it's running or starts the server if it isn't running.

# Controlling Apache with Fedora's chkconfig Command

The `chkconfig` command provides a command-line-based interface to Fedora's `service` scripts. The command can be used to list and control which software services are started, restarted, and stopped for a specific system state (such as when booting up, restarting, or shutting down) and runlevel (such as single-user mode, networking with multitasking, or graphical login with X).

For example, to view your system's current settings, take a look at Fedora's default runlevel as defined in the system initialization table `/etc/inittab` using the `grep` command:

```
# grep id:/etc/inittab
id:3:inittab:default:
```

This example shows that this Fedora system boots to a text-based login without running X11. You can then use the `chkconfig` command to look at the behavior of Apache for that runlevel:

```
# chkconfig --list|grep httpd
httpd   0:off 1:off 2:off 3:off 4:off 5:off 6:off
```

Here you can see that Apache is turned off for runlevels 3 and 5 (the only two practical runlevels in a default Fedora system, although you could create a custom runlevel 4 for Apache). Use `--level`, `httpd`, and the control keyword `on` to set Apache to automatically start when booting to runlevel 3:

```
# chkconfig --level 3 httpd on
```

You can then again use `chkconfig` to verify this setting:

```
# chkconfig --list|grep httpd
httpd   0:off 1:off 2:off 3:on 4:off 5:off 6:off
```

To have Apache also start when your system is booted to a graphical login, again use `level`, `httpd`, and the control keyword `on`, but this time, specify runlevel 5 like so:

```
# chkconfig --level 5 httpd on
```

Again, to verify your system settings, use the following:

```
# chkconfig --list | grep httpd
httpd 0:off 1:off 2:off 3:on 4:off 5:on 6:off
```

Use the off keyword to stop Apache from starting at a particular runlevel.

## Graphic Interface Configuration of Apache

Some of Apache's basic behavior can be configured with Red Hat's `system-config-httd`, a GUI tool for the X Window System. This is an easy way to configure settings, such as Apache's user and group name, the location of PID and process lock files, or performance settings (such as the maximum number of connections), without manually editing configuration files.

> #### CAUTION
> If you use `system-config-httd`, you shouldn't try to manually edit the `httpd.conf` file. Manual changes are overwritten by the GUI client if you again use `system-config-httd`!

Launch this client by using your X desktop panel's Server Settings' HTTP Server menu item or from the command line of an X terminal window, like this:
$ `system-config-httd` &
After you press Enter, you're asked to type the `root` password. You then see the main client window shown in Figure 17.1.

![](img/34e72348d53ca54c2a1d9c871316691b_393_0.png)

**FIGURE 17.1** The `system-config-httd` main dialog box provides access to basic configuration of the Apache web server.

In the Main tab, you can set the server name, indicate where to send email addressed to the webmaster, and set the port that Apache uses. If you want, you can also configure specific virtual hosts to listen on different ports.

### Configuring Virtual Host Properties

In the Virtual Hosts tab, you can configure the properties of each virtual host. The Name list box contains a list of all virtual hosts operating in Apache. Edit a virtual host by opening the Virtual Hosts Properties dialog box, shown in Figure 17.2. You do this by highlighting the name of a virtual host in the Name list box of the Virtual Hosts tab and clicking the Edit button at the right of the tab. Use the General Options item in the Virtual Hosts Properties dialog box to configure basic virtual host settings.

![](img/34e72348d53ca54c2a1d9c871316691b_394_0.png)

**FIGURE 17.2** `system-config-https`'s Virtual Host Properties dialog box gives you access to numerous options for configuring the properties of an Apache virtual host.

Click the Site Configuration listing in the General Options list of this dialog box to set defaults, such as which files are loaded by default when no files are specified (the default is `index.*`) in the URL.

The SSL listing in the General Options pane gives you access to settings used to enable or disable SSL, specify certificate settings, and define the SSL log filename and location. Select the Logging listing to access options for configuring where the error messages are logged, as well as where the transfer log file is kept and how much information is put in it.
