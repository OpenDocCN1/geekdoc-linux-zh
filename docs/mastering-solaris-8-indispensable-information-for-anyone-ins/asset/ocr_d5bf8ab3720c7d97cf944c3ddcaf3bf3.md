There are really only two significant options that you might want to use with the `mkdir` command:

+   * The `-m`, or mode, option sets the access privileges of the directory using either symbolic or octal nomenclature (these two systems are described in the section “Modifying Access Rights” earlier in this chapter).
+   * The `-p`, or parent, option will create any directory name in the path you specified if it doesn’t already exist.

For example, if you specify a list of directory names without paths, then `mkdir` creates those directories in your current directory. If you give the command `mkdir -p /usr/docs/letters/l2001letters` from within the docs directory and the docs directory doesn’t already have a `/usr/docs/letter` subdirectory, then this command creates the `/usr/docs/letters` subdirectory and places the `l2001letters` directory into that new subdirectory. This is a pretty convenient option to use if you can remember it.

The second option (-m) that allows you to set the access privileges of a new directory is illustrated by the command `mkdir -m ugo=rwx-w 12001letters`, which creates the new directory and gives the user, group, and others access rights to read and execute but not to write. In octal format, a similar command, `mkdir -m 600 12001letters`, creates the directory and sets the user’s access permissions to read (4) plus write (2).

In the CDE, to use the File Manager window to create a new folder, follow these steps:

+   1. Select the New Folder command from the File menu. The New Folder dialog box, shown in the following graphic, appears.

![](bbox=[0.32, 0.58, 0.78, 0.72])

+   2. To have Solaris create the new folder at the location you specify, enter the path name and folder name (in the format `<pathname>/<foldername>`) into the New Folder Name text box.
+   3. Click the Apply button to create the folder or the OK button to create the folder and close the dialog box.

The New Folder dialog box is not a command-line processor; it doesn’t support the `-p` or `-m` options, nor will it accept a folder name list.