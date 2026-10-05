http://www.dcs.ed.ac.uk/home/jec/xfsft/

To be able to test the program, you obviously need TrueType fonts. The following-example is based on the Verdana font which is supplied with Microsoft Windows. (Please note that font files are subject to copyright and cannot be copied freely).

![](bbox=[0.335, 0.163, 0.664, 0.442])

Figure 7.4 The Verdana font in the fonts dialog of Gimp.

First you need to create a new directory (for example /usr/local/fonts/truetype). Into this directory, you copy all TrueType fonts with the extension *.ttf. Subsequently, you need to create fonts.dir. In the first line, this file contains the number of entries; in the following lines, the X font. You can either create this file manually (following the example of the fonts.scale.sample sample file supplied together with xfsft) or employ the ttkfdir program which you can find on the Internet.

http://www.darmstadt.gm.de/~pommnitz/xfsft.html

In the simplest case, fonts.dir for the verdana ttf could look as follows. (The second line is only split for reasons of space).

```
1
verdana.ttf \
-microsoft-verdana-medium-r-normal--0-0-0-0-0-p-0-iso8859-1
```

Entry in the configuration file and xfsft, plus insertion in XF86Contig are exactly the same as with xfs. Do not forget to include the TrueType directory in the configuration file.

# Setting the dpi value

dpi stands for dots per inch and specifies the screen resolution. An example: if your screen width is 36 cm (19-inch monitor) and the horizontal resolution 1280 pixels, then about 90 pixels are displayed per inch (1280 / 36 × 2.54).