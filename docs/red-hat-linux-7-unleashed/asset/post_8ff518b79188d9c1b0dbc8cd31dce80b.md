
If the panel is getting in the way during your KDE session, click the small button to the far left or right of the panel to temporarily hide the panel from your screen. To restore the panel, click the small button again.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_164_0.png)

## Using KDE's Konqueror or the K File Manager

The newest K file manager, known as **Konqueror**, is near the center of the magic of new versions of KDE. This file manager (included with the newer, but not stable version of KDE on your CD-ROMs) will eventually replace KDE's current kfm client, and provides a usable desktop where you can drag, drop, multiple-select, copy, move, or delete icons of data files or programs. Many of the desktop actions supported by Konqueror become apparent when you drag or right-click a file's icon.

The Konqueror client is launched like the kfm client when you ask for help or click on your KDE panel's home directory icon. After installation, this client may also be launched as a Web browser from the panel's Internet menu. Like kfm, if you have an active Internet connection, you can browse to remote Web sites and FTP files directly from remote computers by dragging icons of files from the Konqueror window to your desktop.

The **root** display, which includes your home directory and your **root** display, is represented by the directory named **Desktop** in your home directory. If you drag files to this folder, the files' icons appear on your **root** display. Similarly, if you drag a file from another folder or directory to the desktop, it appears in your **Desktop** directory.

The Konqueror client is installed along with the newer KDE base files, support libraries, and other RPMs. You'll find the newer KDE distribution under the /preview directory of your second Red Hat Linux CD-ROM.

## Configuring KDE with the KDE Control Center

The KDE Control Center is the main dialog box through which you can change numerous settings of your desktop, get system information (such as the currently mounted devices and capacities), or (if logged in as the root operator) configure and control KDE's appearance, background, fonts, and sessions for all users.

Click the Application Starter button on your desktop's panel, and then click KDE Control Center to display the Control Center dialog box. The main dialog box appears, as shown in Figure 5.14.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_165_0.png)

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_165_1.png)

### Using Display Manager Options

Use the Modules menu's Applications group login menu item in the Control Center to change the appearance or contents of the kdm login dialog box. You must be logged in as the root operator to access this portion of the Control Center, but you can get around this limitation without logging out of the current KDE session. Open a terminal window and type the `su` command, followed by the `kcontrol` client, on the command line:

```
# su -c kcontrol &
```

The Login Manager dialog box, shown in Figure 5.15, enables you to change how the kdm login dialog box appears when you set Linux to boot directly to X. You can change the greeting strings, the type of logo used, and even the language used for your KDE sessions. By clicking different tabs at the top of the dialog box, you can change the fonts, background, icons for users (perhaps using a scanned image of a person’s face), and sessions using other window managers. After you make your changes, click Apply.

**Figure 5.15** Use the Login Manager tab to change the appearance of KDE’s login screen.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_166_0.png)

You can also control which users are permitted to log in. Click the Users tab in the Login Manager dialog box. The Users dialog box appears, as shown in Figure 5.16. To selectively control user logins, click the Show Only Selected Users button and then click and add users to the Selected Users section of the dialog box using the >> button.

To control reboot or shutdown through the kdm login screen, click the Sessions tab of the Login Manager dialog box and then click the Allow to Shutdown drop-down menu. Select None, All, Root Only, or Console Only. When finished, click the Apply button.

### Changing Your Desktop’s Wallpaper

KDE comes with nearly 150 different wallpapers to fill the root display or to fill your desktop’s background. To configure the current desktop’s wallpaper, again use the Control Center, then choose Look & Feel, Desktop, then Background from the Modules menus. You can also click a blank area of the desktop and select the Configure Background menu item. Additionally, you can click the Application Starter button on the desktop panel and select Preferences, Look & Feel, Desktop, then Background.

**Figure 5.16** The Users tab can control who is permitted to log in in Linux through Xsso.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_167_0.png)

**Note**

KDE wallpapers are in JPEG format and are stored under the /usr/share/wallpapers directory. Many of these wallpapers look best when used with a display using thousands of colors. Although the default KDE wallpapers are in JPEG format, other graphics formats may be used. Look under the /usr/share/pixmaps/backgrounds/tiles directory for nearly two dozen images suitable in tiled format as a background. You'll find six directories of 230 swirling, colorful images under the /usr/share/pixmaps/backgrounds/Propaganda directory. You'll also find an excellent selection of stunning NASA photos under the /usr/share/pixmaps/backgrounds/space directory.

The Background dialog box, shown in Figure 5.17, enables you to set the name of each desktop, each desktop's colors, and whether the desktop uses a wallpaper. To set a different wallpaper, click the Wallpaper pop-up menu in the Wallpaper section of the dialog box and then click Apply. A random setting may be used to show wallpapers on the desktop from different directories in different order and at specified intervals.

**Figure 5.17** Use the Background dialog box to set your desktop's name, colors, and wallpaper.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_168_0.png)

### Changing Your Screensaver

KDE comes with 20 different screensavers. To configure a screensaver for your KDE desktop, click Preferences, Look & Feel, then the Screensaver menu item on the Panel menu. You can also use KDE's Control Center.

The Screensaver dialog box, shown in Figure 5.18, has a number of settings, such as the type of screensaver, the time delay before activating the screensaver, a random setting to cycle through installed screensavers, and whether you want to require a password to go back to work. After you make your changes, click Apply; click OK to close the dialog box.

**Figure 5.18** The Screensaver dialog box has different settings you can use to test a screensaver, set a time delay, or require a password.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_168_1.png)

### Changing Keyboard and Mouse Settings

Click **Keyboard** from the *Peripherals* menu in the Control Center's *Modules* menu to toggle keyboard character repeat (repeated printing of a character when a key is held down), and whether each key-press generates a key-click sound. Click **Apply** (shown in Figure 5.19) when you finish with your selection.

**Figure 5.19** *The Keyboard dialog box toggles Keyboard repeat and key-click sounds.*

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_169_0.png)

You can also access keyboard and mouse settings through the panel's *Preferences* menu or KDE's Control Center. The *Mouse* dialog's *Advanced* tab lets you change how fast your mouse cursor moves across the screen. To change the sequence of mouse buttons for right- or left-handed users, use the *General* tab (shown in Figure 5.20). These functions are similar to using the **xset** and **xmodmap** commands from the command line.

**Note**

Mouse behavior when clicking on windows may also be configured by using the *Look & Feel*, *Windows Behavior*, *Mouse Behavior* menu item in the Control Center.
