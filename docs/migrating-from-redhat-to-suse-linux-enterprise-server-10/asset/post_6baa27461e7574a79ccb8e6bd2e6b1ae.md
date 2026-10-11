
The YaST dialog appears.

**Figure 2-2**

![](img/63e88022bf135307e3eac051ad238b5b_80_0.png)

You control the ncurses interface with the keyboard. To start the ncurses interface of YaST, you can start a terminal emulation from your GNOME desktop by selecting **Gnome Terminal** from the main menu (application group: **System**).

Enter **su -** to get root permissions. After entering the root password, start YaST by entering **yast**.

![](img/63e88022bf135307e3eac051ad238b5b_81_0.png)

Press **Tab** to move from one box to another or to the text buttons. To go back to the previous box, press **Shift+Tab**. Use the arrow keys to navigate within the box. Mark highlighted menu items by pressing the **Spacebar**.

To select a menu item, press **Enter**. You can often press **Alt** and the highlighted letter to access an item directly.

Except for the controls and the appearance, the graphical mode and the text mode of YaST are identical.

You can list the available YaST modules with the command **yast -l** or **yast --list**. To start an individual module, specify its name. For example, you can enter the following to start the software installation module:

```
yast sw_single
```

You can enter the software module name with the command **yast** or **yast2**, as in the following:

- **yast** sw_single (text mode)
- **yast2** sw_single (graphical mode)

> To install a software package you can also enter **yast -i *package.rpm***. The package is installed directly without any dialogs.

To display a list of YaST options, enter one of the following:

- **yast --help**
- **yast -h**

The main dialog of YaST is called the *YaST Control Center*.

From here you can select a category on the left (such as Software or System) and a module on the right (such as Online Update) to configure and manage your system.

When you finish making changes with a YaST module, YaST uses back end services such as SuSEconfig.

### The Role of SuSEconfig

You can consider YaST as a front end to various other programs, such as a front end to RPM (RPM Package Manager) software management, a front end to user management, or a front end to various configuration files of different services (like a mail or web server).

Usually YaST writes your configuration changes directly into the final configuration file. In rare cases there is an additional intermediate step, where the information you enter is first written to a file in the directory */etc/sysconfig/* before it is written into the final configuration file.

This is where the program **SuSEconfig** becomes important.

SuSEconfig is a tool used in SUSE Linux Enterprise Server to configure the system according to the variables that are set in the various files in *`/etc/sysconfig/`* and its subdirectories.

These files contain variables such as `SYSLOGD_PARAMS=""` in *`/etc/sysconfig/syslog`* and `SMTPD_LISTEN_REMOTE="no"` in *`/etc/sysconfig/mail`*.

Some of these variables are used directly (such as in some start scripts). For example, if `SYSLOGD_PARAMS` is set to “-r”, the daemon that logs system messages is directed to listen on port 514 for system messages from other hosts.

Other variables are used to modify other files. For example, if `SMTPD_LISTEN_REMOTE` is set to “yes,” the variable `INET_INTERFACES` in *`/etc/postfix/main.cf`* is set to “all” by the script *`/sbin/SuSEconfig`* and the scripts in *`/sbin/conf.d`*.

SuSEconfig acts as a back end for YaST and activates the configuration changes you make when using a YaST module.

If you modify files in *`/etc/sysconfig/`* using an editor, all you might need to do is restart a service for the change to take place. However, you might also need to run SuSEconfig.

For this reason, we recommend running SuSEconfig after manually editing files in *`/etc/sysconfig/`*.

SuSEconfig uses the subsystem specific scripts in *`/sbin/conf.d/`* to configure the various subsystems. For example the variables in *`/etc/sysconfig/postfix`* are evaluated by the script *`/sbin/conf.d/SuSEconfig.postfix`*.

## Exercise 2-1 Get to Know YaST

In this exercise, you learn how to use the different user interfaces of YaST and how to start some YaST modules.

You will find this exercise in the workbook.

(End of Exercise)

## **Objective 2**
**YaST Software Management**

Software management has different aspects:

- Manage Installation Sources
- Install Software Packages
- Apply Security Updates

### Manage Installation Sources

The software installation dialog lists only the packages that are on the current installation media.

If you want to add more installation sources, select **Software > Installation Source** from the YaST Control Center. The following appears:

Figure 2-4

![](img/63e88022bf135307e3eac051ad238b5b_85_0.png)

HARDCOPY PERMITTED–NO DISTRIBUTION ALLOWED

To add a new source, select the **Add** drop-down list and select the *type* of installation source. Depending on the type of source, you might have to provide additional information (such as the IP address of an installation server).

To edit the configuration of an existing installation source, select the source in the list and select **Edit**.

If you want to disable an installation source temporarily, select the source in the list and select **Enable or Disable**.

To remove an installation source permanently, select the source from the list and select **Delete**.

YaST uses the first installation source in the list that has the software package you want to install. To change the order of a source in the list, select the source and **Up** or **Down**.

### **Install Software Packages**

After performing a standard SUSE Linux Enterprise Server 10 installation, you will often need to install additional software. To do this, start the YaST module **Software > Software Management**.

The installed packages and the packages that are available on the installation media are analyzed and dependencies between packages are checked.

After this checking, the following dialog for searching packages appears:

![](img/63e88022bf135307e3eac051ad238b5b_87_0.png)

![](img/63e88022bf135307e3eac051ad238b5b_87_1.png)

To help you find the software you want to install, you can choose from different filters listed in the drop-down list in the top left corner of the window labeled Filter. The following filters are available:

- **Patterns.** Displays all software that is available on the known installation media. It is grouped in predefined sets of packages that logically belong together.
- **Package Groups.** Displays all software that is available on the known installation media. It is grouped by category.
- **Languages.** Displays all language related files (e.g., spell checker, help)
- **Installation Sources.** Lists all registered installation sources and displays the available packages of this source.
- **Search**. Lets you enter a search term and where you want YaST to search for the software package.
- **Installation Summary**. Displays all the packages with a marked status.

To find a package, select the Search filter, enter the package name or parts of the package name or some keywords in the Search field; then select **Search**.

The matched packages are listed in the right area. The installation state is shown by a small symbol in front of the package name. The most commonly displayed symbols include the following:

**Figure 2-6**

| Symbol | Description |
|---|---|
| Do not install | This package is not installed and it will not be installed |
| ☑ Install | This package will be installed. It is not installed yet |
| ☑ Keep | This package is already installed. Leave it untouched |
| ↻ Update | This package is already installed. Update it or reinstall it (if the versions are the same). |
| 🗑 Delete | This package is already installed. Delete it |
| ⚠ Taboo | This package is not installed and should not be installed under any circumstances, especially not because of unresolved dependencies that other packages might have or get. Packages set to "taboo" are treated as if they did not exist on any installation media. |
| 🔒 Protected | This package is installed and should not be modified, especially not because of unresolved dependencies that other packages might have or get. Use this status for third-party packages that should not be overwritten by newer versions that may come with the distribution. |
| ☑ Autoinstall | This package will be installed automatically because some other package needs it **Hint**: You may have to use "taboo" to get rid of such a package. |

To view a list of all possible symbols, select **Help > Symbols**.
