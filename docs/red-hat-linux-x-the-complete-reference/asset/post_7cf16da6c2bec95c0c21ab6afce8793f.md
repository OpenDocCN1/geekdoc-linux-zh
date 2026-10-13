
## Note

If, while running Linux, you wish to open the DVD-ROM included with this book, you can insert it in your DVD-ROM drive. If a file manager window does not open automatically

![](img/32a48d8db4c23e6e2eb70d1e5034c976_48_0.png)

## ABC Amber CHM Converter Trial version

Please register to remove this banner.

http://www.processestext.com/abchm.html

## Chapter 3: Interface Basics

### Overview

Using Linux has become an almost intuitive process, with easy-to-use interfaces like graphical logins and graphical user interfaces (GUIs) like GNOME and KDE. Even the standard Linux command line interface has become more user-friendly with editable commands, history lists, and cursor-based tools. To start using Linux, you have to know how to access your Linux system and, once you are on the system, how to execute commands and run applications. Access is supported through either the default graphical login or a command line login. For the graphical login, a simple window appears with menus for selecting login options and text boxes for entering your username and password. Once you access your system, you can then interact with it using either a command line interface or a graphical user interface (GUI). With GUI interfaces like GNOME and KDE, you can use windows, menus, and icons to interact with your system. Red Hat has integrated the look and feel of both to provide one standard GUI interface called Bluecurve, making their use less confusing.

Linux is noted for providing easy access to extensive help documentation. It's easy to obtain information quickly about any Linux command and utility while logged in to the system. You can access an online manual that describes each command or obtain help that provides more detailed explanations of different Linux features. A complete set of manuals provided by the Linux Documentation Project is on your system and available for you to browse through or print. Both the GNOME and KDE desktops provide help systems that give you easy access to desktop, system, and application help files.

Tip
The Red Hat Linux Getting Started Guide provides a detailed tutorial on using your Red Hat Linux system for the first time. Check the Reference, Customization, and Security guides for specialized tasks.

### User Accounts

You never directly access a Linux system. Instead, Linux sets up an interface called a *shell* through which you can interact with it. Linux is a multi-user system that can support several user shells at once, accommodating several users simultaneously, each connected through their own terminal or from a remote system.

User access to the system is provided through *accounts*. Unix, upon which Linux is based, was first used on large minicomputers and mainframes that could accommodate hundreds of users at the same time. Using one of many terminals connected to the computer, users could log in to the Unix system using their usernames and passwords. To gain access to the system, you needed to have a user account set up for you. A system administrator created the account, assigning a username and password for it. You then used your account to log in and use the system.

You can, in fact, create other new user accounts using special system administration tools. These tools become available to you when you log in as the root user. The *root user* is a special user account reserved for system administration tasks, such as creating users and installing new software. Basic system administration operations are discussed briefly in Chapters 4 and 5, but they are discussed in more detail in Chapters 27-33.

### Accessing Your Linux System

To access and use your Linux system, you must carefully follow required startup and shutdown procedures. You do not simply turn off your computer. If you have installed the boot loader GRUB, when you turn on or reset your computer, the boot loader first decides what operating system to load and run. GRUB will display a menu of operating systems to choose.

If, instead, you wait a moment or press the ENTER key, the boot loader loads the default operating system. If a Windows system is listed, you can choose to start that instead.

You can think of your Linux operating system as operating on two different levels, one running on top of the other. The first level is when you start your Linux system, and where the system loads and runs. It has control of your computer and all its peripherals. You still are not able to interact with it, however. After Linux starts, it displays a login screen, waiting for a user to log in to the system and start using it. You cannot gain access to Linux unless you log in first.

You can think of logging in and using Linux as the next level. Now you can issue commands instructing Linux to perform tasks. You can use utilities and programs such as editors or compilers, or even games. Depending on a choice you made during installation, however, you may be interacting with the system using either a simple command line interface or the desktop directly. There are both command line login prompts and graphical login windows. Red Hat will use a graphical interface by default, presenting you with a graphical login window at which you enter your username and password. If you choose not to use the graphical interface, you are presented with a simple command line prompt to enter your username.

### The Display Manager: GDM

With the graphical login, your GUI interface starts up immediately and displays a login window with boxes for a username and password. When you enter your username and password and then press ENTER, your default GUI starts up. On Red Hat, this is GNOME by default.

For Red Hat, graphical logins are handled by the GNOME Display Manager (GDM). The GDM manages the login interface along with authenticating a user password and username, and then starting up a selected desktop. If problems ever occur using the GUI interface, you can force an exit of the GUI with the CTRL-ALT-BACKSPACE keys, returning to the Login screen (or the command line if you started your GUI from there). Also, from the GDM, you can shift to the command line interface with the CTRL-ALT-F1 keys, and then shift back to the GUI with the CTRL-ALT-F7 keys.

When the GDM starts up, it shows a login window with a box for login. Four pop-up menus are located at the bottom of the screen, labeled Session, Language, Shutdown, and Restart. To log in, enter your username in the box labeled Username and press ENTER. You are prompted to enter your password. Do so, and press ENTER. By default, the GNOME desktop is then started up.

When you log out from the desktop, you return to the GDM login window. To shut down your Linux system, click the System menu to display the entry Reboot or Shutdown. Select Shutdown to shut down your system. Alternatively, you can also shut down when you log out from GNOME. GNOME will display a logout screen with the options Logout, Shutdown, or Reboot. Logout is the default, but selecting Shutdown will also shut down your system. Selecting Reboot will shut down and restart your system. (You can also open a terminal window and enter the shutdown, halt, or reboot command as described in the next section: halt will log out and shut down your system.)

From the Session menu, you can select the desktop or window manager you want to start up. Here you can select KDE to start up the K Desktop, for example, instead of GNOME. On Red Hat, both KDE and GNOME will use an interface with a Bluecurve look and feel, appearing much the same. The Language menu lists a variety of different languages that Linux supports. Choose one to change the language interface.

### Accessing Linux from the Command Line Interface

For the command line interface, you are initially given a login prompt. The system is now running and waiting for a user to log in and use it. You can enter your username and password to use the system. The login prompt is preceded by the hostname you gave your system. In this example, the hostname is turtle. When you finish using Linux, you first log out. Linux then displays exactly the same login prompt, waiting for you or another user to log in again. This is the equivalent of the login window provided by the GDM. You can then log into another account.

```
Fedora Core release 1
Kernel 2.4.22-1 on an i686
```

```
turtle login:
```

### Logging In and Out

Once you log in to an account, you can enter and execute commands. Logging in to your Linux account involves two steps: entering your username and then entering your password. Type in the username for your user account. If you make a mistake, you can erase characters with the BACKSPACE key. In the next example, the user enters the username dylanp and is then prompted to enter the password:

```
Fedora Core release 1
Kernel 2.4.22-1 on an i686
```

```
turtle login: dylanp
Password:
```

When you type in your password, it does not appear on the screen. This is to protect your password from being seen by others. If you enter either the username or the password incorrectly, the system will respond with the error message "Login incorrect" and will ask for your username again, starting the login process over. You can then reenter your username and password.

Once you enter your username and password correctly, you are logged in to the system. Your command line prompt is displayed, waiting for you to enter a command. Notice the command line prompt is a dollar sign ($), not a number sign (#). The $ is the prompt for regular users, whereas the # is the prompt solely for the root user. In this version of Linux, your prompt is preceded by the hostname and the directory you are in. Both are bounded by a set of brackets.

```
[turtle /home/richlp]$
```

To end your session, issue the logout or exit command. This returns you to the login prompt, and Linux waits for another user to log in.

```
[turtle /home/richlp]$ logout
```

### Shutting Down Linux

If you want to turn off your computer, you must first shut down Linux. If you don't shut down Linux, you could require Linux to perform a lengthy systems check when it starts up again. You shut down your system in one of two ways. First, you log in to an account and then enter the halt command. This command will log you out and shut down the system.

```
$ halt
```

Alternatively, you can use the shutdown command with the -h option. With the -r option, it shuts down the system and then reboots it. In the next example, the system is shut down after five minutes. To shut down the system immediately, you can use +0 or the word now (see Chapter 28 for more details).

```
# shutdown -h now
```
