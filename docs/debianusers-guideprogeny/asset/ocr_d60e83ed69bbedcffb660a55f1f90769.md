# # Stopping Commands from Running

Press Ctrl-C.

The command that is running stops. Then a new command prompt displays below the previous one.

# # Navigating the Command Line

Linux systems store files in directories. The directories are arranged in a tree-like structure. At the top of the tree is the root directory (\/. Even directories on another partition are sub-directories of the root directory. See “Searching for Files and Text,” page 167.

Using a few basic commands, you can

+   - Change directories.
+   - Read the contents of directories.
+   - Identify the type of entries in a directory.
+   - Find your current directory.
+   - Clear the screen.

# # Changing directories

*Type cd* DIRECTORY.

Unless the directory you are changing to is a sub-directory of the current one, usually you should type the full path name to the directory.

To change to the directory immediately above the present one, type cd..(two periods).

# # Reading the Contents of Directories

*Type ls* OPTIONS DIRECTORY.

By carefully selecting your options, you can use the ls list command to help you locate files. For example, -s lists files in order of size, while -t lists files by when they were modified.