
configuration. You can also use a `DefaultDepth` entry (which is 24, or thousands of colors, in the example), along with a specific color depth to standardize display depths in installations.

You can also specify a desktop resolution larger than that supported by the hardware in your monitor or notebook display. This setting is known as a virtual resolution in the Display subsection. This allows, for example, an 800x600 display to pan (that is, slide around inside) a virtual window of 1024x768.

> **NOTE**
> 
> If your monitor and graphics card support multiple resolutions and the settings are properly configured, you can use the key combination of Ctrl+Alt+Keypad+ or Ctrl+Alt+Keypad- to change resolutions on the fly during your X session.

## Configuring X

Ubuntu usually does a good job of detecting your graphics card and monitor, although sometimes problems can arise if the PC’s video card is not recognized. If your display is not configured correctly then Ubuntu thankfully provides some tools to help you make changes to the way your display is set up.

You can use the following configuration tools, among others, to create a working `xorg.conf` file:

- `displayconfig-gtk`—This is Ubuntu’s graphical configuration tool, which launches a handy GUI tool to help create an `xorg.conf` file.
- `Xorg`—The X server itself can create a skeletal working configuration.

![](img/8f9e74e2b343ff525bebfb720a3d8441_91_0.png)

FIGURE 3.4  The `displayconfig-gtk` client provides a graphical configuration interface for creating or updating a system’s `xorg.conf` file. Here you see the Screen Settings main screen, offering resolution and color-depth settings.

The following sections discuss how to use each of these software tools to create a working xorg.conf file.

## Configuring X with the displayconfig-gtk Client

You can use the displayconfig-gtk client to create or update an xorg.conf file. You can start by clicking the Screens and Graphics menu item found under System, Administration

![](img/8f9e74e2b343ff525bebfb720a3d8441_92_0.png)

FIGURE 3.5 displayconfig-gtk's hardware settings are used to configure a video card for X.

if you are already running X. You will be asked to enter your password in order to open the application; once you've done this you'll see a window similar to Figure 3.4.

![](img/8f9e74e2b343ff525bebfb720a3d8441_92_1.png)

FIGURE 3.6 You can scroll to select the correct graphics card to use for your X sessions.

The Screen Settings window shows the current selected screen, along with details of the model, resolutions available, the refresh rate, and orientation. In the event that you are using two screens (dual- or multi-head displays) then you have the ability to select whether it is the primary or secondary screen, and the physical location of it.

If you click the Graphics Card tab, other configuration options become available, as shown in Figure 3.5.

Click the name of the graphics card to open up a list of alternative cards (shown in Figure 3.6). Simply select a manufacturer to see a list of cards associated with that manufacturer and to choose the correct one for your X sessions.

When you have finished your changes to your X server settings, you can quickly test them to see if they will work by clicking the Test button. Ubuntu will then attempt to use your chosen settings, allowing you to either choose to keep them or revert back to the original settings. If you are happy with the new mode then click Keep Configuration. Finally, click the OK button to close the dialog box. You may then see a dialog advising that you have to log out and then log back in (or exit your X session and restart X) to use the new settings.

The new settings will be stored in a new xorg.conf file under the /etc/X11 directory. If you find that the new settings do not work, you can simply copy the backup xorg.conf file named xorg.conf.backup to xorg.conf in the same directory to revert to your original settings.

## Using Xorg to Configure X

You can create the xorg.conf file manually by typing one from scratch using a text editor, but you can also create one automatically by using the Xorg server or configuration utilities (as discussed in the previous sections). As the root operator, you can use the following on the server to create a test configuration file:

```
# X -configure
```

After you press Enter, a file named xorg.conf.new is created in root's home directory, the /root directory. You can then use this file for a test session, like this:

```
# X -config /root/xorg.conf.new
```

## Starting X

You can start X sessions in a variety of ways. The Ubuntu installer sets up the system to have Linux boot directly to an X session using a display manager (that is, an X client that provides a graphical login). After you log in, you use a local session (running on your computer) or, if the system is properly configured, an X session running on a remote computer on the network. Logging in via a display manager requires you to enter a username and password. You can also start X sessions from the command line. The following sections describe these two methods.

> NOTE
> If you have used the Server install then your system will boot to a text login—see "Command Line Quickstart" in Chapter 4 for more details on what to do here.
