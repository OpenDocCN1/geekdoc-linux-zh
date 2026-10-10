boot Linux is controlled by a *runlevel*—a system state entry in `/etc/inittab`. The following runlevels are defined in the file:

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

In this example, Linux boots and then runs X.

The default display manager might also be specified in `/etc/inittab`, as follows:

```
x:5:respawn:/usr/bin/xdm -nodaemon
```

However, Fedora uses a shell script named `prefdm`, found under the `/etc/X11` directory, to set the display *manager*:

```
x:5:respawn:/etc/X11/prefdm -nodaemon
```

According to this script, the display manager is based on the file named `desktop` under the `/etc/sysconfig` directory. The words GNOME, KDE, and XDM following a `DESKTOP=` entry determine what display manager is used for login. The following sections describe how to configure the three most commonly used display managers: gdm, kdm, and xdm.

# Configuring gdm

The gdm display manager is part of the GNOME library and client distribution included with Fedora, and it provides a graphical login when a system boots directly to X. Its login (which is actually displayed by the gdmlogin client) hosts pop-up menus of window managers, languages, and system options for shutting down (halting) or rebooting the workstation. Although you can edit (as root) `gdm.conf` under the `/etc/X11/gdm` directory to configure gdm, a much better way to configure GNOME’s display manager is to use the `gdmsetup` client.

You can use the `gdmsetup` client to configure many aspects of how GDM appears and behaves. You launch this client from the GNOME System menu, under Administration, Login Window.

When `gdmsetup` loads, you’ll see the GDM Setup window, as shown in Figure 3.8.