
Here you can see that Apache is turned off for runlevels 3 and 5 (the only two practical runlevels in a default Fedora system, although you could create a custom runlevel 4 for Apache). Use `level httpd` and the control keyword `on` to set Apache to automatically start when booting to runlevel 3.

```bash
# chkconfig --level 3 httpd on
```

You can then again use `chkconfig` to verify this setting:

```bash
# chkconfig --list | grep httpd
httpd                     0:off    1:off    2:off    3:on     4:off    5:off    6:off
```

To have Apache also start when your system is booted to a graphical login using X, again use `level httpd`, and the control keyword `on`, but this time, specify runlevel 5 like so:

```bash
# chkconfig --level 5 httpd on
```

Again, to verify your system settings, use:

```bash
# chkconfig --list | grep httpd
httpd                     0:off    1:off    2:off    3:on     4:off    5:on     6:off
```

Use the `off` keyword to stop Apache from starting at a particular runlevel.

## Controlling Apache with Red Hat's system-config-services Client

You can also use a graphical version of the `chkconfig` command named `system-config-services`, during an X session to set when Apache is started or stopped and at which runlevel. To start `system-config-services`, select the Services on the Server Settings menu from your desktop panel's System Settings menu, or type the command in a terminal window like so:

```bash
$ system-config-services &
```

After you press Enter, you're prompted for the root password (because you shouldn't be running X as root).

This client is a graphical runlevel editor. To have Apache start when using runlevel 3, first use the Edit Runlevel menu to select runlevel 3 and then scroll through the list of services to find `httpd`. If you click the `httpd` check box, as shown in Figure 21.1, and then click the toolbar's Save button, Apache is started at that runlevel the next time the system starts or reboots.

You can also use the Service Configuration client to instantly control a service. Use the Edit Runlevel menu to select the current runlevel in use; highlight `httpd`; and then click the Start, Stop, or Restart toolbar button.

![](img/2045828cf45e5632bf056f9ca99d6755_570_0.png)

**FIGURE 21.1** Use the system-config-services client to set when Apache is started or stopped on your Fedora system.

## Runtime Server Configuration Settings

At this point, the Apache server runs, but perhaps you want to change a behavior, such as the default location of your website's files. This section talks about the basics of configuring the server to work the way you want it to work.

Runtime configurations are stored in just one file—`httpd.conf`, which is found under the `/etc/httpd/conf` directory. This configuration file can be used to control the default behavior of Apache, such as the web server's base configuration directory (`/etc/httpd`), the name of the server's process identification (PID) file (`/etc/httpd/run/httpd.pid`), or its response timeout (300 seconds). Apache reads the data from the configuration file when started (or restarted). You can also cause Apache to reload configuration information with the command `/etc/rc.d/init.d/httpd reload`, which is necessary after making changes to its configuration file. (You learned how to accomplish this in the earlier section, “Starting and Stopping Apache.”)

### Runtime Configuration Directives

You perform runtime configuration of your server with configuration directives, which are commands that set options for the `httpd` daemon. The directives are used to tell the server about various options you want to enable, such as the location of files important to the server configuration and operation. Apache supports nearly 300 configuration directives using the following syntax:

```
directive option option...
```

Each directive is specified on a single line. See the following sections for some sample directives and how to use them. Some directives set only a value such as a filename, whereas others enable you to specify various options. Some special directives, called sections, look like HTML tags. Section directives are surrounded by angle brackets, such as `<directive>`. Sections usually enclose a group of directives that apply only to the directory specified in the section:

```
<Directory "/your/source/">
	directive option option
	directive option option
</Directory>
```

All sections are closed with a matching section tag that looks like this: `</directive>`. Note that section tags, like any other directives, are specified one per line.

> **TIP**
> After installing and starting Apache, you'll find an index of directives at http://localhost/manual/mod/directives.html.

## Editing httpd.conf

Most of the default settings in the config file are okay to keep, particularly if you've installed the server in a default location and aren't doing anything unusual on your server. In general, if you don't understand what a particular directive is for, you should leave it set to the default value.

The following sections describe some of the configuration file settings you *might* want to change concerning operation of your server.

### ServerRoot

The `ServerRoot` directive sets the absolute path to your server directory. This directive tells the server where to find all the resources and configuration files. Many of these resources are specified in the configuration files relative to the `ServerRoot` directory.

Your `ServerRoot` directive should be set to `/etc/httpd` if you installed the RPM or `/usr/local/apache` (or whatever directory you choose when you compiled Apache) if you installed from the source.

### Listen

The `Listen` directive indicates on which port you want your server to run. By default, this is set to 80, which is the standard HTTP port number. You might want to run your server on another port—for example, when running a test server that you don't want people to find by accident. Don't confuse this with real security! See the "File System Authentication and Access Control" section for more information about how to secure parts of your web server.

### User and Group

The user and group directives should be set to the UID and group ID (GID) the server uses to process requests. In Fedora, set these configurations to a user with few or no privileges. In this case, they're set to user `apache` and group `apache`—a user defined specifically to run Apache. If you want to use a different UID or GID, be aware that the server will run with the permissions of the user and group set here. That means in the event of a security breach, whether on the server or (more likely) in your own CGI programs, those programs run with the assigned UID. If the server runs as root or some other privileged user, someone can exploit the security holes and do nasty things to your site. Always think in terms of the specified user running a command such as `rm -rf /` because that would wipe all files from your system. That should convince you that leaving `apache` as a user with no privileges is probably a good thing.

Instead of specifying the User and Group directives using names, you can specify them using the UID and GID numbers. If you use numbers, be sure that the numbers you specify correspond to the user and group you want and that they're preceded by the pound (#) symbol.

Here's how these directives look if specified by name:

```
User apache
Group apache
```

Here's the same specification by UID and GID:

```
User #48
Group #48
```

> **TIP**
> If you find a user on your system (other than root) with a UID and GID of 0, your system has been compromised by a malicious user.

### ServerAdmin

The `ServerAdmin` directive should be set to the address of the webmaster managing the server. This address should be a valid email address or alias, such as `webmaster@gnulix.org`, because this address is returned to a visitor when a problem occurs on the server.

### ServerName

The `ServerName` directive sets the hostname that the server returns. Set it to a fully qualified domain name (FQDN). For example, set it to `www.your.domain` rather than simply `your.domain`. This is particularly important if this machine will be accessible from the Internet rather than just on your local network.

You don't need to set this unless you want a name other than the machine's canonical name returned. If this value isn't set, the server will figure out the name by itself and set it to its canonical name. However, you might want the server to return a friendlier

![](img/2045828cf45e5632bf056f9ca99d6755_572_0.png)
