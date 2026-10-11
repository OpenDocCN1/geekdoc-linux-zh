In addition, you can use the **system-config-display** command to configure the video adapter card and monitor information for the X.org implementation of X Windows in Red Hat Fedora Core 2. Regardless of whether this command is run from a GUI or terminal environment, it automatically detects your video and monitor hardware. It then proceeds to load a graphical environment (if one doesn't already exist) and a configuration utility that can be used to set the maximum resolution and color depth, as shown in Figure 9-20.

> **NOTE**
> 
> Alternatively, you can navigate to the Red Hat button, System Settings, Display within the GNOME or KDE desktop to start the configuration utility shown in Figure 9-20.

![](bbox=[0.17, 0.36, 0.65, 0.77])

Although your video card and monitor are automatically detected and configured, you can alter these settings by clicking the Hardware tab of the configuration utility, as shown in Figure 9-21. In addition, if you have two video cards and two monitors, you can configure them to work as a single large display by clicking the Dual head tab, as shown in Figure 9-22.

After you click OK in the configuration utility, the previous /etc/X11/xorg.conf file is saved as /etc/X11/xorg.conf.backup and the new settings are written to /etc/X11/xorg.conf. You must then restart X Windows for the changes to take effect.