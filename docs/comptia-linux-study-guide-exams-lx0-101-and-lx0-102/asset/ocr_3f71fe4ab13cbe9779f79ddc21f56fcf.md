# EXERCISE 4.2

# Locating Files

This exercise demonstrates several methods of locating files. You'll locate the startx program. If your system doesn't have X installed, you can search for another program or file, as pwd or fstab. You may need to change the path to find in step 5.) To find a file, follow these steps:

+   1. Log into the Linux system as a normal user.

+   2. Launch an xterm from the desktop environment's system if you use a GUI login method.

+   3. Type locate startx. The system should display several filenames that include the string startx. This search should take very little time. (A few distributions lack the locate command, so this won't work on some systems.)

+   4. Type where startx. The system responds with the names of a few files that contain the string startx. Note that this list may be slightly different from the list returned by step 3 but that the search proceeds quickly.

+   5. Type find /usr -name startx. This search takes longer and, when as an ordinary user, likely returns several permission denied error messages. It should also return a single line listing the /usr/bin/startx or /usr/X11R6/bin/startx program file. Note that this command searches only /usr. If you searched /usr/X11R6, the command would take less time; if you searched /, the command would take more time.

+   6. Type which startx. This search completes almost instantaneously, returning the complete filename of the first instance of startx system on its path.

+   7. Type type startx. Again, the search completes very quickly. It should identify startx as an external command stored at /usr/bin/startx, /usr/X11R6/bin/startx, or possibly some other location.

# Summary

File management is basic to being able to administer or use a Linux system. Common commands are useful to both users and administrators for copying, moving, renaming, and otherwise manipulating files and directories. You may also want to set up access controls, both to limit the amount of disk space users consume and to limit who may access specific files and directories. Linux provides tools to help you locate files using various criteria.