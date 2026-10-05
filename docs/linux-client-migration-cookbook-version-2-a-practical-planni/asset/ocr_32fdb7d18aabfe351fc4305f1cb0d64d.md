```
picture_options = stretched
picture_opacity = 100
draw_background = true
```

The following code changes the wallpaper to a corporate logo:
gconftool-2 --type string --set /desktop/gnome/background/picture_filename/usr/share/backgrounds/images/corporate_logo.Jpg

Immediately after running the command, the wallpaper should change to the newly specified path.

For further information about how to make mandatory changes to GConf, 7.1.2, "GNOME lockdown options" on page 151.