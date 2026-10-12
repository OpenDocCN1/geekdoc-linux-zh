For example, to view the graphic `tiger.ps`, use the `gv` command from the command line of a terminal window like this:

```
# gv /usr/share/ghostscript/5.50/examples/tiger.ps
```

After you press Enter, you'll see the graphic in `gv`'s main window, as shown in Figure 8.9.

# **Note**

See Chapter 19, "Printing with Linux," for details on setting up your printer to work with Red Hat Linux. You'll learn about how Red Hat Linux uses software filters and the `gs` PostScript interpreter to translate PostScript documents into a format or language understood by your printer.

![](bbox=[0.2, 0.41, 0.9, 0.76])

**FIGURE 8.9**
*The `gv` client previews, rotates, scales, and prints PostScript documents, or selected pages of PostScript documents.*

You can use `gv`'s various menus to rotate the image, reduce or enlarge the display, page through, or print selected pages of multi-page PostScript documents. Another client included with Red Hat Linux to support previewing PostScript is KDE's `kghostview` previewer.

If you'd like to display other types of graphics, use the `display` command, part of the ImageMagick software package. This command may be used to display one or more images, or a visual directory of images, and has many different features. For example, to