# Configuring X Fonts

directly into X, consult “Running an XDMCP Server” for information on doing this.) A quicker approach, but one that presents some opportunity for error, is to add the font path to a running system using the xset program:

```
$ xset fp+ /your/font/directory
$ xset fp refresh
```

The first of these commands adds /your/font/directory to the end of the font path. (Substitute +fp for fp+ to add the directory to the start of the existing font path.) The second command tells X to re-examine all the font directories to rebuild the list of available fonts. The result is that you should now be able to access the new fonts. (You'll need to restart any programs that use the new fonts.) One program to quickly test the matter xfont enables to select an X core font for display so you can check if the fonts you've added are available and display as you expect.

# Configuring a Font Server

Prior to the release of XFreeType 4.0, several Linux distributions began using TrueType-enabled font servers to provide TrueType font support. Most distributions have now abandoned this practice, but some haven't, and font servers can be useful in some environments.
A font server is how windy to deliver fonts to many computers from a central location. This can be a great time-saver if you want to add fonts to many computers—set them up to use a font server and tweak that server's font configuration. To use a font server, X must list that server in its font path:

Section “Files”

```
FontPath "unix:/7100"
FontPath *tcp/font.pangaea:7100
```

EndSection

The first line in this example specifies a local server. (Using unix:-1 rather than unix:/7100 also works in some cases.) The second line specifies that the server on the remote font server,.pangaea is to be used. If your computer is already configured to use a font server, you don't change the X configuration to add or delete fonts; you can modify the server's configuration. (You can still modify the X configuration directly, but it may be cleaner to manage all the local fonts from one configuration file).
Add to a font server, you should first install the fonts on the system, as described earlier You should then modify the font server’s configuration file, /etc/X11/fs/config. Rather than a series of FontPath lines, as in the main X configuration file, the font server’s configuration lists the font path using the catalogue keyword as a comma-delimited list:

```
catalogue = /usr/share/fonts/100dpi:unscaled,
/usr/share/fonts/Type1,
/usr/share/fonts/truetype,
```