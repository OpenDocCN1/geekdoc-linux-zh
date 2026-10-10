
## Viewing files and folders

When you click a folder icon on the KDE desktop, Konqueror starts automatically and opens that folder. For example, click the My Computer icon in the upper-left corner of the KDE desktop in SUSE Linux. Konqueror runs and displays the contents of your computer. Click the Home Folder icon on the vertical toolbar in the left edge of the Konqueror window and then click Home Folder on the middle pane. Konqueror displays the contents of your home directory (think of a directory as a folder that can contain other files and folders) in its main window. Figure 3-6 shows a typical user’s home directory in Konqueror.

![](img/11709a8f88c8cd03868a929dc94c0e2b_216_0.png)

If you’ve used Windows Explorer, you can use Konqueror in a similar manner.

The Konqueror window is vertically divided into three parts:

- A narrow left pane shows icons you can click to perform various tasks in Konqueror.
- A wider middle pane (that can be toggled on or off) shows a tree view of the current folder.
- The widest pane (at the right) uses icons to show the files and folders in the current folder.

Konqueror uses different types of icons for different files and shows a preview of each file’s contents. For image files, the preview is a thumbnail version of the image.

The Konqueror window’s title bar shows the name of the currently selected directory. The Location text box (along the top of the window) shows the full name of the directory — in this case, Figure 3-6 shows the contents of the /home/naba directory.

Use the leftmost vertical row of buttons to select other things to browse. When you click one of these buttons, the middle pane displays a tree menu of items that you can browse. For example, to browse other parts of the file system, do the following:

1. From the leftmost vertical column of icons in the Konqueror window (refer to Figure 3-6), click the Root Folder icon (the second icon from the bottom). A tree menu of directories appears in the middle pane.
2. In the tree view, locate the folder that you want to browse. For example, to look at the /etc folder, click the plus sign next to the /etc folder. Konqueror displays the other folders and changes the plus sign to a minus sign.
3. To view the contents of the X11 subdirectory, scroll down and click X11. The pane on the right now shows the contents of the /etc/X11 directory.

Konqueror displays the contents of a folder using different types of icons. Each directory appears as a folder, with the name of the directory shown underneath the folder icon. Ordinary files appear as a sheet of paper.

The Konqueror window has the usual menu bar and a toolbar. You can view the files and folders in other formats as well. For example, choose View→: View Mode→: Detailed List View to see the folder’s contents with smaller icons in a list format (see Figure 3-7), along with detailed information (such as the size of each file or directory, and at what time each was last modified).

If you click any of the column headings — Name, Size, File Type, or Modified, to name a few — along the top of the list view, Konqueror sorts the list according to that column. For example, if you click the Modified column heading, Konqueror displays the list of files and folders sorted according to the time of last modification. Clicking the Name column heading sorts the files and directories alphabetically by name.

Not only can you move around different folders by using Konqueror, you can also do things such as move a file from one folder to another or delete a file. I don’t outline each step because the steps are intuitive and similar to what you do in any GUI (such as Windows or the Mac interface). Here are some things you can do in Konqueror:

- **View a text file**: Click the filename, and Konqueror runs the KWrite word processor, displaying the file in a new window.
- **Copy or move a file to a different folder:** Drag and drop the file’s icon on the folder where you want the file to go. A menu pops up and asks you whether you want to copy, move, or simply link the file to that directory.
- **Delete a file or directory:** Right-click the icon and choose Move to Trash from the context menu. To permanently delete the file, right-click the Trash icon on the desktop and choose Empty Trash from the context menu. Of course, do this only if you really want to delete the file. When you Empty Trash, the deleted files are really gone forever. If you want to recover a file from the trash, double-click the Trash icon on the desktop and from that window drag and drop the file icon into the folder where you want to save the file. When asked whether you want to copy or move, select Move. You can recover files from the trash until the moment you empty the trash.
- **Rename a file or a directory:** Right-click the icon and choose Rename from the context menu. Then you can type the new name (or edit the old name) in the text box that appears.
- **Create a new folder:** Choose View•View Mode•Icon View. Then right-click an empty area of the rightmost pane and choose Create New• Directory from the context menu. Then type the name of the new directory and click OK. (If you don’t have permission to create a directory, you get an error message.)

![](img/11709a8f88c8cd03868a929dc94c0e2b_218_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_218_1.png)

## 194 Navigating the File System with Linux Commands

### Viewing Web pages

Konqueror is much more than a file manager. With it, you can view a Web page as easily as you can view a folder. Just type a Web address in the Location text box and see what happens. For example, Figure 3-8 shows the Konqueror window after I type www.irs.gov in the Location text box on the toolbar and press Enter.

![](img/11709a8f88c8cd03868a929dc94c0e2b_219_0.png)

**Figure 3-8:** Konqueror can browse the Web as well.

Konqueror displays the Web site in the pane on the right. The left pane doesn’t change.

## Navigating the File System with Linux Commands

Although GUI file managers such as Nautilus (in GNOME) or Konqueror (in KDE) are easy to use, you can use them only if you have a working GUI desktop. Sometimes, you may not have a graphical environment to run a graphical file manager. For example, you may be logged in through a text terminal, or X may not be working on your system. In those situations, you have to rely on Linux commands to work with files and directories. Of course, you can always use Linux commands, even in the graphical environment — all you have to do is open a terminal window and type the Linux commands.

In the sections that follow, I briefly show some Linux commands for moving around the Linux file system.

### Commands for directory navigation

In Linux, when you log in as *root*, your home directory is `/root`. For other users, the home directory is usually in the `/home` directory. My home directory (when I log in as *naba*) is `/home/naba`. This information is stored in the `/etc/passwd` file. By default, only you have permission to save files in your home directory, and only you can create subdirectories in your home directory to further organize your files.

Linux supports the concept of a *current* directory, which is the directory on which all file and directory commands operate. After you log in, for example, your current directory is the home directory. To see the current directory, type the `pwd` command.

To change the current directory, use the `cd` command. To change the current directory to `/usr/lib`, type the following:

```
cd /usr/lib
```

Then, to change the directory to the *cups* subdirectory in `/usr/lib`, type this command:

```
cd cups
```

Now, if you use the `pwd` command, that command shows `/usr/lib/cups` as the current directory.

These two examples show that you can refer to a directory's name in two ways:

- An absolute pathname (such as `/usr/lib`) that specifies the exact directory in the directory tree
- A relative directory name (such as *cups*, which represents the *cups* subdirectory of the current directory, whatever that may be)

If you type `cd cups` in `/usr/lib`, the current directory changes to `/usr/lib/cups`. However, if I type the same command in `/home/naba`, the shell tries to change the current directory to `/home/naba/cups`.

![](img/11709a8f88c8cd03868a929dc94c0e2b_220_0.png)

Use the `cd` command without any arguments to change the current directory back to your home directory. No matter where you are, typing `cd` at the shell prompt brings you back home!
[/content]
