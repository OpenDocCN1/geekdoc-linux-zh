![](bbox=[0.29, 0.09, 0.71, 0.32])

FIGURE 6.4 Use the Hardware tab's Video Card Configure button to choose a new video card for your X sessions.

If your video card supports the use of two or more monitors, you can use the Dual head tab toconfigure multiple monitor support. Xorg supports multiple displays using a feature named Xinerama. This feature enables multiple monitors to appear as a single display, and each display can be located in any quadrant of a screen's layout.

In order to use Xinerama for your desktop sessions, you must start the xorg server with its +xinerama option. For xorg.conf file must also have proper settings, and each display must be capable of supporting identical color depth (usually 16bpp or thousands of colors). Details about using Xinerama with xorg can be found in the xorg man page and in the Xinerama HOWTO at http://www.tldp.org/HOWTO/Xinerama-HOWTO/ .

When you have finished your changes to your X server settings, click the OK button. You will then see a dialog advising that you will need to log out and then log back (or exit your X session and restart X) in order to use the new settings.

The new settings will be stored in a new xorg.conf file under the /etc/X11 directory. If you find that the new settings do not work, you can simply copy the backup xorg.conf file named xorg.conf.backup to xorg-conf in the same directory to revert to your origi
nal settings.

# Using Xorg to Configure X

You can create the xorg.conf file manually by typing one from scratch using a text editor, but you can also create one automatically by using the Xorg server or configuration utili
ties (as discussed in the previous sections). As the root operator, you can use the follow
ing on the server to create a test configuration file:

```
# X -configure
```

After you press Enter, a file named xorg.conf.new is created in root's home directory, the /root directory. You can then use this file for a test session, like this:

```
# X -config /root/xorg.conf.new
```