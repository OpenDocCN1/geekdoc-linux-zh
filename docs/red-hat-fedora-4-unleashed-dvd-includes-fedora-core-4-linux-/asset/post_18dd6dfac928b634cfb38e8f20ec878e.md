
* `system-config-display`—This is Fedora's graphical configuration tool, which launches an X session to create an `xorg.conf` file.
* `xorg`—The X server itself can create a skeletal working configuration.

The following sections discuss how to use each of these software tools to create a working `xorg.conf` file.

## Configuring X with the system-config-display Client

You can use the `system-config-display` client to create or update an `xorg.conf` file. You can start by clicking the Display menu item from the desktop panel's System Settings menu if you are already running X, but you can also begin, as root, by starting the client from the command line during a console session, like this:

```
# system-config-display
```

The screen clears, and `system-config-display` attempts to start an X session. If you start this client during an X session, its main window appears, as shown in Figure 6.1.

![](img/774d40fd20903495c5cd00e2efad3f33_205_0.png)

**FIGURE 6.1** The `system-config-display` client provides a graphical configuration interface for creating or updating a system's `xorg.conf` file. Here you see the Display Settings main screen, offering resolution and color-depth settings.

The Display Settings main screen is a dialog showing the current monitor and video card settings (if configured). You can change the resolution (horizontal and vertical pixels) and color depth (number of supported colors) by clicking one or the other of the drop-down menus. Click the OK or Cancel button to save or cancel any change.

If you click the Hardware tab, other configuration options become available as shown in Figure 6.2.

![](img/774d40fd20903495c5cd00e2efad3f33_206_0.png)

**FIGURE 6.2** `system-config-display`'s Hardware settings are used to configure a monitor and video card (and multihead video card) for X11R6.

Click the Configure button in the Monitor Type area of the Hardware tab dialog to change your Monitor settings, as shown in Figure 6.3. You can use this dialog to configure a different monitor or to change current monitor settings.

First, scroll through the list of monitor brands (from the MonitorDB database), and then click the small triangle to the left of the name of the manufacturer or type. You will then see a list of model names. Click to select one, and when you are finished, click the OK button to use the new settings or click the Cancel button to abort changes.

To configure a video card, you can click the Video Card area's Configure button in the Hardware tab dialog. The Video Card dialog appears, as shown in Figure 6.4.

You can scroll through the list of video cards. You can click one to select it and when you are finished, click the OK button to finalize your selection.

![](img/774d40fd20903495c5cd00e2efad3f33_206_1.png)

**FIGURE 6.3** You can scroll to select a new monitor to use for your X sessions.

![](img/774d40fd20903495c5cd00e2efad3f33_207_0.png)

**FIGURE 6.4** Use the Hardware tab's Video Card Configure button to choose a new video card for your X sessions.

If your video card supports the use of two or more monitors, you can use the Dual head tab to configure multiple monitor support. Xorg supports multiple displays using a feature named Xinerama. This feature enables multiple monitors to appear as a single display, and each display can be located in any quadrant of a screen's layout.

In order to use Xinerama for your desktop sessions, you must start the xorg server with its `+xinerama` option. For xorg.conf file must also have proper settings, and each display must be capable of supporting identical color depth (usually 16bpp or thousands of colors). Details about using Xinerama with xorg can be found in the xorg man page and in the Xinerama HOWTO at http://www.tldp.org/HOWTO/Xinerama-HOWTO/.

When you have finished your changes to your X server settings, click the OK button. You will then see a dialog advising that you will need to log out and then log back (or exit your X session and restart X) in order to use the new settings.

The new settings will be stored in a new `xorg.conf` file under the `/etc/X11` directory. If you find that the new settings do not work, you can simply copy the backup `xorg.conf` file named `xorg.conf.backup` to `xorg.conf` in the same directory to revert to your original settings.

## Using Xorg to Configure X

You can create the `xorg.conf` file manually by typing one from scratch using a text editor, but you can also create one automatically by using the Xorg server or configuration utilities (as discussed in the previous sections). As the root operator, you can use the following on the server to create a test configuration file:

```
# X -configure
```

After you press Enter, a file named `xorg.conf.new` is created in root's home directory, the `/root` directory. You can then use this file for a test session, like this:

```
# X -config /root/xorg.conf.new
```

## Starting X

You can start X sessions in a variety of ways. The Fedora installer will set up the system initialization table `/etc/inittab` to have Linux boot directly to an X session using a *display manager* (that is, an X client that provides a graphical login). After you log in, you will use a local session (running on your computer) or, if the system is properly configured, an X session running on a remote computer on the network. Logging in via a display manager requires you to enter a username and password. You can also start X sessions from the command line. The following sections describe these two methods.

### Using a Display Manager

An X display manager presents a graphical login that requires a username and password to be entered before access is granted to the X desktop. It also allows you to choose a different desktop for your X session. Whether or not an X display manager is presented after you boot Linux is controlled by a *runlevel*—a system state entry in `/etc/inittab`. The following runlevels are defined in the file:

```
# 0 - halt (Do NOT set initdefault to this)
# 1 - Single user mode
# 2 - Multiuser, without NFS (The same as 3, if you do not have networking)
# 3 - Full multiuser mode
# 4 - unused
# 5 - X11
# 6 - reboot (Do NOT set initdefault to this)
```

Runlevel 5 is used for multiuser mode with a graphical X login via a display manager; booting to runlevel 3 provides a console, or text-based, login. The `initdefault` setting in the `/etc/inittab` file determines the default runlevel:

```
id:5:initdefault:
```

In this example, Linux boots and then ends up running X.

The default display manager might also be specified in `/etc/inittab`, like this:

```
x:5:respawn:/usr/bin/xdm -nodaemon
```

However, Fedora uses a shell script named `prefdm`, found under the `/etc/X11` directory, to set the display manager:

```
x:5:respawn:/etc/X11/prefdm -nodaemon
```

According to this script, the display manager is based on the file named `desktop` under the `/etc/sysconfig` directory. The words GNOME, KDE, and XDM following a `DESKTOP=` entry determine what display manager is used for login. The following sections describe how to configure the three most commonly used display managers: gdm, kdm, and xdm.

## Configuring gdm

The `gdm` display manager is part of the GNOME library and client distribution included with Fedora and provides a graphical login when a system boots directly to X. Its login (which is actually displayed by the `gdmlogin` client) hosts pop-up menus of window managers, languages, and system options for shutting down (halting) or rebooting the workstation. Although you can edit (as root) `gdm.conf` under the `/etc/X11/gdm` directory to configure `gdm`, a much better way to configure GNOME’s display manager is to use the `gdmsetup` client.

You can use the `gdmsetup` client, shown in Figure 6.5, to configure many aspects and features of the login display. You launch this client from the GNOME desktop panel’s System Settings Login Screen menu item, or from the command line, like this:

```
# gdmsetup &
```

After you press Enter, you see the GDM Setup window, as shown in Figure 6.5.

You can specify settings for security, remote network logins, the X server, and session and session chooser setup by clicking on the tabs in the GDM Setup dialog.

![](img/774d40fd20903495c5cd00e2efad3f33_209_0.png)

**FIGURE 6.5** You use `gdmsetup` to configure the `gdmlogin` screen when using `gdm` as a display manager.

## Configuring kdm

The `kdm` client, which is part of the KDE X desktop suite, offers a graphical login similar to `gdm`. You configure `kdm` by running the KDE Control Center client `kcontrol`, as the root operator, by clicking the Control Center menu item from the KDE `kicker` or desktop panel menu. You can also start KDE Control Center by using the `kcontrol` client at the command line like so:

```
$ kcontrol &
```
