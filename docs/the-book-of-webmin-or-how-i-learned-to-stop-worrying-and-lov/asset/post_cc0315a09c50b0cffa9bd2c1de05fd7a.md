
necessary if a firewall prevents you from accessing port 10000 and you only have console or SSH access to the machine. In this case, editing the port option will alter the port, and the bind directive configures the address on which Webmin listens. Whenever editing the miniserv.conf file, Webmin must be restarted for changes to take effect.

## Logging

As mentioned earlier, Webmin provides very flexible logging features. With these features, you can very easily monitor what actions those users with administrator privileges are performing on the server. It is also possible to log actions based on the module where the actions are performed. The option **Log resolved host names** will cause Webmin to provide a host name rather than just an IP address for the client computer that performed an action. And **Clear logfiles every...hours** causes Webmin to rotate its own logs and keep them from overfilling the disk with old logs. If long-term logs are needed for security auditing purposes, it may be wise to include the Webmin log in your normal system backup rotation.

The decisions regarding what to log, whose actions to log, and how long to store those logs should be carefully considered for your situation. In some cases, a log is unnecessary, while in others it may be required by company policy or useful in addressing the security needs of your environment. If logging is enabled, care should be taken to ensure Webmin will have plenty of disk space in the Webmin log directory, as some options can lead to quite verbose logging (**Log changes made to files by each action**, for example). Remember that Webmin action logging has nothing to do with the logging features of other parts of the system. Syslog is configured separately in the **System:System Logs** module, while application-specific logging is usually configured within the application module.

## Proxy Servers

Webmin provides several tools that must connect to the Internet to operate correctly. These include the **Webmin Update** feature, the **Software Packages** module and others. If your local network uses a proxy to access Web or FTP sites on the Internet, you may configure those settings here. If your proxy requires authentication, the username Webmin will use to log-in can also be configured on this page in the **Username for proxy** and **Password for proxy** fields.

## User Interface

The Webmin user interface is configurable in a number of ways. In this module you may configure the colors of your Webmin pages. The colors are expected to be in standard hex triplets, as used in HTML markup on the Internet. You may also choose to use the standard fonts of your browser to display page titles, rather than the font provided by the theme you are using. Finally, you may configure where on the page Webmin will display the login name and host name of the server. This page does not configure Webmin themes, which are configured on their own page, and the changes that can be made here are mild by comparison to the possibilities when using themes. Be aware also that these changes may not take effect when using a theme other than the old standard Webmin theme. For example, the new MSC.Linux theme overrides all of these options with its own standard values.

## Webmin Modules

As previously mentioned, one of the best things about Webmin is that it is completely modular. Every server daemon, every system feature, every Webmin feature, has its own module that connects to the core Webmin libraries and answers to the Webmin miniserv.pl web server. Because of the elaborate, but still easily comprehensible, modular framework that Webmin provides, it is very easy to write full-featured modules that integrate seamlessly into Webmin and your operating system.

## Install Module

From this page, you can install new modules, either from a local file, an uploaded file, or a file downloaded from an FTP site or website. Webmin module packages are simply tar archive files that contain the complete directory structure of the module. These modules end in the suffix .wbm

> NOTE A great resource for additional Webmin modules is the Third Party Modules for Webmin [http://www.thirdpartymodules.com/webmin] page, run by Richard Teachout. Richard is a longtime fan and supporter of Webmin and a regular contributor to the Webmin discussion lists. After spending some time on the list, he perceived a need for a comprehensive resource for modules that work with Webmin. At the time of this writing, there are over 200 modules listed at his site, though it should be mentioned that the site also lists the modules included in the standard Webmin distribution. If you've written a Webmin module, you should post it to this site, so others will be able to easily find and benefit from your efforts. It is also a great place to find example code to help you when writing your own modules (in addition to the standard modules, of course!). Beware, however, that as with any group of free software the modules vary wildly in quality. Some are excellent and on par with any of the best standard Webmin modules, while others are in such an early stage of development that they are not useful.

## Clone Module

The Clone Module feature provides an impressive amount of flexibility for administrators who must provide limited administration access for several instances of the same software on the same machine. If, for example, you have two different Apache configurations running on your system, you could clone the Apache module to allow different users to access the different Apache configurations.

> **CAUTION** *While this feature does allow interesting and powerful options for multiple users configuring similar services, Webmin should not yet be viewed as an ideal tool for administering a virtual hosting server, where many users configure the Apache virtual servers, Sendmail aliases, and DNS entries. There are a number of commercial and Open Source efforts underway to provide such services within the framework of Webmin. At the time of this writing none are production-ready, but with the number of people pursuing the goal, it is likely that such a tool is not far off.*

To clone a module, select the module to clone from the drop-down menu, then enter a new name for the module. To avoid the problem of the new module interfering with the original module, you will want to carefully consider the service being administered by the cloned module. Usually, you will need to set up the new clone with a wholly separate installation of the service being configured. So, for example, if you have cloned Squid so that you may run two different Squid processes you *must* configure them to use separate configuration files, cache directories, log files, and process IDs. If this precaution is not taken, one or both of the processes will behave erratically or fail to work at all.

## Example: Cloning the Squid Module

To take the example further, let's create a clone of the Squid module and configure two Squid processes to run on the same server without stepping on each other. First, copy the squid.conf configuration file from the command line or the Webmin File Manager to a file named squid2.conf

```
[root@delilah /]# cp /etc/squid/squid.conf /etc/squid/squid2.conf
```

Next, create your module clone of the Squid module (referred to as Squid2 from here on). Browse to the newly created clone module, and edit the module configuration by clicking the Module Config link in the upper left corner of the Squid2 index page. Here you should change the Full path to squid config file to point to the newly created configuration file. You will also need to change the Command to start squid and Command to stop squid to point to another file name as well; let's call it /etc/rc.d/init.d/squid2. We'll have to actually create these files before trying to start up our new Squid process.

We will also need to alter the Full path to PID file to point to squid2.pid rather than squid.pid and change the log directory name. I usually use /var/log/squid2 for a cloned Squid process. This is all that is required within the module configuration for the moment. Click Save to save your changes and return to the Squid2 index page.

Now that we've told Webmin the file to edit, we can actually edit it to configure Squid to operate independently of Squid. First we'll need to change Squid2 to operate on a different port or IP than Squid, because no two processes can listen on the same IP-port combination. 8080 is a good secondary cache port to use. This option is configured in Squid2:Ports and Networking. Next alter the cache directories to something different than the Squid cache directories, because they cannot be shared. The same must be done for the access.log,
