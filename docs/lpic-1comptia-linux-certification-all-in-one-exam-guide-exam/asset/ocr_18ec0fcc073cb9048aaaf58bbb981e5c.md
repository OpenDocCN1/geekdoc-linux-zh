server is to actually install the fonts you want to distribute on it. If your Linux distribution is running X.org, then your fonts need to be installed to the /usr/share/X11/fonts directory or the /usr/share/fonts directory. Here is an example:

```
fs2:/usr/share/fonts # ls
100dpi  75dpi  Speedo  Type1  URW  cyrillic  encodings  misc  truetype
```

Linux fonts come in two varieties:

+   * **Bitmap fonts**  Bitmap fonts are the oldest type of Linux fonts. As the name implies, bitmap fonts use a series of pixels to represent characters on the screen. They are easy to use and don't require much computing horsepower to display on the screen. However, they do have one glaring weakness: They scale poorly. Basically, you need a different version of the same font for each screen resolution and each font point size. In other words, installing one bitmap font on your Linux system will probably require you to install multiple font files.
+   In the preceding example, you can see that there is one directory in the fonts directory named 100dpi and another directory named 75dpi. Most X servers install a limited number of bitmap fonts by default.

+   * **Scalable fonts**  Scalable fonts, as their name implies, are scalable. Instead of using pixels to represent characters, they use vector lines that are dynamically sized as needed. As a result, you only need a single font file for each font.
+   There are two commonly used formats for scalable fonts:

+   * **PostScript Type 1**  In the preceding example, these fonts are stored in the Type1 subdirectory.

+   * **TrueType**  In the preceding example, these fonts are stored in the truetype subdirectory.

To install a font, copy the font files to the appropriate subdirectory of your system's fonts directory. For Type1 fonts, you need to copy the .pfa or .pfb file for the font. For TrueType fonts, you need to copy the .ttf file for the font. Bitmap font files need to go into the 100dpi and/or the 75dpi directories.

Then you need to create a font description file for the font and register it with the system. To do this, open a terminal session and (as root) switch to the font directory and enter the mkttfonscale command followed by the mkfontdir command. These commands make an index of scalable (as well as bitmap) font files for the X server.

Next, you need to open port 7100 in the firewall of the X font server.

> **TIP** If you installed the font in a directory other than one of the default directories (Type1 or truetype) in the fonts directory, you must manually edit your X configuration file (such as xorg.conf) and add a FontPath directive to your Files section for the new directory.