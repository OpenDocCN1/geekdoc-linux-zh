# D.3 Frink

+   7. Click the Unstuff button, or press the Return key.

+   8. StuffIt Expander will now unpack the files from the CD-ROM to a
folder on your desktop.

# D.3 Frink

Frink is distributed as a gzip tar archive (frink132.tgz) with a
configure script for Unix systems. A compiled version of frink is in the
D:\win_bin directory. The frink source code is also packaged as a self-
extracting zip file.

# D.3.1 Compiling frink under MS-Windows

To compile this package with VC++ 4.0 follow these steps:

+   1. Place the Tcl/Tk for Real Programmers CD-ROM in your CD-ROM drive.

+   2. Run the D:\devel\frink\frink132.exe self-extracting zip archive to
extract the source code. By default this will be extracted into

```
C:\frink.32
```

+   3. Start up VC++.

+   4. Create a new project (File - New - Project Workspace).

+   5. Select Console Application from the listbox, and check win32 under
Platform.

+   6. Type the path to the directory you created (but not the directory
elf) in the Location: entry box (i.e., if you created a new directory
C:\frink, type C: in the Location: entry box).

+   7. Type the name of the directory you created in the Name: entry box.

+   8. Click the Create button. The new project will now be created. Wait until
t progress bars have been erased from your screen.

+   9. Open the Insert Files into Project window (Insert - Files into Project).

+   10. With the control key depressed, click each of the .c files with the left
mouse button, then click the Add button.

+   11. Pull down the Build menu-button and select Build All.

663