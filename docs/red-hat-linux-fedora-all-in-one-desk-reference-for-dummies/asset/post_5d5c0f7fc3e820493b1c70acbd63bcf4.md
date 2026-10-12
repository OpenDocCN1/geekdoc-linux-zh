
Figure 1-8:
Set the geographic location from the Weather Preferences menu.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_136_0.png)

For U.S. locations, scroll down to your state and click the plus sign. Then select your location from the list and click OK. Then right-click the GNOME Weather Report applet icon and select Update. The applet should now display the weather for your location. Figure 1-9 shows a typical weather display by the Weather Report applet.

Figure 1-9:
The Weather Report applet displays weather information on the panel.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_136_1.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_136_2.png)

If you don't want the applet anymore, right-click and choose Remove from Panel from the menu.

GNOME has many more applets (over 20, in fact) to try out. There is almost a cottage industry of applets. For example, refer to Figure 1-7: The first menu shows five categories of applets and a number of button applets such as the Log Out button and the Lock button. Table 1-4 gives you an overview of the applets in these categories.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_136_3.png)

If any applet listed in Table 1-4 strikes your fancy, go ahead and try it out. To find an applet, right-click an empty area of the panel, choose Add to Panel, and then look in the appropriate category menu.

Table 1-4 GNOME Applets

| Applet | What It Does |
|---|---|
| *Accessories* | |
| Clock | Displays the current time (and date, when you mouse over the applet). |
| Dictionary Lookup | Displays a small text input area and a Lookup button so you can type a word and look up its meaning by using the GNOME Dictionary program. |
| Stock Ticker | Displays stock quotes in a scrolling stock ticker. |
| Weather Report | Displays weather information. |
| *Amusements* | |
| Fish | Displays a small fish. |
| Geyes | A pair of eyes that follows your mouse around the screen. |
| *Internet* | |
| Inbox Monitor | Checks for e-mail and lets you know when you have new mail. |
| Modem Lights | Provides an interface for dialing out with the modem and viewing status information about the modem when you're using it. |
| Terminal Server Client | Runs an application that can connect as a client to Microsoft Windows 2000 Terminal Server and display a remote desktop from that server (available only if you install the tsclient package). |
| Wireless Link Monitor | Displays the status of your PC's wireless link, provided you have a wireless link up and running. |
| *Multimedia* | |
| CD Player | Provides the user interface for a CD player. |
| Volume Control | Provides an interface for controlling sound volume and launching an audio mixer application. |
| *Utility* | |
| Battery Charge Monitor | Displays the charge status of your laptop's battery (so this applet is for laptops only). |
| Character Palette | Shows accented versions of a character (you type the character) so that you can copy and paste it into documents. |
| Command Line | Adds a small command line where you can type Linux commands. |
| Disk Mounter | Displays a disk drive icon that you can click to access a drive. |
| Keyboard Layout Switcher | Displays an icon through which you can switch the keyboard layout from one country to another. |
| *Utility* | |
| Notification Area | Sets up an area where notification icons appear. |
| Pilot Applet | Displays an icon for synchronizing your Palm Pilot with the Red Hat Linux system. |
| Show Desktop Button | Displays a button that lets you hide all windows and show the desktop. |
| System Monitor | Shows you how busy your PC is. |
| Window List | Displays buttons for each of the running applications. |
| Workspace Switcher | Displays a rectangle that contains four small rectangular areas, each representing a virtual desktop that you can click to switch to that virtual desktop. |
| *Launchers* | |
| Launcher... | Brings up a dialog box from where you can set up a new launcher — an icon on the panel that acts as a shortcut to an application. |
| Launcher from menu | Provides access to the entire Main Menu hierarchy from which you can pick a program and create a launcher for that program on the panel. |
| *Other* | |
| Button | Brings up a list from which you can select a button to add to the panel (the buttons enable the user to perform specific tasks such as log out, lock the screen, take a screenshot, perform a search, and run a command). |
| Main Menu | Adds a Main Menu button to the panel (this is the Red Hat button from which you can access the entire menu hierarchy and start any application). |
| Drawer | Adds a drawer, which acts as a storage area for other applets (it looks like a real drawer — you can open and close it by clicking). |

## Using the Nautilus Shell

The Nautilus file manager, or more accurately graphical shell, is intuitive to use — it's similar to the Windows Active Desktop. You can manage files and folders and also manage your system with Nautilus.

### Viewing files and folders

When you double-click a file or a folder, Nautilus starts automatically. For example, double-click the home icon in the upper-left corner of the GNOME desktop. Nautilus runs and displays the contents of your home directory
(think of a directory as a folder that can contain other files and folders). If you want to see the folders you're browsing, choose View→Side Pane from the Nautilus menu. Figure 1-10 shows a typical user's home directory in the Nautilus file manager after you choose View→Side Pane.

With the side pane open, the Nautilus window is vertically divided into two parts. The left window shows different views of the file system and other objects that you can browse with Nautilus. The right window shows the files and folders in the currently selected folder in the left window. Nautilus displays icons for files and folders. For image files, it shows a thumbnail of the image.

The Nautilus window's title bar shows the name of the currently selected folder. The Location text box along the top of the window shows the full name of the directory in Linuxspeak — in this case, Figure 1-10 is showing the contents of the /home/naba directory.

If you have used Windows Explorer, you can use Nautilus in a similar manner. To view the contents of another directory, do the following:

- 1. **Choose Tree from the Information drop-down menu (located in the left window).**
  A tree menu of directories appears in that window. Initially the tree shows the root directory as a folder labeled /.
- 2. **Click the right arrow next to the / folder; in the resulting tree view, locate the directory you want to browse.**
  For example, to look at the /etc directory, click the right arrow next to the /etc directory. This causes Nautilus to display the subdirectories in /etc and to change the right arrow to a down arrow. X11 is one of the subdirectories in /etc that you'd view in the next step.
- 3. **To view the contents of the X11 subdirectory, click X11.**
  The window on the right now shows the contents of the /etc/X11 directory, as shown in Figure 1-11.

Nautilus displays the contents of the selected directory using different types of icons. Each directory appears as a folder, with the name of the directory shown underneath the folder icon. Ordinary files, such as XF86Config, appear as a sheet of paper. The file named X is a link to an executable file. The pref dm file is another executable file.

The Nautilus window has the usual menu bar and a toolbar. Notice the View as Icons button in Figure 1-11 on the right side of the toolbar. That means Nautilus is displaying the directory contents using large icons. Click the button, and a drop-down list appears. Select View as List from the list; this
causes Nautilus to display the contents by using smaller icons in a list format, along with detailed information, such as the size of each file or directory and the time when each was last modified, as shown in Figure 1-12.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_140_0.png)

Figure 1-10:
You can view files and folders in Nautilus.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_140_1.png)

Figure 1-11:
The Nautilus file manager shows the contents of the /etc/X11 directory.
