
![](img/f265c9d1f2610aca197c430cbfcd51f5_563_0.png)

**Figure 9.31** *Terminal help mode.*

the help screen, **ntop** shows the supported keyboard commands. The **q** command is used to halt the operation of **ntop**. The **^c** command sequence will accomplish the same thing.

## Linux Control Panel

One of the important features of Linux is that many network administrative chores and tasks have been automated within a graphical user interface (GUI) configuration tool known as the control panel. This chapter provides an overview of the control panel provided with the standard release of Red Hat Linux. Those who are new to UNIX and do not want to edit special network configuration files or use shell commands will find the control panel a welcome aid. Although the control panel doesn’t provide the ability to control every aspect of networking, it does provide support for most of the important tasks.

### The Control Panel

The control panel provides a GUI to a number of network and system configuration tasks. You can use it to do the following:

- control the startup/shutdown of processes or services
- change the date and time
- configure/control printers
- configure network parameters
- configure modem parameters
- load/unload kernel modules
- configure additional system parameters

This tool can be invoked from the GNU Network Object Model Environment (GNOME) interface via the GUI main menu or the command line. To start it from the GUI, single-click on the GNOME *up triangle*, navigate to the *System* menu, then move to the right and select the Control Panel submenu. Figure 10.1 shows the main GNOME menu and *System* menu.

Alternatively, the user can access the control panel from the command line by typing the following:

```
# /usr/bin/control-panel
```

You should be *root* when running `control-panel` because it modifies standard UNIX configuration files that require administrator privileges. Despite the fact that `control-panel` contains several different icons and provides a significant amount of functionality, we are only interested in the areas that relate to networking. However, it is important that a general overview of the other functions be provided as well, with significant emphasis on the network elements as they pertain to network management. A basic overview of the `control-panel` services is presented first, followed by an in-depth review of the networking related tasks.

The network component of the `control-panel`, known as the `network configurator`, configures basic networking services. UNIX contains a large number of configuration files that store

important system and networking information in one or more specific formats. Luckily, this tool handles placing the data in the appropriate files and in the correct format. However, as a UNIX administrator, you will need to know where some of the files are located and their associated format because access to the control panel may not be possible or even practical in certain situations.

![](img/f265c9d1f2610aca197c430cbfcd51f5_566_0.png)

Figure 10.1 Accessing the control panel.

Starting the control panel displays the main window shown in Figure 10.2. The window contains a single menu, File, plus eight icons. The File menu contains two items: Change Orientation and Exit. The Exit option is self-explanatory, while the Change Orientation option acts as a toggle and will alter the way the icons are displayed. In Figure 10.1, the orientation of the icons is horizontal, and selecting the Change Orientation item will cause the icons to be displayed vertically instead. Selecting the option again will return to the previous orientation.

### Run-level Editor

The first icon accesses the run-level manager, which can control systems and/or network services that are activated on startup and services that are deactivated when the system is halted. Linux supports the standard *run-level* mechanism, which has its origins in the AT&T UNIX releases, where systems services are invoked and stopped based on different modes or run levels within the system. For instance, Linux usually operates in *run level 5*, which is known as multiuser mode. This is the primary operating mode when the system is booted and running normally. On other systems such as Solaris, *run level 2* is multiuser mode without NFS services, while *run level 3* is the normal multiuser mode. A user can determine which run level the system is operating in by using the **runlevel** Linux command. Alternatively, the **uname -a** command can be used.

![](img/f265c9d1f2610aca197c430cbfcd51f5_567_0.png)

### Changing Date and Time

The next icon changes the date and time of the system. A dialog window is presented that permits the user to select individual components (such as hour, minute, and second) of the current date/time so that they may be changed.

### Configure/Control Printers

This icon displays the System Print Manager, which allows you to define, control, and delete system printers. The tool supports the creation of local, remote via Line Printer Daemon (LPD), Windows 95/NT, and NetWare printers. Also, the user can control the printer background process and send test pages to the defined printers as a diagnostic debugging aid.

### Network Configuration

This icon represents the network configurator tool that controls basic networking services. This tool defines client domain name server properties, routing information, networking interfaces, and host information. The next section, “Using the Network Configurator,” provides more detailed information.

### Using Kernel Modules

The Linux system supports dynamic loading of system modules. Modules provide additional functionality or services to the system without having to build a new kernel or restart the system. This icon accesses the *kernel configurator* and permits the loading and unloading of modules on-the-fly. For instance, if the user wants to enable support for a TokenRing network interface, he can do so by loading the *tr* module, which is one of the available modules.

### Accessing Help

The *help* icon can be used to configure where the system will search for online documentation. This includes, for instance, the location of man (manual) pages.

### System Configuration

The final icon displays the Linux *configurator* tool, which configures and controls a large number of system and network parameters. The configurator software can also be started from the command line using the *linuxconf* command. An overview of the tool appears in the following section.

## Using the Network Configurator

As previously mentioned, the *network configurator* provides the ability to configure basic networking parameters. The following tasks can be accomplished using this software:

- configure DNS client configuration parameter
- maintain the hostname database
- configure, alter, or delete network interfaces
- configure network routing

Selecting the network configurator icon from the control panel displays the window shown in Figure 10.3.

![](img/f265c9d1f2610aca197c430cbfcd51f5_569_0.png)

Figure 10.3 network configurator window.

The top of the window contains a set of buttons that are used to navigate different views or categories. Each button represents a different category. A total of four buttons are provided, and clicking on any one of them will cause the main window to be redrawn with the associated view.

### Configuring DNS Parameters

The first button, Names, is the default view and is always displayed first whenever the configurator software is invoked. This view is used to define the hostname of the local system and the default domain name. Also, the user can configure the DNS servers to query and search metrics. In Figure 10.3, the name of the system, scrates, is contained in the Hostname field and DNS domain name, home.com, is listed in the Domain field. Changing the Hostname field will change the name of the system. If you want to list the name of the system while not using the control panel, use the hostname command.

The remaining three fields, Domain, Search for hostnames in additional domains, and Nameservers, control the operations of the DNS client software. The three name servers that are defined
