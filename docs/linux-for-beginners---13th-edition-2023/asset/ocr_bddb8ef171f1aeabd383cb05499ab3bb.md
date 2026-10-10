# Command Line Quick Reference

When you start using Linux full time, you will quickly realise that the graphical interfaces of Ubuntu, Mint, etc. are great for many tasks but not great for all tasks. Understanding how to use the command line not only builds your understanding of Linux but also improves your knowledge of coding and programming in general. Our command line quick reference guide is designed to help you master Linux quicker.

# TOP 10 COMMANDS

These may not be the most common commands used by everyone but they will certainly feature frequently for many users of Linux and the command line.

**cd**
The cd command is one of the commands you will use the most at the command line in Linux. It allows you to change your working directory. You use it to move around within the hierarchy of your file system. You can also use chdir.

**mv**
The mv command moves a file to a different location or renames a file. For example mv file sub renames the original file to sub . mv sub ~/Desktop moves the file 'sub' to your desktop directory but does not rename it. You must specify a new filename to rename a file.

**ls**
The ls command shows you the files in your current directory. Used with certain options, it lets you see file sizes, when files where created and file permissions. For example, ls - shows you the files that are in your home directory.

**chown**
The chown command changes the user and/or group ownership of each given file. If only an owner (a user name or numeric user ID) is given, that user is made the owner of each given file, and the files' group is not changed.

**cp**
The cp command is used to make copies of files and directories. For example, cp file sub makes an exact copy of the file whose name you entered and names the copy sub but the first file will still exist with its original name.

**chmod**
The chmod command changes the permissions on the files listed. Permissions are based on a fairly simple model: You can set permissions for user, group and world and you can set whether each can read, write and or execute the file.

**pwd**
The pwd command prints the full pathname of the current working directory (pwd stands for 'print working directory'). Note that the GNOME terminal also displays this information in the title bar of its window.

**rm**
The rm command removes (deletes) files or directories. The removal process unlinks a filename in a filesystem from data on the storage device and marks that space as usable by future writes. In other words, removing files increases the amount of available space on your disk.

**clear**
The clear command clears your screen if this is possible. It looks in the environment for the terminal type and then in the term.info database to figure out how to clear the screen. This is equivalent to typing Control-L when using the bash shell.

**mkdir**
Short for "make directory", mkdir is used to create directories on a file system. If the specified directory does not already exist. For example, mkdir work creates a work directory. More than one directory may be specified when calling mkdir.