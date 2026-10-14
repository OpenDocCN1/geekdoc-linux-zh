
To add a launcher to the Quicklaunch applet you must already have the launcher set up in either the Main Menu or on your desktop. Once you have the launcher you may drag it onto the Quicklaunch applet to create a small launcher button. To launch the application simply press the launcher button.

To drag a launcher from your Main Menu click once on the menu to open it, and click once on the submenu to open it. With your left mouse button click and hold the application launcher and drag it to the Quicklaunch applet and release.

Once the launcher is in the Quicklaunch applet you may right mouse click on it and select Properties to change any properties associated with the launcher. The dialog that is launched is the standard GNOME launcher properties dialog which you can read more about in the section called Adding Application Launchers in Chapter 5.

## 13 GNOME CD Player

### Introduction

The GNOME CD Player (gtcd) is a GNOME-enabled application which is preloaded with GNOME. This is a simple CD Player which allows you to listen to Compact Discs on your PC.

### Using the GNOME CD Player

The GNOME CD Player will be available to you in the Main Menu in the Audio menu and can also be invoked in the command line with $gtcd.

![](img/46f4935125ba89e12897afbe9d77a097_648_0.png)

Figure 13-1: The GNOME CD Player

IMPORTANT: You must have the correct access to your CD-ROM drive for this application to be successful. If you have the root password type the following in a terminal window:

```
$ su
$ Password: [type in root password]
$ chmod a+r /dev/cdrom
$ exit
```

If your CD-ROM is located somewhere other than /dev/cdrom make sure you change it in the commands above.

The GNOME CD Player works like any CD Player with common buttons such as Play, Stop, Pause, etc. Plus a track selector button which displays the track titles in a drop down menu. You have access to change various properties as well by pressing the Preferences button. This will bring up the GNOME CD Player Preferences dialog.

There are three tabs in the GNOME CD Player Preferences, Preferences, Keybindings, and CDDB Settings.

![](img/46f4935125ba89e12897afbe9d77a097_649_0.png)

# Figure 13-2: The GNOME CD Player Properties

- Preferences Tab - In this dialog you may specify:
  - What you would like the GNOME CD Player to do when first started, and when exited.
  - The location of your CD-ROM on your system. This is usually /dev/cdrom.
  - The Color to display the Track and CD Title.
  - The Font to display the Track and CD Title.
  - Whether you would like handles on the title window which will allow you to drag the title window off the CD Player to float on the desktop.
  - Whether tooltips are enabled when your mouse is over the buttons.

- **Keybindings Tab** - In this tab you can change the keybindings associated with the GNOME CD Player. These keybindings allow you to use the Player without using your mouse. If you want to change one of the bindings select it with your mouse and type the new key in the **Click here to change** text box. Press Apply to save the changes

- **CDDB Settings Tab** - CDDB stands for CD Database and is a huge global database of CD information. Each CD has an identity which the CD Player can read. If you are connected to the Internet it will then search a CDDB server for that CD identity and return any information it has on it. This usually includes CD Title, Artist, and Track Titles. It can also include notes and lyric information. Once retrieved the GNOME CD Player will store the information on your hard drive for future access. In the CDDB Settings tab you can change the CDDB server and edit your local CDDB database. You can read more about CDDB by visiting the CDDB Website (http://www.dcdb.org).

Another feature in the GNOME CD Player is the Track Editor. The track editor can be launched by the Track Editor button on the main GNOME CD Player window. The Track Editor allows you to edit the CD track information in case it is incorrect or there was no CDDB entry for your CD. You may also check the status of the CDDB information by pressing the CDDB Status button at the bottom of the Track Editor. This will show you what messages, if any, were returned from the CDDB server.
