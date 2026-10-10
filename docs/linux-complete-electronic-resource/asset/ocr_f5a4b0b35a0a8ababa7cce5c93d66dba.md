Jeff Phillips <`jeff@IRATUS.org>` uses Caldera's WordPerfect 7 for Linux (on Slackware, of all things) and says that it works well. It apparently includes built-in printer support, as one would expect. Caldera should have info at `http://www.caldera.com/`. You can also buy a newer version of WordPerfect directly from Corel’s chosen Unix port company.

Other vendors should feel free to drop me a line with your offerings.

# ON-SCREEN PREVIEWING OF PRINTABLE THINGS

In this section you’ll learn that nearly anything you can print can be viewed on the screen, too.

# PostScript

Ghostscript has an X11 driver best used under the management of the PostScript previewer `gv`. The latest versions of these programs should be able to view PDF files, as well. Note that `gv` has replaced the older previewer `Ghostview`; the new user interface is much prettier and more full of features than Ghostview’s plain old Athena GUI.

# TeX DVI

TeX DeVice Independent files may be previewed under X11 with `xdvi`. Modern versions of `xdvi` call Ghostscript to render PostScript specials.

A VT100 driver exists as well. It’s called `dgvt`. `Tmview` works with Linux and `svgalib`, if that’s all you can do.

# Adobe PDF

Adobe’s Acrobat Reader is available for Linux; just download it from their Web site at `http://www.adobe.com/`.

You can also use `xpdf`, which is freeware and comes with source, and I should think Ghostview supports viewing PDF files with `gs` under X11 by now.