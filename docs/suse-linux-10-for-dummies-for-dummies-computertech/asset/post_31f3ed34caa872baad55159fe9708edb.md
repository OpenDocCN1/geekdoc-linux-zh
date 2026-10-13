
6. **Read the release notes and click Next.**

The release notes contain last-minute information about the SUSE Linux distribution, including any known problems and workarounds. It’s worth glancing through so that you know about anything that might apply to your PC’s hardware configuration. When you click Next, YaST detects all of your PC’s hardware and displays a summary (Figure 2-9).

7. **Accept or change the displayed hardware configuration for your PC (Figure 2-9) and click Next.**

The hardware configuration includes information about specific hardware such as your graphics card, monitor, sound card, printing system, and so on. Typically, the displayed configuration should be acceptable, but you should check each of the items. In particular, check the graphics card configuration to see if YaST correctly detected the monitor and graphics card. If not, you can make changes by clicking Graphics Cards (see Figure 2-9) and changing the information in a subsequent window. After the configuration steps are complete, YaST informs you that the installation is complete, as shown in Figure 2-10.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_53_0.png)

**Figure 2-9:** Accept or change hardware configuration and click Next.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_54_0.png)

**Figure 2-10:** Click Finish to reboot and begin using your SUSE system.

8. **Click Finish to complete the installation.**

The installer then reboots the system. If you are using the KDE desktop, the system automatically logs you in using the local user account you defined during installation. Otherwise, you see the graphical login screen where you can log in to the system and start using it.

Congratulations! You can now start using SUSE Linux.

## Chapter 3: Starting SUSE for the First Time

*In This Chapter*

- Powering up SUSE Linux
- Logging in
- Checking out the GUI desktops
- Playing with the shell
- Shutting down

You’re sitting in front of your PC about to turn it on. You know that the PC has SUSE Linux installed. You’re wondering what to expect when you turn it on and what you do afterward. Not to worry. If you’re using SUSE Linux for the first time, this chapter shows you how to log in, check out the graphical desktops, try out some cryptic Linux commands, and finally, shut down the PC.

If this quick tour of SUSE Linux seems hurried, don’t worry; I cover everything at a slower pace and with more details in later chapters.

For those of you who already know something about SUSE Linux, flip through this chapter to see if anything looks new. You never know what you may not know!

### Powering Up SUSE Linux

When you power up the PC, it goes through the normal power-up sequence and loads the boot loader — called GRUB. The boot loader is a tiny computer program that loads the rest of the operating system from the hard drive into the computer’s memory. The whole process of starting up a computer is called _booting_.

The GRUB boot loader displays a graphical screen with the names of the operating systems that the boot loader can load. For example, if your PC has both Microsoft Windows and SUSE Linux installed on the hard drive, you see both names listed. Use the up- and down-arrow keys to select the operating system you want to use and press Enter. If the PC is set up to load SUSE Linux by default, you don’t have to do anything — after a few seconds the boot loader starts SUSE Linux.

You see a graphical boot screen that shows information about the progress of the system startup. If you selected KDE as your desktop and enabled automatic login during installation, you are automatically logged in and you get a KDE desktop similar to the one shown in Figure 3-1. By the way, SUSE Linux logs you in using the normal user account that you set up during installation. If you selected GNOME as your desktop, then you are logged in to a GNOME desktop.

If Automatic Login is not enabled for any user, you get a graphical login screen. You can log in using the account you defined during the installation. Type the username and press Enter. When prompted for it, type the password and press Enter. You then see the initial GNOME graphical user interface (GUI — pronounced *gooey* for short) appear.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_56_0.png)

You should not normally log in as `root`. When you log in as `root`, you could accidentally damage your system because you can do anything when you’re `root`. Always log in as a normal user. When you need to perform any task as `root`, type `su -` in a terminal window and enter the root password. Graphical system administration tools such as YaST prompt for the `root` password when needed.

### Getting GUI

When you install SUSE Linux, you can install one of two GUI desktops — GNOME or KDE. I provide a quick look at both KDE and GNOME desktops in this section.

Figures 3-1 and 3-2 provide a snapshot of KDE and GNOME desktops, respectively. In these figures, I point out the major components of each desktop.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_57_0.png)

Figure 3-1: Getting familiar with the KDE desktop.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_58_0.png)

**Figure 3-2:** Getting to know the GNOME desktop.

- **Panel:** The panel is like the Windows taskbar. KDE has one at the bottom of the screen, and GNOME has one at the top and one at the bottom. The KDE panel and GNOME’s top panel are the places where you can access the main menu of applications and launch programs by clicking icons on the panel. The panel also shows information such as the date and time and what applications are currently running.

- **Main Menu:** This is the leftmost button on the KDE panel and GNOME’s top panel. It brings up the Main menu (see Figure 3-3), from which you can start applications and perform other tasks such as lock the screen, get help, switch users, or log out. In GNOME, the Main Menu is labeled Applications menu, and some of these options are in separate menus — the Places menu and the Desktop menu.

- **Desktop Icons:** The desktops display the usual desktop icons — a My Computer icon for browsing the contents of the computer, a Trash icon, and icons for accessing devices such as a floppy drive and a CD/DVD drive or CD writer. The KDE desktop also has an icon for browsing the local Windows network, as well as icons for support, Print Manager, and the OpenOffice.org office suite.

- **Home Folder:** Opens your home directory in a graphical file manager.

- **Terminal Program:** Runs a program that provides a terminal window where you can type Linux commands.

- **SUSE Help Center:** Starts the SUSE Help Center, where you can get help on various aspects of SUSE Linux.

- **Web Browser:** Runs the Web browser.

- **Personal Information Manager:** Starts a mail, calendar, and contact manager. GNOME desktop provides Evolution as the personal information manager.

- **Desktop Pager or Workspace Switcher:** Click on a square to bring up a different desktop.

- **Clipboard Tool:** Click to see what has been cut and what you can paste elsewhere.

- **Power Management Tool:** Right-click to view a menu that you can use to start the YaST Power Management module that enables you to edit power-saver settings.

- **Volume Control:** Click to change the sound volume.

- **SUSE Hardware Tool:** Click to view information about devices in the PC and configure them.

- **SUSE Watcher:** Click to open a window you can use to both check for online updates as well as start online updates.

- **Clock:** Displays the current time. Clicking it brings up a calendar showing the current date.

- **Hide Panel:** Available in KDE, the end-point of the panel serves as a “hide panel” button, which means that if you click this icon, the panel slides to the right and disappears. Click again, and the panel reappears. You can hide the panel to create more room for other windows.

In addition to what you see on the KDE and GNOME desktops, you have many more choices in the main menu that appears when you click Main Menu on the panel. (See Figure 3-3.) Similar to the Windows Start button, the Main Menu is where you start when you want to run an application.
