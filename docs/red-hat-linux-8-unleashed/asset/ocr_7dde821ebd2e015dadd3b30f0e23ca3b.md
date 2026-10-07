# Runtime Server Configuration Settings

![](bbox=[0.156, 0.093, 0.814, 0.477])

FIGURE 16.1 Use the redhat-config-services client to set when Apache is started or stopped on your Red Hat Linux system.

# Runtime Server Configuration Settings

At this point, the Apache server will run, but perhaps you want to change a behavior, as the default location of your Web site's files. This section talks about the basics of configuring the server to the way you want it to work.

Runtime configurations are stored in just one file—httpd.conf, which is found under the /etc/httpd/conf directory. This configuration file can be used to control the default behavior of Apache, as the Web server's base configuration directory (/etc/httpd), the name of the server's process identification (PID) file (/etc/httpd/run/httpd.pid), or response timeout (300 seconds). Apache reads the data from the configuration file when started (or restarted). You can also Apache to reload configuration information with the command /etc/rc.d/init.d/httpd reload, which is necessary after making changes to its configuration file (you learn how to accomplish this in the later section, “Starting and Stopping Apache”).

# Runtime Configuration Directives

You perform runtime configuration of your server with configuration directives, which are commands that set options for the httpd daemon. The directives are used to tell the server