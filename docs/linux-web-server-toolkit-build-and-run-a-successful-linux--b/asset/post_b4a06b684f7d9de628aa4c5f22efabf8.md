
# Linux Web Server Toolkit

![](img/e01f1106dd2902613fa07890c8baa7e6_117_0.png)

Figure 4-5: A File Information dialog box lets you view the owner of the file and access privileges.

You can select a field to show the owner or access permissions for the file. When you are viewing the owner and group for the file, you can select from the list of users and groups on the system to assign the owner and group.

When you are looking at the access permissions, you can check and uncheck boxes to set the permissions for the owner, group, and other users. Avoid setting the Set User ID or Set Group ID unless you feel confident in what you're doing.

There is also a default mask that defines what permissions are assigned automatically to any files that are created by the Desktop. You can see this mask in the Preferences window under Creation Preferences.

# Using Layouts

The open Directory windows, icons on the Desktop, and arrangement of the Icon Bar are all part of a Desktop layout. You can save the complete layout under a name that you select, return to that layout at any time.

This is useful when you do several kinds of tasks on your Linux system. For example, if you sometimes do system administration tasks and you like to have a particular set of tools and options available, you can create an Admin layout. If you also do development work that requires a different set of tools, you can create a second layout.

# Chapter 4: Internet and UNIX Technologies

These layouts will appear under the Layouts menu on the Desktop. You can quickly select one of the layouts you created (or one of the default layouts that come with the system) in order to switch to the environment you want to use with all the appropriate tools immediately available.

# Preference Settings

From the Desktop, you can set many of the system settings that affect your work. Some of these settings apply only when you are running the Desktop, and many are related to the graphical tools. No tools are provided with the Desktop for configuring Internet access, PPP, routing, users and groups, or similar system administration. For these, use menu-driven LISA utility or the command-line utilities described earlier.

# ENVIRONMENT VARIABLES

From the Run menu of the Desktop, choose the Environment Variables item to open a dialog box where all environment variables are listed with their names and values.

Environment variables are named values that are available to all programs run from your current session or programs that run from your current session. They provide information about your hardware or software environment to the programs. For example, your standard login process defines an environment called HOME that contains the path to your home directory. Any program you run after log in can request the value of HOME and know where your home directory is located.

In addition to the standard environment variable that the operating system uses, many applications use environment variables to control settings such as where they place documents, where program files are located, or where the default network connections should be.

The Environment Variables window, shown in Figure 4-6, provides a place where you can examine these variables and all that are needed for your system.

![](img/e01f1106dd2902613fa07890c8baa7e6_118_0.png)

Figure 4-6: The Environment Variable Editing window lets you examine and add variables.

Be aware, however, that environment variables apply only within the scope in which they are created. The simple explanation of this is that if you add a new variable using the Desktop, then exit the Desktop and start a program, the variable that you created will not be available to the program. Only programs started from within the Desktop (by double-clicking on an icon), for example will see the new variable that you created.

# OTHER PREFERENCE SETTINGS

You can open the main Preferences window by selecting Preferences from the Windows menu on the Desktop. From the Preferences window, double-click on the icon for the type of preferences that you want to see or change. A separate window appears for each group of settings.

For example, to set the colors of the Desktop, choose the Colors icon. You can select background, foreground, or shading colors for the Desktop windows. Or, to set the default text editor used when you double-click on a text file, choose the Execution preferences and look at the Default editor. The default editor will be the CRISP- editor that comes with Linux. If you are already a UNIX fan, you can change to the vi or emacs editors by changing this line. The preferences you can set are too numerous to list here, so be sure to explore this feature to get a full understanding of how you can customize your system.

# Summary

This chapter defined some key technologies of the Internet and Linux that will help you as you set up your Linux Web server. It also provided some commands for managing users and using the graphical interface to complete tasks on your Linux system.

In this chapter you've learned the following:

- The Internet is based completely on UNIX standards; UNIX standards are a part of Linux. This means all other types of systems that want to connect to the Internet have to add UNIX protocols to their base systems.
- The Web is one of many protocols that are used to transfer data across the Internet. The Web is the most talked-about right now, but each protocol is designed for specific uses.
- Linux commands are like UNIX commands, and are entered from a shell prompt, similar to the DOS C:> prompt but with much greater capabilities. As a multiuser, multitasking system, Linux lets you create and manage user and group accounts, and the access permissions granted to each user and group to use system resources.

# Chapter 4: Internet and UNIX Technologies

- The X Window System is the standard graphical system for UNIX and Linux. It can be a challenge to configure, but provides networking features and flexibility not found in any other operating system. The Desktop interface included with the CD-ROM in this book provides an easy-to-use interface for most of the configuration tasks described in this chapter.

In Chapter 5, you'll learn how to install OpenLinux Lite from the CD-ROM included with this book. Chapter 5 covers preparing your computer, completing the installation, and configuring the system after installation. In the rest of Part II, I'll describe installing Web server software and getting everything set up to start serving Web pages on the Internet.

# Part II:

# Installing Your Web Server

Now that you've finished making all the important decisions for your Web site, it's time to carry out your plan. The next three chapters help you install your Linux system, connect to the Internet, and get your Web server up and running.

# Chapter 5

# Installing Linux

THIS CHAPTER DESCRIBES HOW to install Linux on your computer. It is specifically targeted to the CD-ROM included with this book, but a lot of the information about hardware and Linux in general will apply to other Linux distributions as well. Topics covered in this chapter include the following:

- Reviewing the system requirements
- Preparing your hard disk for Linux
- Installing OpenLinux Lite
- Setting up the graphical system (the X Window System)
- Using your network connection

# Evaluating Your Hardware Requirements

Linux supports an amazing variety of hardware. The fact that source code is available enables developers to create drivers and other software to support new hardware and peripherals as they come out. It's likely that whatever hardware is supported by Linux. Online documents provide up-to-date information about the latest hardware support added to Linux.

Unfortunately, when hardware companies create a new product, they often don't worry about compatibility with previous models. Part of that may be because they often provide a driver for Windows software, but the rest of the computer world might be left wondering how to use the power of new models and features. The Linux model of open source code solves cases in most by relying on the people who use the hardware to provide the driver software.

This section describes the recommended hardware for a Web server and also tells how to install and use that hardware on your Linux system. Hardware modules are also discussed.
