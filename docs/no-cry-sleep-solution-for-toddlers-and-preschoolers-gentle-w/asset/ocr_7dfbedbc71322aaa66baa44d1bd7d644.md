byte in its octal representation. However, you can also specify a character, decimal, or hexadecimal representation. The od command is helpful when you need to detect any special character in your file or if you want to display a binary file.

# The File Structure

Linux organizes files into a hierarchically connected set of directories. Each directory may contain either files or other directories. In this respect, directories perform two important functions. A directory holds files, much like files held in a file drawer, and a directory connects to other directories, much as a branch in a tree is connected to other branches. With respect to files, directories appear to operate like file drawers, with each drawer holding several files. To access files, you open a file drawer. Unlike file drawers, however, directories can contain not only files, but other directories as well. In this way, a directory can connect to another directory.

Because of the similarities to a tree, such a structure is often referred to as a tree structure. This structure could more accurately be thought of as an upside-down bush rather than a tree, however, because no trunk exists. The tree is represented upside down, with the root at the top. Extending down from the root are the branches. Each branch grows out of only one branch, but it can have many lower branches. In this respect, it can be said to have a parent/child structure. In the same way, each directory is itself a subdirectory of one other directory. Each directory may contain many subdirectories but is itself the child of only one parent directory.

The Linux file structure branches into several directories beginning with a root directory, /. Within the root directory several system, directories contain files and programs that are features of the Linux system. The root directory also contains a directory called home that contains the home directories of all the users in the system. Each user’s home directory, in turn, contains the directories the user has made for their own use. Each of these could also contain directories. Such nested directories would branch out from the user’s home directory, as shown in Figure 10-2.

> NOTE The user’s home directory can be any directory, though it is usually the directory that bears the user’s login name. This directory is located in the directory named /home on your Linux system. For example, a user named dylan will have a home directory called dylan located in the system’s /home directory. The user’s home directory is a subdirectory of the directory called /home on your system.

# FIGURE 10-2
The Linux file structure beginning at the root directory

![](bbox=[0.35, 0.88, 0.88, 0.99])