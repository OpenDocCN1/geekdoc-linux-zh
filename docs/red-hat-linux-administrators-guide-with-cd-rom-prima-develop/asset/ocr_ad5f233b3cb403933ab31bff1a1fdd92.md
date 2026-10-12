You can find all the documentation needed for compiling and installing at the main KDE home page, http://www.kde.org/. To avoid increasing the already congested traffic at this site, try one of the many mirrored sites. These locations carry all the same source code, documentation, and information as the main KDE site. Using a mirror site will most likely also increase your download speed, which, considering the size of many of these files downloaded via a modem, can be quite tedious.

The documentation includes explicit instructions on how to compile and install each program on your hard drive. Generally you can install as many as 10 packages, although only two are required and a third is recommended. The others merely complement the core KDE files with a wide assortment of utilities. Sequence is also important in successfully installing the programs. Here is the recommended order as shown on the main KDE installation page:

+   ♦  *kdesupport* (recommended). This package contains support libraries that have not been written as part of the KDE project, but which are needed nevertheless. If the libraries in this package (libgif, libjpeg, libmime, libau, and libgdbm) are already installed on your system, you may not need to install kdesupport. You should probably install it if only to standardize on the release.

+   ♦  *kdelibs* (required). This package contains shared libraries that all KDE applications need.

+   ♦  *kdebase* (required). This package contains the base applications that form the core of the K Desktop Environment: the window manager, the terminal emulator, the control center, the file manager, and the panel.

+   ♦  *kdegames* (optional). This package includes few games such as *Mabjongg*, *Snake*, *Asteroids*, and *Tetris*, to name a few.

+   ♦  *kdegraphics* (optional). This package includes various graphics-related programs such as PostScript Previewer, DVI Previewer, and a drawing program.

+   ♦  *kdetools* (optional). This package includes various desktop tools, including a calculator, an editor, and other nifty utilities also found on a default Red Hat install but using the Qt libraries and optimized for KDE.

+   ♦  *kdemultimedia* (optional). This package contains multimedia applications such as a CD player, a mixer, and an MP3 player.