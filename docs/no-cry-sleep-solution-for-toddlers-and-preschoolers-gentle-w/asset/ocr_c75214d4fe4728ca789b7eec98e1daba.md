User access to the system is provided through accounts. Unix, upon which Linux is based, was first used on large minicomputers and mainframes that could accommodate hundreds of users at the same time. Using one of many terminals connected to the computer, users could log in to the Unix system using their usernames and passwords. To gain access to the system, you needed to have a user account set up for you. A system administrator created the account, assigning a username and password for it. You then used your account to log in and use the system.

You can, in fact, create other new user accounts using special system administration tools. These tools become available to you when you log in as the root user. The root user is a special user account reserved for system administration tasks, such as creating users and installing new software. Basic system administration operations are discussed briefly in Chapters 4 and 5, but they are discussed in more detail in Chapters 27-33.

# Accessing Your Linux System

To access and use your Linux system, you must carefully follow required startup and shutdown procedures. You do not simply turn off your computer. If you have installed the boot loader GRUB, when you turn on or reset your computer, the boot loader first decides what operating system to load and run. GRUB will display a menu of operating systems to choose.

If, instead, you wait a moment or press the ENTER key, the boot loader loads the default operating system. If a Windows system is listed, you can choose to start that instead.

You can think of your Linux operating system as operating on two different levels, one running on top of the other. The first level is when you start your Linux system, and where the system loads and runs. It has control of your computer and all its peripherals. You still are not able to interact with it, however. After Linux starts, it displays a login screen, waiting for a user to log in to the system and start using it. You cannot gain access to Linux unless you log in first.

You can think of logging in and using Linux as the next level. Now you can issue commands instructing Linux to perform tasks. You can use utilities and programs such as editors or compilers, or even games. Depending on a choice you made during installation, however, you may be interacting with the system using either a simple command line interface or the desktop directly. There are both command line login prompts and graphical login windows. Red Hat will use a graphical interface by default, presenting you with a graphical login window at which you enter your username and password. If you choose not to use the graphical interface, you are presented with a simple command line prompt to enter your username.

# The Display Manager: GDM

With the graphical login, your GUI interface starts up immediately and displays a login window with boxes for a username and password. When you enter your username and password and then press ENTER, your default GUI starts up. On Red Hat, this is GNOME by default.

For Red Hat, graphical logins are handled by the GNOME Display Manager (GDM). The GDM manages the login interface along with authenticating a user password and username, and then starting up a selected desktop. If problems ever occur using the GUI interface, you can force an exit of the GUI with the CTRL-ALT-BACKSPACE keys, returning