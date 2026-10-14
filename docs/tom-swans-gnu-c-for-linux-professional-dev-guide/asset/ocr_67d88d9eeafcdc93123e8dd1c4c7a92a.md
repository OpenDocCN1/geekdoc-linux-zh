the easiest solution is to install everything—enable that option at the end of the component list and go on to the next screen. However, if you choose to install only some components, in addition to the default selections, add at least the following items (items marked with an asterisk are required for this book's sample programs):

+   - Printer Support
+   - X Window System* (Chapters 28-30 only)
+   - KDE or Gnome X Interface or Other Window-managers*
+   - Emacs (console only), Emacs with X windows (console for X), or XEmacs (graphical interface), or all three programming editors*
+   - C Development*
+   - Development Libraries*
+   - C++ Development*
+   - Kernel Development
+   - X Development*
+   - X Games (recommended)
+   - KDE and Gnome Development
+   - Extra documentation (recommended)

> Note
> You may see an option for installing individual packages—archives containing files, patches, and installation information for different pieces of Linux and related software. Don't select this option unless you are an experienced Linux user. Various components need multiple, dependent packages, and not selecting the correct packages might cause installation to fail. You can install individual packages at any time after you install Linux (see Chapter 3, "Installing GNU C++").

When you are finished selecting the components you want to install, the automatic installer creates a file system on your drive partitions. This might take several minutes, especially if you elected to check for bad blocks. There is little or no indication that something is happening during this process, so unless you can see a flashing drive light or other indicator, be patient, even if the computer appears to have fallen asleep.

Soon, you will see numerous installation screens that display all sorts of text, progress bars, and other items while individual components are unpacked and installed. There's nothing for you to do except watch, so you might want to get up, stretch, eat lunch, or have a cup of tea. On a slow system, this stage of the installation might take a half hour or more.

After all selected components are installed, "auto probe" looks for a mouse. Read the resulting screen and make any necessary changes. If you have a two-button mouse, enable the Emulate 3 Buttons check box. Some Linux programs, particularly X software, use three mouse buttons, and unless you have a three-button mouse, it's a good idea to select this feature now.