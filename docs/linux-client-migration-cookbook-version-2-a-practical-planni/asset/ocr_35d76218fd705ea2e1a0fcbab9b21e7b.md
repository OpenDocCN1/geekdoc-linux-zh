# Configuration Editor - background

![](bbox=[0.258, 0.093, 0.803, 0.565])

E-2 Editing gconf2 entries with the graphical gconf-editor

gcontool-2 is a command line application, which provides the access to the same information and is quite useful for scripting purposes. The number of configuration options that are available to the gcontool-2 tool are vast and too numerous to list in this book. To display the current options that are set for the GNOME desktop, enter the following command:

gcontool-2 -R /desktop

Although we do not cover all options, we show how we customize our desktop and explain each of the commands that are used. To list all the settings associated with the desktop background, enter the following command:

gcontool-2 -R /desktop/gnome/background

This displays the following default values:

```
color_shading_type = solid
secondary_color = #585768
primary_color = #585768
picturere_filename=/usr/share/wallpapers/suse-1024x768.jpg
```

318 Linux Client Migration Cookbook, Version 2