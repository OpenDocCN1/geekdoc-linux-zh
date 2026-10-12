
## Table 10.4 Functions available under Control category (continued)

| Main Category | Subcategory | Description |
| :--- | :--- | :--- |
| | Shutdown/ Reboot | Runs the **/usr/bin/shutdown** command |
| | Control service activity | Enables/disables system services, i.e., those started by the system during normal booting |
| | Mount/Unmount file systems | Same as the Control service activity item above |
| | Control configured local drives | Same as the Control service activity item above |
| | Control configured nfs volumes | Same as the Control service activity item above |
| | Mount other NFS file systems | Same as the Control service activity item above |
| | Configure super-user scheduled tasks | Maintains a crontab entry for the root account |
| | Archive configurations | Not implemented |
| | Switch system profile | Controls the use of one or more system profiles that can be activated on command |
| | Control PPP/SLIP/PLIP links | Enables or disables network links |
| | Control files and systems | |
| | Configure all configuration files | Provides the ability to maintain important system configuration files. Specific files include `/etc/HOSTNAME`, `/etc/aliases`, and `/etc/exports`. |
| | Configure all commands and daemons | Configures the mapping between system command names and the commands themselves. For instance, `cat` maps to `/bin/cat` |
| | Configure file permission and ownership | Controls the permission of files and directories across the system |
| | Configure Linuxconf modules | Administers Linux modules. Each can be activated or deactivated |
| | Configure system profiles | Toggles between one or more system configuration profiles |
| | Override Linuxconf addons | Controls Linux modules |
| | Create Linuxconf addons | Defines a new Linux module |
| | logs | |
| | date & time | Controls system date and time settings |
| | Features | Controls special behavior of the Linuxconf program |

## tkined Tool—Network Editor

The **tkined** network editor that is available with the Scotty network package provides a graphical user interface (GUI) for a large number of network monitoring and support functions. Also, it provides an interactive editor for creating and manipulating network topology maps. The tool is customizable by the user, and additional networking and system tools can be integrated into the basic package. The software is based on the XWindow system and is available and supported on several different operating system platforms.

### tkined Overview

The **tkined** application is a fully featured network manager that provides many of the management capabilities found in some of the more popular commercial products. This tool is considered one of the best public domain network monitoring packages available and boasts many features and functions. The **tkined** application isn't a complicated software package, but it does contain many menu items, submenus, sub-windows, and specific modules. As a result, you must review the basics in order to start using the software right away.

From a functional standpoint, **tkined** does the following:

- discovers networking devices and systems
- creates/maintains network maps and views
- manages SNMP devices
- supports IP monitoring
- creates performance graphs and charts

To start the application, invoke the **tkined** command within a shell prompt:

```
# /usr/bin/tkined
```

Executing the command will display the main window shown in Figure 11.1. By default, the window contains no objects or network devices because a certain amount of customization must be done before **tkined** can monitor your network.

The main window contains a full complement of menu items, a tool selection palette on the left, and a network topology mapping panel. The network mapping panel is used to display a variety of network elements in icon format. The package contains a large number of icons that you can use to represent specific devices and systems, or specific network topologies such as bus and ring that may be found on a network. Finally, you can create different views that contain specific devices, entire subnetworks, charts and graphs, and other items.

![](img/f265c9d1f2610aca197c430cbfcd51f5_600_0.png)

**Figure 11.1** Main tkined window.

## Topology Views

The package supports the idea of using different views to represent various aspects of the network, such as Cisco routers or a number of critical servers. You can create additional views to house performance graphs or entire subnets. When the application is first started, an empty view is created. The name of the view is displayed in the header of the main application window. The name of the view is also the name of the file in which the view is stored. The default view file is noname.txt, which you can change.

The primary purpose of views is to help divide the network into smaller components. The sheer number of systems on many networks makes it very difficult to monitor the networks, but, by partitioning the network into different elements or components, you can make the task much easier. The choice of how to break apart the network is really up to you. The important thing to remember is that you should partition the network into logical or functional areas that best fit your department or company business model.

For instance, let's assume you work for the network group that is primarily responsible for support of the backbone network and Wide Area Network (WAN). Support for specific subnets rests with individual departments, which basically means that devices can be added, moved, or removed for these subnets at any time. As a result, it may not be reasonable to monitor specific end nodes or devices contained within those subnets; instead it would be more interesting to monitor the core backbone devices and WAN components. The topology maps or views created within **tkined** would reflect this monitoring physiology.

In fact, it is in the best interest of all parties for each individual or support group to deploy additional copies of **tkined** to address each specific need and monitoring requirement. Using multiple copies of **tkined** on the same system is one possible approach to this situation.

## Network Discovery

One powerful use of **tkined** is to dynamically discover the network devices within a single subnet, multiple subnets, or individual devices. One of the primary objectives for a network manager is to quickly and easily integrate the topology of the network into the tool. To begin the discovery process, select the *IP Discovery* sub-menu from the *Tools* main menu. A new menu called *IP: Discovery* will be displayed to the right of the tool menu. Figure 11.2 shows this new menu. It contains an option, *Discover IP Network*, that queries devices using ICMP and SNMP protocols in an attempt to learn the network topology. Selecting this option displays the sub-window shown in Figure 11.2.

![](img/f265c9d1f2610aca197c430cbfcd51f5_601_0.png)

**Figure 11.2** *Network discovery request window*.

The dialog window requires the user to enter a valid IP network address or group of addresses followed by spaces. As shown in Figure 11.2, the `10.0.2.0` network will be discovered when you click the discover button. Clicking this button also displays the window shown in Figure 11.3.

The window shows the progress of the discovery and the specific steps that were involved. The discover process shown in Figure 11.3 took only 66 seconds to complete and found seven nodes on the network. Given the number of nodes, the time required doesn't represent a problem. However, on a large network, the discovery process could take a lot longer. Note that tkined has detected those devices that support SNMP and those that do not. In the example, the application found six SNMP agents; this is correct for this network. We will see later on that tkined supports a significant number of functions based on SNMP and that accurate detection of SNMP devices is paramount. The other important information regarding the status window is the count of the number of objects that were created. Figure 11.3 indicates that a total of 16 objects were created. Since there were seven devices, each one has an individual icon, a network connection objects, and two networks.

![](img/f265c9d1f2610aca197c430cbfcd51f5_602_0.png)

Figure 11.3 Discovery status window.

Once the discovery is complete, tkined attempts to render the topology and devices with the networking topology panel. Figure 11.4 shows the results of probing the 10.0.2.0 network. Notice that the icons are a little unorganized and that the default icon is used for all the devices. You can customize the topology map and move the objects around to make the map a bit more visually appealing. Unfortunately, if you want to use more representative icons, you must assign them manually.

To move an icon around, simply select the object and then, pressing both mouse buttons, move the icon to the desired position and release the mouse. To help track your actions, the software displays a square box as a guide that moves as the mouse is moved. You can move all objects within the topology view around in this manner.
