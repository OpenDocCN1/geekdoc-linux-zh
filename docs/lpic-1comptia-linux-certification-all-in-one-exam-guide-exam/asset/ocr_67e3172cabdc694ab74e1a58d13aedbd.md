If you're using X.org, your configuration settings are saved in /etc/X11/xorg.conf. If you're using XFree86, your configuration settings are saved in /etc/X11/XF86Config. Here is a portion of a sample xorg.conf file:

```
Section "InputDevice"
 Driver "vmmouse"
 Identifier "VMware Mouse"
 Option "Buttons" "5"
 Option "Device" "/dev/input/mice"
 Option "Name" "IMS/2 Generic Wheel Mouse"
 Option "Protocol" "IMPS/2"
 Option "Vendor" "Sysp"
 Option "ZAxisMapping" "4 5"
 Option "Emulate3Buttons" "true"
EndSection

Section "Modes"
 Identifier "Modes[0]"
 Modeline "1024x768" 65.0 1024 1048 1184 1344 768 771 777 806 -hsync -vsync
 Modeline "1024x768" 61.89 1024 1080 1184 1344 768 769 772 794
EndSection
```

Notice in this example that the xorg.conf file is broken into sections that begin with the Section *name* directive and end with EndSection.

![](bbox=[0.05, 0.43, 0.13, 0.5])

> **NOTE** The XF86Config file version 4 and later use a similar structure. Older versions of XFree86 use a slightly different configuration file format.

Let's look at the most commonly used sections in a typical xorg.conf file. First is the Files section. This section tells the X server where to find the files it needs to do its job, such as font files and input device files. Here is an abbreviated example of a Files section:

```
Section "Files"
 FontPath "/usr/X11R6/lib/X11/fonts/misc:unscaled"
 FontPath "/usr/X11R6/lib/X11/fonts/local"
 FontPath "/usr/X11R6/lib/X11/fonts/75dpi:unscaled"
 FontPath "/usr/X11R6/lib/X11/fonts/100dpi:unscaled"
 ""
 FontPath "/usr/X11R6/lib/X11/fonts/ttest"
 FontPath - "/opt/kde3/share/fonts"
 InputDevices "/dev/gpmdata"
 InputDevices "/dev/input/mice"
EndSection
```

Next is the ServerFlags section. This section specifies global X server options. This section is optional, and any options specified in it may be overridden by corresponding options with the same name listed in the ServerLayout section. Here is an example of a ServerFlags section in an xorg.conf file:

```
Section "ServerFlags"
 Option "AllowMouseOpenFail" "on"
EndSection
```

In this example, the AllowMouseOpenFail option is set to a value of on. This allows the X server to start up even if a mouse isn't connected or can't be initialized.