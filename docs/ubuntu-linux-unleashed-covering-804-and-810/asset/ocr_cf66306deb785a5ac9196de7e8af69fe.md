The Screen Settings window shows the current selected screen, along with details of the model, resolutions available, the refresh rate, and orientation. In the event that you are using two screens (dual- or multi-head displays) then you have the ability to select whether it is the primary or secondary screen, and the physical location of it.

If you click the Graphics Card tab, other configuration options become available, as shown in Figure 3.5.

Click the name of the graphics card to open up a list of alternative cards (shown in Figure 3.6). Simply select a manufacturer to see a list of cards associated with that manufacturer and to choose the correct one for your X sessions.

When you have finished your changes to your X server settings, you can quickly test them to see if they will work by clicking the Test button. Ubuntu will then attempt to use your chosen settings, allowing you to either choose to keep them or revert back to the original settings. If you are happy with the new mode then click Keep Configuration. Finally, click the OK button to close the dialog box. You may then see a dialog advising that you have to log out and then log back in (or exit your X session and restart X) to use the new settings.

The new settings will be stored in a new xorg.conf file under the /etc/X11 directory. If you find that the new settings do not work, you can simply copy the backup xorg.conf file named xorg.conf.backup to xorg.conf in the same directory to revert to your original settings.

# Using Xorg to Configure X

You can create the xorg.conf file manually by typing one from scratch using a text editor, but you can also create one automatically by using the Xorg server or configuration utilities (as discussed in the previous sections). As the root operator, you can use the following on the server to create a test configuration file:

```
# X -configure
```

After you press Enter, a file named xorg.conf.new is created in root's home directory, the /root directory. You can then use this file for a test session, like this:

```
# X -config /root/xorg.conf.new
```

# Starting X

You can start X sessions in a variety of ways. The Ubuntu installer sets up the system to have Linux boot directly to an X session using a display manager (that is, an X client that provides a graphical login). After you log in, you use a local session (running on your computer) or, if the system is properly configured, an X session running on a remote computer on the network. Logging in via a display manager requires you to enter a username and password. You can also start X sessions from the command line. The following sections describe these two methods.

> NOTE
> If you have used the Server install then your system will boot to a text login—see "Command Line Quickstart" in Chapter 4 for more details on what to do here.