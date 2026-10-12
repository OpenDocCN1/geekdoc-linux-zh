
## Adding User Accounts

Figure 3-6:
The sound card configuration utility displays information about the sound card.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_92_0.png)

When you start Red Hat Linux for the first time, you get the chance to add a personal user account. If you didn't add a user account during the first boot as described in Chapter 4 of this mini-book (or if you want to add more user accounts for family members or coworkers), you can do so at any time by using the Red Hat User Manager.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_92_1.png)

Setting up a personal user account other than root is a good idea. The problem with root is the absolute power of that superuser account — you can literally do anything, even destroy critical system files, with ease. It's better to log in as an ordinary user. When you must do something as root, simply type the su command. You'll be prompted for the root password; after you enter that password you'll become root. When you're finished with your superuser duties, type exit to return to your mere mortal self.

To add user accounts with the Red Hat User Manager, follow these steps:

- 1. Choose Main Menu→System Settings→Users and Groups from the GNOME desktop.

If you're not logged in as root, the Red Hat User Manager prompts you for the root password (see Figure 3-7), which you have to enter to run the manager.

Figure 3-7:
Enter the root password here.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_92_2.png)

- 2. Enter the password and click OK.

The Red Hat User Manager window (shown in Figure 3-8) features two tabs: Users and Groups. The Users tab displays the current list of user accounts. The Groups tab lists your current groups. Figure 3-8, for example, lists the users on my Red Hat Linux system; the list will be different on your system.

- 3. To add a new user, click the Add User button on the toolbar.

The Create New User dialog box appears, as shown in Figure 3-9.

- 4. Fill in the requested information, and then click OK.

The new user now appears in the list on the Users tab in the Red Hat User Manager window.

Figure 3-8:
The Red Hat User Manager window shows the current user accounts.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_93_0.png)

Figure 3-9:
Entering information about a new user account.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_93_1.png)

- 5. Repeat Steps 3 and 4 to add as many user accounts as you want.
- 6. When you're done, choose File→Exit to quit the Red Hat User Manager.

To edit existing user account information, select the user name from the list in the Users tab and then click the Properties button on the toolbar. The selected user's information appears in a User Properties dialog box, where you can then edit it; click OK to make the changes.

If you want to remove a user account, click the user name in the Users tab. Then click the Delete button on the toolbar.

## Managing CD-ROMs

The GNOME desktop makes it easy to use CD-ROMs in Red Hat Linux. Just place a CD-ROM in the drive, and an icon appears on the desktop. Behind the scenes a special utility called Magicdev is always running, waiting to detect when a CD-ROM is inserted or removed. When you insert a CD that has an autorun file, Magicdev asks whether you want to run that file (Figure 3-10).

Figure 3-10:
The Magicdev prompt.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_94_0.png)

Typically, running the autorun file starts an installer program that can install the software on the CD.

Magicdev also automatically starts the Nautilus file manager, which shows the contents of the CD-ROM (as in Figure 3-11).

Finally, Magicdev puts a CD-ROM icon on the GNOME desktop. You can then use the CD, either through the Nautilus file manager or through the icon on the desktop. To access the files and folders, you simply double-click the icons in the Nautilus window.

The CD-ROM icon is your best bet for certain tasks such as ejecting the CD when you're done with it. If you right-click the CD-ROM icon, a pop-up menu appears, listing the things you can do with the CD-ROM (as in Figure 3-12).

![](img/a7eec43a54473e95dc5ea333fecf1bd7_95_0.png)

Figure 3-11:
When you insert a CD, Nautilus displays the CD's contents.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_95_1.png)

Figure 3-12:
Choosing what to do with the CD-ROM.

When you're done with the CD, choose Eject from the pop-up menu to eject the CD-ROM from the drive. Doing so automatically removes the icon.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_96_0.png)

If there is a CD in the CD-ROM drive and you don't see a CD-ROM icon on the GNOME desktop, just eject the CD (by pressing the Eject button on the CD-ROM drive). Insert the CD again and Magicdev should recognize the CD.

The KDE desktop also automatically opens a CD-ROM's contents in a file manager called Konqueror. For example, Figure 3-13 shows the result of inserting a CD in the KDE desktop.

Figure 3-13:
KDE automatically displays a CD's contents in the Konqueror file manager.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_96_1.png)

## Installing RPM Packages

Sometimes you have to install or remove software to troubleshoot or configure your Red Hat Linux system. Most Red Hat Linux software comes in the form of Red Hat Package Manager (RPM) files. An RPM file is basically a single package that contains everything — all the files and configuration information — needed to install a software product. This section shows you how to install RPM packages.

From the GNOME desktop, use Add and Remove Software utility — a graphical utility for installing and uninstalling RPMs. Follow these steps:

- 1. Choose Main Menu→System Settings→Add/Remove Applications.
- 2. Type in the root password and press Enter.

If you're not logged in as root, a dialog box prompts you for the root password.

The Add and Remove Software utility starts and gathers information about the status of packages installed on your system. After it sorts through the information about all the installed packages, the utility displays a list of all the packages (Figure 3-14). The left side of the window has two large buttons: Install Software and Remove Software. By default the Install Software button is selected.

Figure 3-14: The Add and Remove Software utility shows information about the package groups.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_97_0.png)

The utility displays information about the packages organized into package groups such as Desktops and Applications (a package group is a collection of related RPMs). Each package group has a graphical icon, a label such as X Window System or GNOME Desktop Environment, and a brief description as well. For each package group, the utility displays how many packages are installed. If a package group has any uninstalled packages, the utility displays an Install hyperlink.

- 3. To install any uninstalled package, click the Install hyperlink next to that package.

A dialog box appears with details of what you're about to install and how much disk space the new packages would require. Figure 3-15 shows the result of clicking the Install hyperlink next to the KDE Desktop Environment in Figure 3-14.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_98_0.png)

Figure 3-15:
A package group's details.

- 4. Click Install Packages to install the selected package.

To remove one or more package groups, click the Remove Software button on the left panel in the Add and Remove Software window. Now the Add and Remove Software window shows the installed packages with a Remove hyperlink. To remove packages from a package group, click the Remove hyperlink next to that package group. A dialog box pops up listing the packages you can remove. Click Remove Packages and those packages are history!

## Chapter 4: Trying Out Red Hat Linux

### In This Chapter

- ✔ Booting Red Hat Linux
- ✔ Logging in
- ✔ Checking out the GUI desktops
- ✔ Playing with the shell
- ✔ Shutting down

You’re sitting in front of your PC about to turn it on. You know that the PC has Red Hat Linux installed (maybe you did the installing yourself, but who’s keeping track?). You’re wondering what to expect when you turn it on and what you should do afterward. Not to worry. If this is your first time using Red Hat Linux, this chapter shows you how to log in, check out the graphical desktops, try out some cryptic Linux commands, and finally, shut down the PC.

Those of you who already know something about Red Hat Linux, flip through the pages to see if anything here looks new. You never know what you may not know!

### Booting Red Hat Linux

When you power up the PC, it goes through the normal power-up sequence and loads the boot loader — GRUB or LILO, depending on which one was selected during Red Hat Linux installation. The boot loader is a tiny computer program that loads the rest of the operating system from disk into the computer’s memory. These programs are now called boot loaders (once known as bootstrap loader). The whole process of starting up a computer is called booting.

Whether the boot loader is LILO or GRUB doesn’t matter much. In either case, a graphical screen appears with the names of operating systems that the boot loader can load. For example, if your PC has Windows and Red Hat Linux, you see both names listed. You can then use the Up and Down arrow keys to select the operating system you want to use. If the PC is set up to
