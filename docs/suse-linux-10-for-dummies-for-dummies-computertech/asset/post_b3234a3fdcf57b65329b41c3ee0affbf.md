
![](img/b7e91b81e0d84c8a5261ee14a48991b2_106_0.png)

**Figure 6-9:** The Nautilus navigation window with a list view of the `/etc/X11` directory.

If you click any of the column headings — Name, Size, Type, or Date Modified — along the top of the list view, Nautilus sorts the list according to that column. For example, go ahead and click the Date Modified column heading. Nautilus now displays the list of files and directories sorted according to the time of their last modification. Clicking the Name column heading sorts the files and folders alphabetically.

## Manipulating files and directories in Nautilus

Not only can you move around different folders by using the Nautilus navigation window, you can also do things such as move a file from one folder to another or delete a file. I don’t outline each step — the steps are intuitive and similar to what you do in any GUI, such as Windows or Mac. Here are some of the things you can do in Nautilus:

- To move a file to a different folder, drag and drop the file’s icon on the folder where you want the file.
- To copy a file to a new location, select the file’s icon and choose Edit➜Copy File from the Nautilus menu. You can also right-click the file’s icon and choose Copy File from the context menu. Then move to the folder where you want to copy the file and choose Edit➜Paste Files.
- To delete a file or directory, right-click the icon, and choose Move to Trash from the context menu. (You can do this only if you have permission to delete the file.) To permanently delete the file, right-click the Trash icon on the desktop and choose Empty Trash from the context menu. Of course, do this only if you really want to delete the file. Once you choose Empty Trash, you are never going to see the file again. If you have to retrieve a file from the trash, double-click the Trash icon and then drag the file’s icon back to the folder where you want to save it. You can retrieve a file from the trash until you empty it.
- To rename a file or a directory, right-click the icon and choose Rename from the context menu. Then you can type the new name (or edit the name) in the text box that appears.
- To create a new folder, right-click an empty area of the window on the right and choose Create Folder from the context menu. After the new folder icon appears, you can rename it by right-clicking the icon and choosing Rename from the context menu. If you don’t have permission to create a folder, that menu item is grayed out.

## Using Linux Commands to Manipulate Files and Directories

Although GUI file managers such as Konqueror (in KDE) and Nautilus (in GNOME) are easy to use, you can use them only if you have a working GUI desktop. Sometimes, you may not have a graphical environment to run a graphical file manager. For example, you may be logged in through a text terminal, or the X Window System may not be working on your system. In those situations, you have to rely on Linux commands to work with files and directories. Of course, you can always use Linux commands, even in the graphical environment — all you have to do is open a terminal window and type the Linux commands.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_107_0.png)

To open a terminal window in KDE, click the terminal icon on the panel. In GNOME, choose Applications→System→Terminal→Gnome Terminal.

In the sections that follow, I briefly show some Linux commands for working with the files and directories.

### Commands for directory navigation

In Linux, when you log in as root, your home directory is /root. For other users, the home directory is usually in the /home directory. My home directory (when I log in as naba) is /home/naba. This information is stored in the /etc/passwd file. By default, only you have permission to save files in your home directory, and only you can create subdirectories in your home directory to further organize your files.

Linux supports the concept of a current directory, which is the directory on which all file and directory commands operate. After you log in, for example, your current directory is the home directory. To see the current directory, type the `pwd` command.

To change the current directory, use the `cd` command. To change the current directory to `/usr/lib`, type the following:

```bash
cd /usr/lib
```

Then, to change the directory to the cups subdirectory in `/usr/lib`, type this command:

```bash
cd cups
```

Now, if you use the `pwd` command, that command shows `/usr/lib/cups` as the current directory.

These two examples show that you can refer to a directory’s name in two ways:

- **An absolute pathname** (such as `/usr/lib`) that specifies the exact directory in the directory tree
- **A relative directory name** (such as `cups`, which represents the cups subdirectory of the current directory, whatever that may be)

If you type `cd cups` in `/usr/lib`, the current directory changes to `/usr/lib/cups`. However, if you type the same command in `/home/naba`, the shell tries to change the current directory to `/home/naba/cups`.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_108_0.png)

Use the `cd` command without any arguments to change the current directory back to your home directory. No matter where you are, typing **cd** at the shell prompt brings you back home!

![](img/b7e91b81e0d84c8a5261ee14a48991b2_108_1.png)

By the way, the tilde character (`~`) refers to your home directory. Thus the command `cd ~` also changes the current directory to your home directory. You can also refer to another user’s home directory by appending that user’s name to the tilde. Thus, `cd ~spiderman` changes the current directory to the home directory of spiderman.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_108_2.png)

Wait, there’s more. A single dot (`.`) and two dots (`..`) — often referred to as dot-dot — (clever, huh!) also have special meanings. A single dot (`.`) indicates the current directory, whereas two dots (`..`) indicate the parent directory. For example, if the current directory is `/usr/share`, you go one level up to `/usr` by typing

```bash
cd ..
```

### Commands for directory listings and permissions

You can get a directory listing by using the ls command. By default, the ls command — without any options — displays the contents of the current directory in a compact, multicolumn format. For example, type the next two commands to see the contents of the /etc/X11 directory:

```bash
cd /etc/X11
ls
```

The output looks like this (on the console, you see some items in different colors):

```text
fs             qt_gtk_font2fntrc  WindowMaker    xkb             xorg.conf.md5
fwm2           qt_plugins_3.3rc   xim            Xmodmap         xorg.conf.saxsave
kstylerc       qtrc               Xmodmap.remote Xresources
lbproxy        rstart             xim.d          xorg.conf       xserver
proxymngr      twm                xinit          xorg.conf.install xsm
```

From this listing (without the colors), you cannot tell whether an entry is a file or a directory. To tell the directories and files apart, use the -F option with ls like this:

```bash
ls -F
```

This time, the output gives you some more clues about the file types:

```text
fs/             qtrc             xinit/           xorg.conf.saxsave
fwm2/           rstart/           xkb/             Xresources
kstylerc        twm/              Xmodmap          xserver/
lbproxy/        WindowMaker/      Xmodmap.remote   xsm/
proxymngr/      xim/              xorg.conf@        
qt_gtk_font2fntrc  xim.d/         xorg.conf.install
qt_plugins_3.3rc  xim*             xorg.conf.md5
```

The output from ls -F shows the directory names with a slash (/) appended to them. Plain filenames appear as is. The at sign (@) appended to a file’s name (for example, notice the file named xorg.conf) indicates that this file is a link to another file. (In other words, this filename simply refers to another file; it’s a shortcut.) An asterisk (*) is appended to executable files. (xim, for example, is an executable file.) The shell can run any executable file.

You can see even more detailed information about the files and directories with the -l option:

```bash
ls -l
```
