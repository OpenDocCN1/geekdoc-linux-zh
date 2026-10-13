> **Tip**
> 
> `switchdesk-kde` is another utility that you can use instead of switchdesk-gnome. The difference between these tools is in the toolkits used for displaying the dialog boxes. Either tool can be used to select either desktop.

# SELECTING GNOME MANUALLY

If you want to select GNOME by hand, you can modify the configuration files directly. This can be useful if you have a very customized start-up sequence.

To modify the default desktop for all users under Red Hat and similar distributions, simply edit `/etc/sysconfig/desktop` and enter GNOME as a single line. This will automatically set the desktop for all users who haven't selected their own already.

If you want to set the default desktop for a single user under Red Hat, edit `${HOME}/.Xclients` to read `exec gnome-session`.

Under Debian, at least with the current state of woody, there's no automatic way to select GNOME for all users. On a per-user basis, you can add the following to `${HOME}/.xsession`:

```
```text
# Load default window-manager
/usr/bin/x-window-manager&
# Start GNOME
exec /usr/bin/gnome-session
```
```

You may also want to make sawfish your default window manager:

```
```text
# update-alternatives --config x-window-manager
```
```

There are 4 programs which provide `x-window-manager`.

```text
Selection    Command
     1       /usr/bin/sawfish
     2       /usr/bin/X11/twm
     3       /usr/bin/kde2
*    4       /usr/X11R6/bin/wmaker

Enter to keep the default[*], or type selection number: 1
Using '/usr/bin/sawfish' to provide x-window-manager.
```

OpenLinux has no native support for GNOME, and although it has some hooks similar to Red Hat's `/etc/sysconfig/desktop`, it appears to be moving away from this strategy with OpenLinux 2.4. Currently, the best way to make GNOME your desktop is to edit `${HOME}/.xsession` to read `exec gnome-session` (as in Debian).

> **Tip**
> 
> `${HOME}/.Xclients` or `${HOME}/.xsession` is the last file run by the window manager after start-up, so this is the place for anything you want run before your window manager. Running your window manager should always be the last line of this file, and should always be preceded with `exec` (as in `exec startkde`). The exec tells the shell to completely replace itself with the window manager. Otherwise, an unnecessary copy of your shell will be left in memory. See “SHELL BUILTIN COMMANDS” in the bash man page for more information on exec.