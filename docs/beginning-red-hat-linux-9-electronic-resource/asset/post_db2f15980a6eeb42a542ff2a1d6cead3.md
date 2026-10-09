
Note that Xchat cannot connect to an IRC server through a firewall, at the current time.

## Instant Messaging

Instant messaging is fast emerging as the latest Internet application to connect people together. Most of today's instant messaging applications allow users to chat one-on-one or in a group in real time as well as allow them to share files. Unfortunately, all of the instant messaging applications are not based on a common protocol, but on proprietary protocols that do not interact with each other. What this means is that a user on AIM (AOL's instant messaging solution) cannot seamlessly connect with a user on a different messaging network, say Yahoo! Messenger.

This is where Gaim comes in. Gaim is an instant messaging client that supports multiple protocols and also allows a user to be logged on to different networks with different account names simultaneously. In fact Gaim can even connect to IRC servers. Pretty clever, eh? Gaim can be invoked from Main Menu | Internet | Instant Messenger:

![](img/b852150740856958b10aff9e8c9d2adc_129_0.png)

Before we can use Gaim, we need to set up a couple of things. For Gaim to work with a certain instant messaging network, it needs to have a plug-in for that network loaded. This is a one-time task that can be accomplished by clicking on the Plugins button followed by the Load button and choosing the appropriate plug-in, say libyahoo.so for Yahoo! Messenger or libicq.so for ICQ. Once the plug-ins are set up, we need to fill in account information for each of the networks that we intend to connect to. Account information can be entered by clicking the Accounts button followed by the Add button. The official Gaim web site is http://gaim.sourceforge.net. Chapter 5 discusses Gaim configuration in detail, so we'll leave it at that for the time being.

## Summary

In this chapter we explored the issues associated with connecting our Red Hat Linux 9 installation to the Internet. Hopefully you should now have a working Internet connection, and be able to surf web pages, check your mail, transfer files by FTP, and use IRC with confidence.

In brief, we have:

- Investigated the use of various wizards such as the Internet Configuration Wizard, and Network Configuration Tool to configure devices and connections in the context of different connection requirements.
- Learned how to create logical devices and profiles in order to better manage our resources.
- Explored some of the important Internet access software available with the Red Hat Linux installation.

## Installing Software

As you would expect from a Linux distribution, Red Hat Linux 9 comes bundled with a vast array of software applications for your use. Major applications such as the Open Office productivity suite and Ximian Evolution e-mail client are installed as part of the installation, but there are a great number of other applications that are not. This software may be stored on a CD, on the Internet, or somewhere else entirely. In this chapter we'll be looking at how you can get hold of it, and install it on your system.

During the course of the chapter, we'll be looking at the following areas:

- The RPM and its advantages
- The RPM Package Management Tool
- RPM console commands
- RPM security features
- A few examples of RPM package installation

In the course of this chapter, we will be using the terms RPM Package Management Tool, Package Management Tool, and Red Hat Package Manager interchangeably to refer to Package Management GUI provided by Red Hat Linux 9. We will also use the term `rpm` to refer to the RPM command line interface.

### What Is RPM?

The RPM package manager is an open source packaging system distributed under the GNU GPL. It runs on most Linux distributions and makes it easy for you to install, uninstall, and upgrade the software on your machine. RPM files can be easily recognized by their `.rpm` file extension and the ‘package’ icon that appears in your navigation window:

![](img/b852150740856958b10aff9e8c9d2adc_133_0.png)

> **More information about the background of RPM can be found at:**
> http://www.redhat.com and http://www.rpm.org/max-rpm/

The benefits of using RPM can be summarized as follows:

- **Simplicity**: RPM simplifies the task of installing software. RPM packages can be managed using the RPM GUI interface, or via the command line.
- **Upgradeability**: RPM gives us the flexibility to upgrade existing packages without having to reinstall them. You can freshen and upgrade parts, or all, of your system automatically, with the minimum of fuss.
- **Manageability**: RPM makes it easy to manage software packages. It maintains a database of all the packages installed on the system, so you know exactly what you've got installed, what version it is, and when it was added.
- **Package queries**: RPM provides options to query packages for more details in different ways. You can search the package installed on the system. You can also find out what package a file belongs to. It helps in keeping track of all packages installed on your system.
- **Uninstalling**: RPM makes it easy to uninstall packages. This helps us to keep the system clean.
- **System verification**: RPM also provides a feature to verify packages. In case of any doubt about file deletion, packages can be verified against the original package information using RPM. This checks all the files on the system with the package information and verifies that the files on the system are the same as those installed from the package originally.
- **Security**: RPM provides commands for the user to check the integrity of packages. Packages can be checked using md5sum to verify that they have not been corrupted or tampered with since they were created. RPM also provides functionality to verify a package provider's identity and package integrity using gnupg (very handy if you're downloading sensitive material from the Internet, as you want to be sure that you're installing what you think you're installing).

Now that we've an understanding of what RPM is, and what it can be used for, let's move on to consider how it works. In point of fact, RPM can be used in two different, yet complementary ways – from the desktop, using the GUI interface, and from the command line. We'll look at the GUI first, because it's simpler, and will give us a good grounding from which to proceed.

### The RPM Package Management (GUI) Tool

Red Hat has added a lot of new features to its latest operating systems to make them easier to manage. One of these new features is the Package Management Tool. This tool is a graphical user interface (GUI) designed for the management of package installation and removal. The GUI allows us to add and remove packages at the click of a mouse.

> The package management tool, as accessed from the Main Menu, is able to manage only packages provided as part of a Red Hat Linux 9 installation. To install other RPMs from disk, or download, you need to navigate to the RPM in question and double-click on the file. This will load the package management tool, and skip you straight to the ‘Install’ screen, bypassing the system-specific install options.

### Starting the RPM Package Management Tool

There are two ways to start RPM. To do it from the Main Menu, select Main Menu | System Settings | Add/Remove Applications. Alternatively, from the command line you can type the following command:

```bash
$ redhat-config-packages
```

Either way, if you're logged in with privileges other than root privileges, you'll be prompted to enter the root password.

Once you've identified yourself as an administrator, you'll see the following window:

![](img/b852150740856958b10aff9e8c9d2adc_135_0.png)

### Package Management Tool Functions

Let's take a closer look at the GUI:

![](img/b852150740856958b10aff9e8c9d2adc_135_1.png)

- Package Category
- Package Group
- Details link (to open the package details window)
- Number of packages installed (out of total packages available in group)
- Summary of total disk space required to install packages
- Quit button (to close the interface)
- Update button (to start the installation)
