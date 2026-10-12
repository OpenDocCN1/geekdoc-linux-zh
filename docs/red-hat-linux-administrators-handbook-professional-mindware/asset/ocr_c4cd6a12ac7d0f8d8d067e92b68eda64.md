section starts with the Section “<name of the section>” line and ends with an EndSection line. The following list describes the sections:

+   ■ **Files section.** Used to specify font and color database paths. Here is an example of such a section:

```
```
Section "Files"

RgbPath 		"/usr/X11R6/lib/X11/rgb"

FontPath 		"/usr/X11R6/lib/X11/fonts/misc/"
FontPath 		"/usr/X11R6/lib/X11/fonts/Type1/"
FontPath 		"/usr/X11R6/lib/X11/fonts/Speedo/"
FontPath 		"/usr/X11R6/lib/X11/fonts/75dpi/"
FontPath 		"/usr/X11R6/lib/X11/fonts/100dpi/"

EndSection
```
```

If you add new fonts to your system, you can use the FontPath option to specify the directory for the fonts you installed.

Other commonly used options that you can add in this section are listed in Table 14-1.

| **Table 14-1** *Options for the Files Section of XF86Config* | | |
| :--- | :--- |
| **Option** | **Description** |
| AllowNonLocalXvidmode | Allows the xvidmode program to connect from a remote host. |
| DisableVidMode | Disables certain video mode video extensions used by the xvidmode program. |
| AllowNonLocalModInDev | Allows a remote X client to change keyboard and mouse settings. |
| DisableModInDev | Disables certain input device extensions that can normally be set dynamically. |
| AllowMouseOpenFail | Allows the X server to start without a mouse. |