feature named Xinerama. This feature enables multiple monitors to appear as a single display, and each display can be located in any quadrant of a screen's layout.

To use Xinerama for your desktop sessions, you must start the `xorg` server with its `+xinerama` option. Your `xorg.conf` file must also have proper settings, and each display must be capable of supporting identical color depth (usually 16bpp or thousands of colors). You can find details about using Xinerama with `xorg` in the `xorg` man page and in the Xinerama HOWTO at http://www.tldp.org/HOWTO/Xinerama-HOWTO/. When you have finished your changes to your `X` server settings, click the OK button. You will then see a dialog advising that you have to log out and then log back in (or exit your `X` session and restart `X`) to use the new settings.

The new settings are stored in a new `xorg.conf` file under the `/etc/X11` directory. If you find that the new settings do not work, you can simply copy the backup `xorg.conf` file named `xorg.conf.backup` to `xorg.conf` in the same directory to revert to your original settings.

# Using Xorg to Configure X

You can create the `xorg.conf` file manually by typing one from scratch in a text editor, but you can also create one automatically by using the `xorg` server or configuration utilities (as discussed in the previous sections). As the root operator, you can use the following on the server to create a test configuration file:

```
# X -configure
```

After you press Enter, a file named `xorg.conf.new` is created in root's home directory, the `/root` directory. You can then use this file for a test session, like this:

```
# X -config /root/xorg.conf.new
```

# Starting X

You can start `X` sessions in a variety of ways. The Fedora installer sets up the system initialization table `/etc/inittab` to have Linux boot directly to an `X` session, using a *display manager* (that is, an `X` client that provides a graphical login). After you log in, you use a local session (running on your computer) *or*, if the system is properly configured, an `X` session running on a remote computer on the network. Logging in via a display manager requires you to enter a username and password. You can also start `X` sessions from the command line. The following sections describe these two methods.

# Using a Display Manager

An `X` display manager presents a graphical login that requires a username and password to be entered before access is granted to the `X` desktop. It also allows you to choose a different desktop for your `X` session. Whether an `X` display manager is presented after you