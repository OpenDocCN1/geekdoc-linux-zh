# ## Using Graphical Administrative Interfaces

To simplify Linux administration, several graphical administrative utilities are now available. These graphical utilities put the information you enter into the correct configuration files and usually do some level of error-checking that is not available when you simply edit plain-text configuration files.

Graphical interfaces are a step in the right direction toward making Linux useable by the general population. The problem is, however, that these don’t yet allow you to do everything you need to do, so you will often find yourself having to edit a configuration file by hand after you have entered the information into that file using a graphical application. You will find that you need to do this less for simple tasks (such as adding a user account) than you will for more complex tasks (such as configuring servers).

The trend over the past few versions of Red Hat Linux has been to steer clear of the massive administrative interfaces (such as `linuxconf` and `Webmin`) and instead to offer graphical windows that perform individual administrative tasks. Instead of sharing common interfaces, they share common menus or folders. Then individual graphical windows for configuring a network, adding users, or setting up printers can be launched from that folder or menu.

Where you find your administrative GUI tools depends on which desktop you are using. The following sections describe how to access administrative GUI tools in GNOME or KDE.

# ## Starting graphical administrative interfaces

To administer your Red Hat Linux system through the GNOME or KDE desktops, you open a control panel that is similar to the control panel you might be used to from a Windows system. If you are using the KDE desktop, click the KDE Control Panel icon. Figure 10-2 shows an example of the KDE Control Panel.

![](bbox=[0.03, 0.61, 0.5, 0.83])

**Figure 10-2:** The KDE Control Panel contains GUI applications to manage your Red Hat Linux system.

If you are using the GNOME desktop, click the Start Here icon on the desktop or in the panel. The window that appears contains folders for different types of configuration. Tools for