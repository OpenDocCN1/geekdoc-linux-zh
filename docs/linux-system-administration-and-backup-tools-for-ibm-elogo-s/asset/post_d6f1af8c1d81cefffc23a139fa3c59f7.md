
Linux System Administrator’s Guide by Lars Wirzenius and Joanna Oja, Linux Administration Made Easy by Steve Frampton. You can find the LDP home page at http://www.linuxdoc.org or http://www.sunsite.unc.edu/LDP/

The system administration tools available for each Linux distribution are listed in Table 1:

Table 1. Distributions and their administration tools

| Distribution | Administration Tool |
|---|---|
| Caldera OpenLinux | Caldera Open Administration System (COAS) |
| Red Hat Linux | Linuxconf |
| SuSE Linux | YaST (textmode), YaST2 (GUI) |
| TurboLinux | turboXXXcfg (XXX: apache, fs, fpt, net, print, sound, time, user) turbopkg turboservice |

## 1.1.1 Caldera Open Administration System (COAS)

COAS helps to improve the users administer their Linux systems. The administration tools include the following:

- Multiple user interfaces for administration
- Modular administration tools
- Flexible, powerful administration tools
- Easy-to-use administration tools

The administration system will provide multiple user interfaces for each administration tool. Those interfaces are command line, curses, X, and Java. For more information on COAS, visit the following Web site:

http://www.coas.org/index.html

## 1.1.2 Red Hat Linux

Linuxconf is a sophisticated administration system used by the Red Hat operating system. In many ways, Linuxconf is different from other administration schemes found on UNIX operating systems and most other systems.

Linuxconf is a configuration utility (a user interface to configuration tasks) and an activator. Linuxconf is involved in the operation of your Linux server or workstation. Mostly, it has features to warrant that the what you have configured is performing effectively. The different interfaces include the following:

- A text-based interface
Linuxconf takes control pretty early at boot time when not much is enabled, especially not the X-Windows system. A text-based interface is required. This interface works on the console, on a terminal, using Telnet session, or logged in using a simple modem.

- A Web interface
Linuxconf may be operated with your favorite Web browser. Features of a Web browser such as bookmarks, multiple pages, and hotlinks make management a dream. You don't have to install an HTTP server itself and is started from the inetd server.

- A graphical interface
Linuxconf has two GUI front ends. One is done in Java and is expected to operate stand-alone or from a browser. The other is with the xxWT toolkit and is already operational. Linuxconf is expected to evolve with some monitoring and diagnostic facilities.

- A command line interface
The command line interface is rarely used, and in some operating systems it does not exist. During the execution of special tasks, nothing can beat a script. A good example is the DNS management available in Linuxconf.

## 1.1.3 SuSE Linux

The system administration tool used in Su's Linux is YaST, the acronym for Yet another Setup Tool. It is the program used to configure and administer the operating system. YaST gives you the ability to install and remove system and user software and perform basic system administration tasks. For a list of system administration activities, YaST allows you to perform the following:

- Integrate hardware into the system
- Kernel and boot configuration
- Networking configuration
- Configure the Live Filesystem CD-ROM
- Login configuration
- Set up usewm (the Windows Manager)
- User administration
- Group administration
- Create backups
- System Security Settings
- Configure XFree86
- Modify the YaST configuration file

## 1.1.4 TurboLinux

TurboLinux's easy-to-use TurboTools speed configuration of networks, printers, X-Windows, page updates, user accounts, and a wide variety of other system settings that ease administration once they are up and running.

These tools are featured in Table 1.

This chapter will give you an overview of how to perform the most common administrative tasks on a Caldera OpenLinux Server 2.3 operating system. Most of these tasks can be done with the Caldera Open Administration System (COAS), Caldera's OpenLinux graphical-oriented configuration and administration tool. However, you may still perform these tasks using the command-line tools.

> Stop
> Be careful when you are editing configuration files on your own. If you edit configuration files with an editor, make sure to maintain the format of the file. If you change the format of a configuration file, COAS may not be able to understand the configuration information and you cannot use COAS for future configuration.

## 2.1 Log in to the system

Before you can use any Linux system you need to log in to the system. Whenever you start Caldera OpenLinux, you will see a login window similar to Figure 2.

### Caldera OpenLinux [x220]

| | | |
|---|---|---|
| col | root | |
| Login: | | |
| Password: | | |
| Desktop Environment | | |
| Session Type: kde | Go | Cancel | Shutdown... |

Figure 2. Login window

If you wish to use a text-based user interface, you can press Ctrl-Alt-Fx, where x is the number from 1 to 6, to switch to a text console. For example to switch to console 1, you need to press Ctrl-Alt-F1, and you will see a window similar to Figure 3.

```
Caldera Openlinux server
Version 2.3
Copyright 1996-1999 Caldera Systems, Inc.

x220.first.itso.com login:
```

Figure 3. Text-based user interface

If you want to switch back to the graphical interface press Alt-F8. This means that you are switching to the console number 8. Caldera OpenLinux uses this console for the graphical user interface. To start working with Caldera OpenLinux, you need to log on with either a graphical or a text-based interface. To start the graphical user interface type, in the user name and password in the window shown in Figure 2, and click Go! You will see a window similar to Figure 4.

![](img/4e6a76e57a4105be55d8a1cc0750b023_20_0.png)

Figure 4. Window Manager

## 2.2 Using the Window Manager

Once you are logged into the system through the graphical environment you will see a window similar to Figure 4, which is controlled by the Window Manager. Caldera OpenLinux uses the KDE Window Manager. You can get more information about KDE on:

```
http://www.kde.org
```

At the bottom of the window you can see the toolbar that is used for accessing all functions. It has pull-down menus, icons and buttons. You can use them for accessing the features of the operating system and applications.

> Note
> We recommend that you use than 8bpp color definitions for your XFree86 server setup; otherwise, you will have problems with missing colors when you open more programs.

In the following sections we will describe how to use some basic tools in the graphical environment and especially how to customize your Caldera OpenLinux system using COAS.

## 2.3 Getting the X-Windows terminal window

In order to run commands from the command line when you have the GUI-based window in front of you, you need to create a terminal window. You can do this by clicking the icon representing the terminal window, circled in Figure 5.

![](img/4e6a76e57a4105be55d8a1cc0750b023_21_0.png)

After the terminal window is started, you will see a window similar to Figure 6.

![](img/4e6a76e57a4105be55d8a1cc0750b023_22_0.png)

In this terminal window you can access the system from a command-line prompt as in a text-based interface. The command line prompt gives you more flexibility than menus, but you can do most of the basic things from the menu system. It is a matter of personal choice.

## 2.4 Accessing COAS - Caldera Open Administration System

All the administration tasks in Caldera OpenLinux are performed through the use of COAS. You can access the COAS tools by clicking the COAS icon on the KDE toolbar, circled in Figure 7.
