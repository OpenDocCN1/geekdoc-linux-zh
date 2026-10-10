Each section begins with a Section statement and ends with an End-Section statement. These statements serve to delineate one section from another. Within each section, you can use the listed entries. Many of them enable you to specify a value or name (such as Load “xf86Jstk.so”); be sure to enclose strings (alphanumeric expressions) in quotation marks.

# The Files Section

The Files section specifies the default paths for fonts, X system colors, and X program modules. The following illustrates the appearance of this section:

```
Section "Files"
    RgbPath "/usr/X11R6/lib/X11/rgb"
    FontPath "/usr/X11R6/lib/X11/fonts/Local", \
             "/usr/X11R6/lib/X11/fonts/misc", \
             "/usr/X11R6/lib/X11/fonts/75dpi:unscaled", \
             "/usr/X11R6/lib/X11/fonts/100dpi:unscaled", \
             "/usr/X11R6/lib/X11/fonts/Type1", \
             "/usr/X11R6/lib/X11/fonts/Speedo", \
             "/usr/X11R6/lib/X11/fonts/75dpi", \
             "/usr/X11R6/lib/X11/fonts/100dpi/" 
    ModulePath "/usr/X11R6/lib/modules"
EndSection
```

The next table shows the options you can use in the Files section.

# FILES SECTION ENTRIES

| Use This Entry | To Do This |
|---|---|
| **FontPath** *path names* | Specify the path names of available system fonts in a comma-separated list. Note: Red Hat 6.x and derived systems (including Mandrake 6.x and 7.x) provide font support by means of the xfs font server. The list of font path names should be listed in the Catalogue section of the xfs configuration file */etc/X11/fs/config*.