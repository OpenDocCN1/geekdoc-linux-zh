
![](img/eef64cc01382a4448bc55a2ee7dcc4ca_96_0.png)

Figure 6-2
*A typical Linux pathname*

As you can see from Figure 6-2, a Linux pathname consists of the following parts:

- 1. The root directory, indicated by a forward slash (/) character
- 2. The directory hierarchy, with each directory name separated from the previous one by a forward slash (/) character. A / appears after the last directory name.
- 3. The filename, with a name and one or more optional extensions

Now that you know the basics of the Linux file system, you can explore the file system. You can access the files and directories in two ways:

- By using a graphical file manager in the GNOME or KDE desktop
- By typing appropriate Linux commands in a terminal window or a text console

This session covers both the graphical file manager and the Linux commands. The graphical file manager is similar to Windows Explorer and is intuitive to use. Now spend a few minutes exploring the file system using the GNOME file manager. (The KDE file manager works in a similar manner, so I don't cover it here.)

## Using the GNOME File Manager

After you log into your Red Hat Linux system from the graphical login screen, you can view your home directory with the GNOME file manager by double-clicking on the file folder icon on the desktop. Figure 6-3 shows the initial display of your home directory.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_97_0.png)

Figure 6-3
My home directory, as it appears in the GNOME file manager

### Viewing files with GNOME file manager

The GNOME file manager’s window is vertically divided into two windows. The left side shows a tree view of the file system in a scrolling window; the right side shows the files and directories in the currently selected directory with icons. As you can see from the tree view, Figure 6-3 shows the content of the /home/naba directory. The title bar shows the name of the currently selected directory.

If you have used Windows Explorer, you can use the GNOME file manager in a similar manner. To view the contents of another directory, first locate the directory in the tree view. For example, to view the /etc/X11 directory, click the plus sign (+) next to the etc directory. This causes the file manager to display the subdirectories in etc and change that plus sign to a minus sign. Now click the X11 directory. The right-hand side of the window now shows the contents of the /etc/X11 directory.

The GNOME file manager displays the contents of the selected directory using icons. Each directory appears as a folder with the name of the directory shown underneath the folder icon. Different files have different icons. Ordinary files appear as a sheet of paper. Directories appear as folders.

The GNOME file manager window has the usual menu bar and a toolbar. Notice that, in Figure 6-3, the toolbar button labeled Icons is pressed. That means the directory contents are displayed using large icons. Click the Brief button; this causes the file manager to display the contents using smaller icons in a list format.

To view more information about each file, click the Detailed button on the toolbar. The file manager now displays the size of each file or directory and the time when each was last modified. The detailed view shows the directory’s contents in a tabular form with three columns labeled Name, Size, and MTime. If you click any of the information titles — Name, Size, or MTime — along the top of the detailed view, the file manager sorts the list according to the information. For example, click the MTime information title. The file manager now displays the list of files and directories sorted according to the time of last modification, or the MTime. Clicking the Name information title sorts the files and directories alphabetically by name. This feature works in the Brief and Custom view as well.

Finally, you can view the file permissions by clicking the Custom button. The file manager then displays the icons, filenames, sizes, and file permissions.

For now, ignore the meaning of the permissions. You learn about them in the next section when I discuss the Linux commands that navigate the file system.

### Performing tasks with GNOME File Manager

In addition to moving around the file system and viewing contents of directories, you can use the file manager to perform tasks such as moving a file from one directory to another and deleting a file. I don’t show you each and every step, but you can take a few moments to try the following tasks:

- To move a file to a different directory, drag-and-drop the file’s icon on the directory where you want the file.
- To copy a file to a new location, select the file’s icon and then select File → Copy. You may also right-click the mouse on the file’s icon and select Copy from the pop-up menu. A dialog box prompts you for the name of the directory to which the file should be copied.
- To delete a file or directory, right-click the icon and select Delete from the pop-up menu. A dialog box asks you to confirm if you really want to delete the file or directory. You can click Yes to delete the selected item or click No to cancel the operation.
- To rename a file or a directory, click the name in the Icon view (see Figure 6-3). Then you can type the new name or edit the name.
- To create a new directory, right-click in an empty area of the right-hand window and select New Directory from the pop-up menu. A dialog box prompts you for the name of the new directory.
- To find files, select Commands → Find Files from the menu bar. A dialog box prompts you for what you want to find and where to start the search.

After you enter this information, click OK to start the search. The results of the search appear in a new window.

## Navigating and Manipulating Files and Directories with Linux Commands

Although the graphical file managers are easy to use, you can employ them only if you have a graphical login. Sometimes you may not have a graphical environment to run a graphical file manager. For example, you might be logged in through a text terminal or X might not work on your system. In these situations, you have to rely on Linux commands to work with files and directories. The nice part is that you can always use Linux commands — even in the graphical environment. All you have to do is open a terminal window and type the Linux commands. Click the terminal icon in the GNOME panel to start a terminal emulation program that displays a terminal window.

### Directory navigation

In Linux, your home directory is /root when you log in as root. For other users, the home directory is usually in the /home directory. My home directory (when I log in as naba) is /home/naba. This information is stored in the /etc/passwd file. By default, besides the super user, only you have permission to save files in your home directory and only you can create subdirectories in your home directory to further organize your files.

Linux supports the concept of a current directory, which is the directory in which all file and directory commands operate. After you log in, for example, your current directory is the home directory. To see the current directory from the terminal window, type the pwd command.

To change the current directory, use the cd command. To change the current directory to /usr/share/doc, type the following:

```
cd /usr/share/doc
```

Then, to change the directory to the bash-2.04 subdirectory in /usr/share/doc, type this command:

```
cd bash-2.04
```

Now, if you use the pwd command, that command shows /usr/share/doc/bash-2.04 as the current directory. Therefore, you can refer to a directory's name in two ways:

- An absolute pathname (such as /usr/share/doc) that specifies the exact directory in the directory tree
- A relative directory name (such as bash-2.04, which represents the bash-2.04 subdirectory of the current directory)

If you type cd bash-2.04 in /usr/share/doc, the current directory changes to /usr/share/doc/bash-2.04. However, the same command in /home/naba tries to change the current directory to /home/naba/bash-2.04, which probably does not exist. Incidentally, typing the cd command without any arguments changes the current directory to your home directory.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_100_0.png)

You can use a shortcut to refer to any user's home directory. Prefix a user's login name with a tilde (~) to refer to that user's home directory. Therefore, ~naba refers to the home directory of the user naba and ~root refers to the home directory of the root user. If your system has a user with the login name emily, you can type cd ~emily to change to Emily's home directory.

The directory names . and .. have special meanings. A single period (.) indicates the current directory, whereas two periods (..) indicate the parent directory. If the current directory is /usr/share/doc, for example, you can change the current directory to /usr/share by typing this command:

```
cd ..
```

Essentially, this command takes you up one level in the file system hierarchy.

### Directory listings and permissions

As you move around the Linux directories, you may want to know the contents of a directory. You can get a directory listing by using the ls command. By default, the ls command — without any options — displays the contents of the current directory in a compact, multicolumn format. For example, type the following commands to see the contents of the /etc/X11 directory. (Type the commands shown in boldface; I omitted the command prompts from the listing.)

```
cd /etc/X11
ls
```
