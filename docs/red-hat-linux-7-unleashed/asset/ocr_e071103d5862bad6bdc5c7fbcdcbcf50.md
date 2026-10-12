```
/usr/share/fonts/ISO8859-7/100dpi:unscaled,
/usr/share/fonts/ISO8859-7/misc,
/usr/share/fonts/ISO8859-7/Type1,
/usr/share/fonts/ISO8859-7/75dpi,
/usr/share/fonts/ISO8859-7/100dpi
```

As you can see, you'll find additional fonts for X11 installed under the /usr/share/fonts directory. The ISO8859-2 fonts are part of a collection of nearly 400 central European (or Latin 2) fonts, and provide support for encoding characters in nearly a dozen Slavic and Central European languages.

You can verify the inclusion and availability of these fonts with the xfontsel client. Use xfontsel like this at the command line of a terminal window:

```
# xfontsel
```

You'll see a window (as shown in Figure 4.10) from which you can select different foundry and families of fonts (by clicking fmly).

![](bbox=[0.04, 0.46, 0.7, 0.62])

# XF86Config Module Section

The Module section is used to load server and rendering support, and specifies the names of modules to load from the /usr/X11R6/lib/modules directory:

```
# Module
Section "Module"
	Load "GLCore"
	Load "dbe"
	Load "dri"
	Load "extmod"
	Load "glx"
	Load "pex5"
	Load "record"
	Load "xie"
	Load "type1"
	Load "freetype"
EndSection
```