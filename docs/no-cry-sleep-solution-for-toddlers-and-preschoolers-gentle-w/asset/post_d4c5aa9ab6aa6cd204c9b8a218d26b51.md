
## Red Hat System Configuration

To make effective use of your Linux system, you must know how to configure certain features and services. Administrative operations such as adding users and installing software can now be performed with user-friendly system tools. This chapter discusses basic system administration operations that you need to get your system up and running, as well as to perform basic maintenance such as adding new users or printers.

There are four basic system configuration tasks that you most likely will have to deal with: user management, printer setup, display configuration, and software management. You can manage users, adding new ones, removing others, and updating user properties. Different kinds of printers, remote and local, can be set up for your system. For your video card and monitor, you can select the resolutions and color depths you want. You can also install new software packages and update or remove current ones. You were asked to perform all of these tasks during installation. In addition, there are other tools you can use to configure devices such as your keyboard, sound card, and mouse, as well as perform tasks such as setting the system date and time or selecting a language to use (see Table 4-1). You can make changes or additions easily using the administrative tools described in this chapter.

Configuration operations can be performed from a GUI interface such as GNOME or KDE, or they can be performed using a simple shell command line at which you type configuration commands. You can manually access system configuration files, editing them and making entries yourself. For example, the domain name server entries are kept in the /etc/resolv.conf file. You can edit this file and type in the addresses for the servers.

> Note Configuration tools are accessible only to the root user. You will first need to log in using root as your username and providing the root password you specified during installation.

## Red Hat Administrative Tools

On Red Hat, administration is handled by a set of separate specialized administrative tools developed and supported by Red Hat, such as those for user management and display configuration. Many of these are GUI-based and will work on any X Window System environment such as GNOME or KDE.

To access the GUI-based Red Hat tools, you log in as the root user to the GNOME desktop and open the Start Here window (see Figure 4-1) or select the main menu. System administrative tools are listed in the System Settings folder in the Start Here window, and on the System Settings menu listed in the main menu. Here you will find tools to set the time and date, manage users, configure printers, and update software. Users & Groups lets you create and modify users and groups. Printing lets you install and reconfigure printers. All tools provide very intuitive GUI interfaces that are easy to use. In the System Settings folder and menu, tools are identified by simple descriptive terms, whereas their actual names normally begin with the term redhat-config. For example, the printer configuration tool is listed as Printing, but its actual name is redhat-config-printer. You can separately invoke any tool by entering its name in a terminal window.

### TABLE 4-1
Red Hat System Configuration Tools

| Red Hat Administration Tools | Description |
|---|---|
| System Settings | Red Hat window and menu for accessing administrative tools |
| redhat-config-users | User and Group configuration tool |
| redhat-config-printer | Printer configuration tool |
| redhat-config-xfree86 | Red Hat display configuration tool (video card and monitor) |
| redhat-config-packages | Software management |
| redhat-config-rootpassword | Changes the root user password |
| redhat-config-keyboard | Changes the keyboard configuration |
| redhat-config-date | Changes system time and date |
| redhat-config-mouse | Configures your mouse |
| redhat-config-language | Selects a language to use |
| redhat-config-soundcard | Configures your sound card |

## Configuring Users

Currently, the easiest and most effective way to add new users on Red Hat is to use redhat-config-users, also known as the Red Hat User Manager. You can access it from the GNOME desktop's Start Here window's System Settings window. The redhat-config-users window will display panels for listing both users and groups (see Figure 4-2). A button bar will list various tasks you can perform, including creating new users or groups, editing current ones (Properties), or deleting a selected user or group.

To create a new user, click the New button. This opens a window with entries for the username, password, and login shell, along with options to create a home directory and a new group for that user. Once you have created a user, you can edit its properties to add or change features. Select the user's entry and click Properties. This displays a window with
