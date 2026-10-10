
## Starting Other Applications

There are multiple ways to start a new application. As a systems administrator, you are likely to have a command window up (better known as an "xterm"), so you may find it convenient to simply run the application from there. In fact, most of this book assumes you are running applications from that prompt. Simply open a terminal window box by either clicking on the icon of a terminal on the desktop panel or clicking on the K menu, selecting Utilities, and then clicking on Terminal. This starts up kterm, which is functionally equivalent to an xterm. Once open, you can enter the name of the command you wish to run there and press ENTER.

> NOTE: Many commands discussed in this book must be run from a terminal window.

Under KDE, you can also bring up the equivalent of the Run option under the Windows Start menu by pressing ALT-F2. This brings up a small window in the center of your screen where you can type in the command you want to run. The window automatically goes away once you press ENTER to execute the command or ESC to abort (see Figure 3-5).

![](img/95b125a8bf06051f34d8aba73558b7eb_81_0.png)

Figure 3-5. Changing colors under KDE

The last way is to search through the directory listing using the file browser and double-clicking on the application name you want. This method is, of course, the most tedious, but it can be useful if you can't remember the name of the application. Common directories to check are /usr/bin, /usr/sbin, /bin, /sbin, and /usr/X11R6/bin.

## Changing the Color Scheme

If you're fussy about your desktop environment, you'll probably want to change the appearance of your desktop color scheme. With KDE's Control Center, this is quite easy. Begin by bringing the Control Center up and then click on the Desktop option in the left window. This will bring up a window that looks like Figure 3-6.

![](img/95b125a8bf06051f34d8aba73558b7eb_82_0.png)

Figure 3-6. The Desktop options under the Control Center

### CHANGING YOUR BACKGROUND

Click on the Background menu option under Desktop. This will bring up a configuration panel like the one in Figure 3-7.

To change your background, simply select either a color or wallpaper from the respective menu. If you choose a wallpaper, you can test what the wallpaper will look like before committing to it by clicking on Apply at the bottom of the screen. If you like what you see, you can keep the change by clicking OK. If you don't, simply set it back to the original and click on Apply again.

![](img/95b125a8bf06051f34d8aba73558b7eb_83_0.png)

Figure 3-7. Changing your background configuration panel

### CHANGING COLORS

To change the colors, click on the Colors menu option under Desktop. This will bring up a configuration panel like the one in Figure 3-8.

Simply click on the color combination you like best. If you want to create a new combination, click on the Add button underneath the list and give your new settings a name. Highlight this setting and then select the color you want to give each widget in the right side of the panel. For example, to change the color of normal text, open the widget drop-down box. Select Normal Text. The bar underneath the drop-down box will show the current color. Click on the bar to bring up a color wheel so you can select the new color you like best.

As always, click on Apply once you are done.

### CHANGING THE SCREENSAVER

To change the screensaver, click on the Screensaver option under Desktop. This will bring up a configuration panel like the one in Figure 3-9.

Select the screensaver you like in the menu box. A demo of it will appear in the picture of the monitor in the same panel. You can try out a full-screen version of the screensaver by clicking on Test. If that screensaver has configuration options, the Setup button will also be available so you can configure it.

![](img/95b125a8bf06051f34d8aba73558b7eb_84_0.png)

Figure 3-8. Changing colors under KDE

From this menu, you can also choose to lock your screen in addition to starting the screensaver. This is very handy if you need to leave your work-station in a conspicuous location, like an office.

But the most fun feature is the corner activation. Looking at the picture of the monitor carefully, we see that the four corners of the screen have little gray boxes. Clicking on the boxes reveals a menu that lets us pick Ignore, Save Screen, or Lock Screen. The default value is Ignore. However, by selecting either Save Screen or Lock Screen, you can then move the cursor to that corner and immediately cause that action to happen. For example, I have the lower-right corner of my screen set to Save Screen. When I want to immediately activate my screensaver, I simply move my mouse into that corner and *shazaam*! my screensaver is active. The lower-left corner is set to Lock Screen. So if I know I’m going away from my desk for a long time, I can immediately lock my screen by moving my mouse into the lower-left corner.

The default behavior for the screensaver is to activate after the number of minutes specified in the screensaver configuration window. Setting any of the corners to activate the screensaver does not invalidate the default behavior.

![](img/95b125a8bf06051f34d8aba73558b7eb_85_0.png)

Figure 3-9. Selecting the right screensaver

## ABOUT GNOME

GNOME (GNU Network Object Model Environment), like KDE, offers a complete desktop environment and application framework to make development as well as usage easier. What makes GNOME different is how it achieves these goals. Unlike KDE, GNOME is not a window manager. GNOME provides development libraries and session management—foundation features that we as users don’t see. On top of this foundation is a window manager that takes care of the general appearance of the desktop. The default window manager is Enlightenment, but there are several choices available.

> NOTE: According to the official Web site, the correct pronunciation of GNOME is guh-NOME. This is because the “G” in GNOME stands for gnu, and the correct pronunciation of GNU is guh-wnu. In the same paragraph the GNOME team states that no one will be offended if you pronounce it “NOME.”

From a developer’s point of view, GNOME is very interesting. It defines its interfaces with the rest of the world through the CORBA technology. Thus, any development system that can communicate using CORBA can be used to develop GNOME-compliant applications. (See their developers' Web pages at http://www.gnome.org for more information.) For users, this holds the potential for many applications to be developed to take advantage of the features in GNOME. Of course, like KDE, GNOME also works with existing X-Windows applications quite nicely.

> **NOTE:** If you do not have GNOME installed, you can download the application and installation directions from the GNOME Web site at http://www.gnome.org. Precompiled packages for various distributions are also available at their Web site.

## Starting X-Windows and GNOME

If you are using Red Hat Linux and have opted for its default, you already have GNOME installed as your default GUI. Depending on how X-Windows is configured, you may already have a graphical login prompt. In that case, logging in will automatically place you in the X-Windows environment. If you have a text-based login, simply run `startx` in order to bring X up, like so:

```
[root@ford /root]# startx
```

This should bring up a screen that looks something like Figure 3-10.

If the default GUI that starts is not GNOME, you can change your personal settings to use GNOME by editing the .xinitrc file in your home directory. Begin by trying to exit out of the window manager. If you are in KDE (represented by a big “K” in the lower-left corner), click on the K to bring up a menu. In that menu there should be an option to log out. If you're really stuck, you can also press CTRL-ALT-BACKSPACE to kill the underlying X-Windows manager. This will bring you back into text mode. Edit the .xinitrc file using your favorite editor. If you don't have a favorite, try pico, like so:

```
[root@ford /root]# pico .xinitrc
```

> **NOTE:** If you aren't familiar with pico, don't worry. All of the available commands are always shown at the bottom of the screen. Any command that starts with the caret symbol (^) means you use the CTRL key along with other keys specified. For example, ^X means CTRL-X.

Most likely, the file will be empty. If that is the case, simply add the following content:

```
#!/bin/sh
gnome-session
```

If the file is not empty, go to the very last line. It will probably begin with the string “exec,” which tells the system to execute a program. Change that line so that it reads “gnome-session” instead.
