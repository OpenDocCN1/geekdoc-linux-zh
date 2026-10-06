# redhat-config-xfree86

| Display | The top part of this tab shows the relative display size with the name of the monitor and video card below. |
|---|---|
| Resolution | Sets the screen resolution. |
| Color Depth | Specifies the color depth. Using more colors requires more video memory. |
| Advanced Monitor | Specifies the type of monitor attached to the system. Click Configure to select from a list of monitors or to specify the characteristics of your monitor. From the Monitor Settings window, click Probe Monitor to have the system attempt to determine the type of monitor you are using. |
| Video Card | Specifies the type of video card in the system. Click Configure to select from a list of video cards. From the Video card settings window, click Probe Videocard to have the system to determine the type of video card in your system. |

# Initializing Databases

After booting the system, in as or so tu, root and makewhatis to update the whatis database so that whatis (page 79) and apropos (page 79) work properly; then run updatedb to update the locate database so that locate¹² works properly. The best way to use these utilities is to run the cron scripts that run daily. Working as root, give the following commands:

```
# /etc/cron.daily/makewhatis.cron
# /etc/cron.daily/socate.cron
```

These utilities run for up several minutes and may complain about not being able to find a file or two. When you get the prompt back, your whatis and locate databases are up-to-date.

# Setting Up the Default Desktop Manager

Red Hat introduced the Desktop Switcher scheme, which can replace the traditional scheme that uses the ~/.xinitrc and /etc/X11/xinit/xinitrc files to select a desktop

> 12. The locate (secure locate) utility allows you to index and search for files on your system quickly and securely.