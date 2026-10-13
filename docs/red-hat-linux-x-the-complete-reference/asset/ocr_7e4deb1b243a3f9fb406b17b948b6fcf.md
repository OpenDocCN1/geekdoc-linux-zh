# Apache GUI Configuration Tools

Red Hat provides a GUI configuration tool called the Apache Configuration Tool, accessible from the GNOME and KDE desktops. Also available is Comanche, a popular Apache configuration tool that you download from the Internet. The Apache GUI Project (gul.apache.org) provides a set of GUI tools for configuring and managing your Apache Web server. Its currently active projects are Comanche and TKApache. In the Linuxconf utility, you can also configure your Apache Web server. Webmin provides a very complete Apache Web server module.

The Apache Configuration Tool opens with a window displaying panels for Main, Virtual Hosts, Server, and Performance Tuning. In each of these you will see buttons to open dialog boxes where you can enter default settings. You will also be able to enter settings for particular items such as virtual hosts and particular directories. For example, in the Virtual Hosts panel you can enter default settings for all virtual hosts, as well as add and edit particular virtual hosts. Click the Help button to display a Web page-based reference manual that details how to use each panel. On the Main panel, you enter your Web server address, the Web master's e-mail address, and the ports the Web server will be listening on (see Figure 22-1).

![](bbox=[0.15, 0.5, 0.44, 0.7])

Figure 22-1: Apache Configuration Tool

On the Virtual Hosts panel, be sure to click the Edit Default Settings button to set the default settings for pages searches, error codes, log files, and directories. To add a virtual host, click Add to open a window where you can enter host information such as the virtual hostname and IP address. On the sidebar, you can select different configuration panels for the virtual host, such as log files and directory controls.

On the server panel, you set administrative settings such as the Apache server's user ID and the process ID file. The Performance Tuning panel lets you set different usage limits such as the maximum number of requests and the number of requests per connection.

When the Apache Configuration Tool saves its settings, it will overwrite the Apache configuration file, /etc/httpd/conf/httpd.conf. It is advisable that you first make a backup copy of your httpd.conf file in case you want to restore the original settings created by your distribution for Apache. If you have already manually edited this file, you will receive a warning, and the Apache Configuration Tool will make a backup copy in /etc/httpd/conf/httpd.conf.bak.