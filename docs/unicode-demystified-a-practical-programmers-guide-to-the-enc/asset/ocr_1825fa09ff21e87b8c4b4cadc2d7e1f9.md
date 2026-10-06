```
cat /etc/X11/starthere/sysconfig.desktop
Type=Link
Name=System Settings
Name[it]=Impostazioni di sistema
```

...
Comment=Change systemwide settings (affects all users)
Comment[it]=Modifica impostazioni generali del sistema (per tutti gli utenti)

Icon=redhat-system-settings.png
Terminal=0
Encoding=UTF-8

Terminal=0
URL=system-settings://

![](bbox=[0.476, 0.319, 0.712, 0.456])

**Figure 7-5** Start Here icon and label

# # Start Here

When you log in on a Red Hat system, many systems display a Nautilus window showing the Start Here special location. You can also display Start Here by double-clicking the Start Here icon (Figure 7-5) on the root window, clicking the same icon on a panel once, or entering start-here in the Nautilus location bar. Nautilus displays Start Here as a series of directories. Although Start Here is not strictly a menu, it is the root of a virtual directory structure that can help you in your day-to-day work on your system. In many areas Start Here functions overlap those of the GNOME menu. The Preferences folder, a subfolder of Start Here, duplicates the Preferences item on the GNOME menu. Look around and experiment: you will not be allowed to do anything harmful to the system unless you are logged in as root. Refer to “Start Here” on page 236 for more information.

> > GNOME Desktop and Nautilus
> The GNOME Desktop is run from a backend process that runs as part of Nautilus. If that process stops running, it will usually start up again automatically. If it does not, start Nautilus by giving the command nautilus to restore your desktop. You do not have to keep the Nautilus window open to keep the desktop alive.