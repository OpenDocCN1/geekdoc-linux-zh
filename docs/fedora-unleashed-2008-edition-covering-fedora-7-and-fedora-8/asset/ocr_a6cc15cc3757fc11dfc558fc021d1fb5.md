# # Runtime Server Configuration Settings

At this point, the Apache server runs, but perhaps you want to change a behavior, such as the default location of your website’s files. This section talks about the basics of configuring the server to work the way you want it to work.

Runtime configurations are stored in just one file—`httpd.conf`, which is found under the `/etc/httpd/conf` directory. This configuration file can be used to control the default behavior of Apache, such as the web server’s base configuration directory (`/etc/httpd`), the name of the server’s process identification (PID) file (`/etc/httpd/run/httpd.pid`), or its response timeout (300 seconds). Apache reads the data from the configuration file when started (or restarted). You can also cause Apache to reload configuration information with the command `/etc/rc.d/init.d/httpd reload`, which is necessary after making changes to its configuration file. (You learned how to accomplish this in the earlier section, “Starting and Stopping Apache.”)

# ## Runtime Configuration Directives

You perform runtime configuration of your server with configuration directives, which are commands that set options for the `httpd` daemon. The directives are used to tell the server about various options you want to enable, such as the location of files important to the server configuration and operation. Apache supports nearly 300 configuration directives with the following syntax:

```
directive option option...
```

Each directive is specified on a single line. See the following sections for some sample directives and how to use them. Some directives set only a value such as a filename, whereas others enable you to specify various options. Some special directives, called *sections*, look like HTML tags. Section directives are surrounded by angle brackets, such as `<directive>`. Sections usually enclose a group of directives that apply only to the directory specified in the section:

```
<Directory somedir/in/your/tree>
  directive option option
  directive option option
</Directory>
```

All sections are closed with a matching section tag that looks like this: `</directive>`. Note that section tags, like any other directives, are specified one per line.

TIP
After installing and starting Apache, you’ll find an index of directives at http://localhost/manual/mod/directives.html.

![](bbox=[0.93, 0.6, 0.97, 0.7])