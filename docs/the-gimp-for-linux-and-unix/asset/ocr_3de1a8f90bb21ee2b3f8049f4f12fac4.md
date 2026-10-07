# Chapter 14

# Where Have All the Fonts Gone?

The GIMP ships with about 12 fonts. This certainly isn't enough fonts, considering all the incredible fonts that are available. It is possible to install new Type 1 and TrueType fonts and the GIMP to recognize them, though the process is a bit involved. The following instructions are for those of you running the GIMP on Linux. Have heart, stick to the steps, and you can load in as many fonts as you like.

![](bbox=[0.535, 0.065, 0.955, 0.285])

Figure 6. Use File Manager to copy your Type 1 fonts to a directory of your choice.

# To install Type 1 fonts:

+   1. Using File Manager, copy your Type 1 fonts to a directory of your choice (**Figure 6**). In this example, the directory is /home/phyllis/fonts/.
2. Use a browser to go to `ftp://sunite.unc.edu/pub/Linux/X11/xutils/` (**Figure 7**).
3. Scroll down the list until you find the typelinst-0.6.1.tar.gz

![](bbox=[0.535, 0.365, 0.955, 0.505])

Figure 7. Use a browser to go to `ftp://sunite.unc.edu/pub/Linux/X11/xutils/`. Scroll down until you find the typelinst-0.6.1.tar.gz link.

![](bbox=[0.015, 0.395, 0.045, 0.545])

# Type 1 and TrueType Fonts—What's the Difference?

PostScript Type 1 and TrueType are technical standards used to create fonts. Both standards are resolution independent, meaning that they can be scaled to virtually any size and retain their resolution. (Fonts that are not scalable, as bitmap fonts, will look jagged when their size is changed.)

The difference between Type 1 and TrueType fonts is in the mathematics used to describe the curves of the letters and the size of the font files.

Most high-end devices, such as Linotronic and Varityper imagesters, typically use PostScript Type 1 fonts since they can be sent directly to the output device. TrueType fonts can be downloaded as bitmaps, but this can slow down printing.

If you want to learn more about the differences between Type 1 and TrueType fonts, take a look at Thomas W. Phinney's excellent article at:

```
http://www.truetype.demon.co.uk/articles/ttv1.html
```

210