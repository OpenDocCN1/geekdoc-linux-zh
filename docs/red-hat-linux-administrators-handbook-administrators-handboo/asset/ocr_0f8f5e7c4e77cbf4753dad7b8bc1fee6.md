The scrollable screen shows the state of all the services in the current run level. To turn on a service, you need to select it; to turn off a service, you simply deselect it. After you make all the changes, you can save the changes by clicking the OK button, or you can abort your changes by clicking the Cancel button. If you want to work on a different run level configuration, simply supply the run level with the --level option. For example,

```
ntsysv --level 1
```

enables you to work on the run level 1 configuration.

# Using linuxconf to manage run levels

You can also use the linuxconf tool to configure run levels. Follow these instructions:

+   1. Select Control ↔ Control Panel ↔ Control Service.
+   2. Enable or disable one or more services.
+   3. Accept the changes.
+   4. Activate the changes before you quit linuxconf.

# Creating a new service for a run level

If you install server software packages from well-known vendors, most likely they will provide you with a nice RPM package that also includes the necessary service script to go in /etc/rc.d/init.d. Sometimes, however, you will find useful software that does not come with all the bells and whistles, and you will end up customizing it, or at least modifying how it works on your system. In such a case, you might need to create a service script for your new software. This section shows how you can easily create a new service script that goes in the /etc/rc.d/init.d directory.

First, take a look at Listing 2-4, which shows the httpd script, an existing service script from the /etc/rc.d/init.d directory. This script is used to start and stop the Apache Web server.