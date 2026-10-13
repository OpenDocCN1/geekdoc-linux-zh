# LOOKING INSIDE ARCHIVES

To view the contents of an archive (tar, tgz, zip, and so forth) file, click the file. You can operate on individual files and directories inside the archive, just like you do in a normal directory. You can also right-click the archive and select Archiver, which provides a more archive-specific view, including the ability to easily extract and add items to the archive.

# SPECIAL FEATURES OR TIPS

The file manager has a couple of other features that serve as handy shortcuts for common operations.

# MISCELLANEOUS HANDY SHORTCUTS

To open a terminal window with the current directory the same as the file manager, select Tools, Open Terminal, or use the keyboard shortcut Ctrl+T. This is handy when you get to a directory and discover that you need to perform some complex action there. Instead of opening a terminal window and navigating there manually, just type Ctrl+T. Of course you can always use the integrated terminal emulator by selecting Window, Show Terminal emulator window.

To open a folder in a new file manager window instead of the current file manager window, click it with the middle mouse button.

To open a new file manager window with the same current directory as the current window, click the gear icon in the toolbar (located on the right of the toolbar).

Sometimes, you need to perform a file manipulation for which you just don’t have permissions. In this case it is possible to start a terminal window, su to root, and execute the commands by hand. However, to make it more convenient to overcome this situation, and to enable you to continue operating using a graphical file manager, KDE provides a way to launch a file manager with superuser (root) privileges.

To do this, select System, File Manager (Super User Mode) from the Application Starter menu. A special terminal window starts up and prompts you for the root password for your machine. Enter it, and a file manager with root privileges starts. To remind you that you are operating with special privileges, the handle of the menu bar in the file manager window is shown in bright red. You can use this file manager window to perform operations that require root privileges. When you drag files between file manager windows of both types (root and regular user) onscreen, the window that performs the copy, move, or link operation is the destination window (the window being dropped on). This means, for example, that you cannot drag a file to which you don’t have permissions from a root file manager window to a non-root file manager window. You can, however, perform this drag the other way around.

To view a window in full-screen mode, select Window, Fullscreen Mode (Ctrl+Shift+F). This will expand the current window to fill the entire screen, including the normal panel and menu areas. It will also get rid of the konqueror menu bar and status bar, leaving just