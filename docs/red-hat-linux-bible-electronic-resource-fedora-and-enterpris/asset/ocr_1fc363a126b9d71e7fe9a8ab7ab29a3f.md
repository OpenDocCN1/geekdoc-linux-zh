Understanding where GUI tools, commands, and files are located and how they are used will help you effectively maintain your Red Hat Linux system. Although most administrative features are intended for the root user, other administrative users (described later in this section) have limited administrative capabilities.

# ## Using Red Hat graphical administration tools

The trend over the past few versions of Red Hat Linux has been to steer clear of the massive administrative interfaces (such as `linuxconf` and `webmin`) and instead to offer graphical windows that perform individual administrative tasks. Instead of sharing one monolithic interface, they share common menus. Individual graphical windows for configuring a network, adding users, or setting up printers can be launched from that menu.

To administer your Red Hat Linux system through the GNOME or KDE desktops, Red Hat has provided a common menu (Red Hat calls it the Main Menu; I refer to it as the Red Hat menu). In GNOME click the red hat; in KDE, click the K icon in the lower-left corner of the desktop.

Because these administrative tasks require root permission, if you are logged in as a regular user you must enter the root password before the GUI application's window opens. For example, if you launch the *System Logs* window (System Tools → System Logs) from the GNOME menu as a regular user, you see the pop-up window shown in Figure 10-1.

![](bbox=[0.04, 0.49, 0.48, 0.64])

After you have entered the root password, most of the Red Hat configuration tools will open without requiring you to retype the password during this login session. Look for a "keys" icon in the lower right corner of the panel, indicating that you have root authorization. Click the keys to open a pop-up window that lets you remove authorization. Otherwise, authorization goes away when you close the GUI window.

> **NOTE:** As you configure different features on your Red Hat Linux system, you are asked to launch different individual graphical windows. In general, if you have a choice of tools for configuring a server or adding a feature, I recommend that you use the tool provided by Red Hat. That's because the Red Hat GUI tools more often integrate closely with the way Red Hat stores and manages its configuration information.