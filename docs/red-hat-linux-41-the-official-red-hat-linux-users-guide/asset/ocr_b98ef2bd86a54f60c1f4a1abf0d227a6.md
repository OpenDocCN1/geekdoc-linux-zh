# C.2 Metro X Configuration File

# C.2.1 Warning

The primary configuration file for the X server is **Xconfig**. If inappropriate changes are made to this file, the proper functioning of Metro-X will be impaired! Do not edit the **Xconfig** file unless absolutely necessary.

# C.2.2 Xconfig

Metro-X looks for the **Xconfig** file in the following locations and in the following order:

```
"$HOME/Xconfig
$HOME/.Xconfig
/etc/X11/Xconfig (on Linux only)
/usr/lib/X11/Metro/Xconfig"
```

Most options are set with the configuration utility (**ConfigX**, section 5.3.3). Additional options can be added using an editor, and **ConfigX** will preserve these.

# C.2.3 Keywords

Descriptions of the **Xconfig** keywords are listed below. They are alphabetized here for your convenience and any order dependencies are noted within the individual entries.

# Options Set In Configuration Utility

The following list of **Xconfig** keywords are options controlled via the Metro-X Configuration Utility. Any changes to these options should be made through the utility to avoid accidental damage to the function of Metro-X.

**BitsPerPixel** <emph number> Some X drivers support packed 24 bits per pixel memory organization. This means that each pixel takes up three bytes of video memory. In this case, <emph configX> inserts the line: **BitsPerPixel** 24