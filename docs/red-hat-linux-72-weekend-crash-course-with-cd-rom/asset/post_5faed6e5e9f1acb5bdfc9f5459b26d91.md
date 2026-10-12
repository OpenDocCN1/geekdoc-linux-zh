
Then, to change the directory to the `bash-2.04` subdirectory in `/usr/share/doc`, type this command:

```
cd bash-2.04
```

Now, if you use the `pwd` command it shows `/usr/share/doc/bash-2.04` as the current directory. Therefore, you can refer to a directory's name in two ways:

- *Absolute pathname* (such as `/usr/share/doc`), which specifies the exact directory in the directory tree.
- *Relative directory name* (such as `bash-2.04`), which represents the `bash-2.04` subdirectory of the current directory.

If you type `cd bash-2.04` in `/usr/share/doc`, the current directory changes to `/usr/share/doc/bash-2.04`. However, the same command in `/home/naba` tries to change the current directory to `/home/naba/bash-2.04`, which probably does not exist. Incidentally, typing the `cd` command without any arguments changes the current directory to your home directory.

![](img/5fe8f856723cde0b366f73584b9e64b8_75_0.png)

> You can use a shortcut to refer to any user's home directory. Prefix a user's login name with a tilde (~) to refer to that user's home directory. Therefore, `~kwil` refers to the home directory of the user `kwil1` and `~root` refers to the home directory of the root user. If your system has a user with the login name `emily`, you can type `cd ~emily` to change to Emily's home directory.

The directory names `.` and `..` have special meanings. A single period (`.`) refers to the current directory, whereas two periods (`..`) refer to the parent directory. If the current directory is `/usr/share/doc`, for example, you can change the current directory to `/usr/share` by typing this command:

```
cd ..
```

This command takes you up one level in the directory hierarchy.

# **Directory listings and permissions**

As you move around the Linux directories, you may want to know their contents. You can get a directory listing by typing the `ls` command. By default, the `ls` command—without any options—displays the contents of the current directory in a compact, multicolumn format. For example, type the following commands to see the contents of the `/etc/X11` directory. (Type the commands shown in bold text; the command prompts are not included in the listing.)

```
**cd /etc/X11**
ls
```

applink      lbxproxy     rstart    xdm      XftcConfig    Xmodmap
fs           pprefdm      twm       XF86Config xinit       xserver
gdm         proxyngmr    X         XF86Config X kbxy      xsm

From this listing, you can't tell whether an entry is a file or a directory. To distinguish the directories from the files, use the `-F` option with `ls` as follows:

![](img/5fe8f856723cde0b366f73584b9e64b8_76_0.png)

The `-F` option causes `ls` to append a character to the end of certain files that indicates their type. For example, directory names have a slash (`/`) appended to them. Plain filenames appear as is. An at sign (`@`) indicates that a file, such as `xkb` in the listing, is actually a link to another file.

![](img/5fe8f856723cde0b366f73584b9e64b8_76_1.png)

A link is a filename that refers to another file. It's like a shortcut in Windows.

An asterisk (`*`) is appended to executable files (for example, the `prefdm` file in the listing).

![](img/5fe8f856723cde0b366f73584b9e64b8_76_2.png)

The exact files you see may vary slightly depending on the kind of installation you performed during Friday night's session.

You can see even more detailed information about the files and directories with the `-l` option:

```
ls -l
```

For the `/etc/X11` directory, a typical output from `ls -l` looks like the following:

![](img/5fe8f856723cde0b366f73584b9e64b8_76_3.png)

This listing shows considerable information about each directory entry, which can be a file or another directory. Looking at a line from the right column to the left, you see that the rightmost column shows the name of the directory entry. The date and time before the name shows its MTime, when it was last modified. The file size, in bytes, appears before the MTime.

The file's group and owner appear to the left of the file size column. The next number to the left indicates the number of links to the file or, if the entry is a directory, the number of files it contains (including `.` and `..`). Finally, the leftmost column shows the file's permission settings, which control who can read, write, or execute the file. The very first letter of the permission setting has one of the following special meanings:

- If the first letter is `l`, the file is a symbolic link to another file.
- If the first letter is `d`, the file is a directory.
- If the first letter is a dash (`-`), the file is a normal file.
- If the first letter is `b`, the file represents a block device such as a disk drive.
- If the first letter is `c`, the file represents a character device such as a serial port or a terminal.

After that first letter, the leftmost column shows a sequence of nine characters that appears as `rwxrwxrwx` when each letter is present. Each letter indicates a specific permission: read (`r`), write (`w`), and execute (`x`). A hyphen (`-`) in place of a letter indicates no permission for a specific operation on the file. Thus, the string `rw-` means that the owner has read and write permission, but no execute permission. Think of these nine letters as three groups of three letters (`rwx`), interpreted as follows:

- The leftmost group of `rwx` controls the read, write, and execute permission of the file's owner.
- The middle three `rwx` letters control the read, write, and execute permission of any user belonging to that file's group.
- The rightmost group of `rwx` letters controls the read, write, and execute permission of all other users (collectively referred to as the world).

Thus, a file with the permission setting `rwx-------` is accessible only to the file's owner. Meanwhile, the permission setting `rwxr-r---` makes the file readable by the world.

> Note Typically, executable programs (including shell programs) have execute permission. However, for directories, the execute permission is equivalent to a use permission—a user must have execute permission on a directory to list its contents.

An interesting feature of the `ls` command is the fact that it does not list any file whose name begins with a period. Such files are called *hidden files* or *dot files* because their names begin with a dot (`.`). To see these files, you must use the `ls` command with the `-a` option as follows:

```
ls -a
```

# File manipulation

You might want to copy files from one directory to another. To do so, use the `cp` command to perform this task. The `cp` command makes a *new copy* of a file, leaving the original intact. To copy the file `/usr/X11R6/lib/X11/xinit/Xclients` to the `Xclients.sample` file in the current directory (such as your home directory), type the following:

```
cp /usr/X11R6/lib/X11/xinit/Xclients Xclients.sample
```

If you want to copy a file to the current directory and retain the same name, use a period (`.`) as the second argument of the `cp` command. Thus, the following command copies the `XF86Config` file from the `/etc/X11` directory to the current directory (denoted by a single period):

```
cp /etc/X11/XF86Config .
```

Another Linux command, `mv`, moves a file to a new location. The original copy is gone, and a new copy appears at the specified destination. You can use `mv` to rename a file. If you want to change the name of `today.list` to `old.list`, use the `mv` command as follows:

```
mv today.list old.list
```

On the other hand, you can move the `today.list` file to a subdirectory named `saved` with this command:

```
mv today.list saved
```

Another common file operation is deleting a file. Use the `rm` command to delete a file named `old.list`, for example, by typing the following command:

```
rm old.list
```

![](img/5fe8f856723cde0b366f73584b9e64b8_78_0.png)

> Be careful with the `rm` command, particularly when you log in as root.
> Inadvertently deleting important files with `rm` is very easy.

In addition to copying, renaming, and deleting files, you may want to view a file’s contents. Use the `more` command to look at a text file one page at a time. To view the file `/etc/X11/XF86Config-4`, for example, use this command:

```
more /etc/X11/XF86Config-4
```

The `more` command pauses after each page, so you have to press the spacebar to move to the next page. Press Enter to move forward one line at a time in the file. To move to the previous page, press `b`.

Another useful Linux command for file viewing is `less`. The name is a play on words because `less` does more than `more`, that is, `less` has a richer set of features for viewing files than does `more`.

# Directory manipulation

To organize files in your home directory, you have to create new directories or subdirectories. Use the `mkdir` command to create a directory. For example, to create a directory named `images` in the current directory, type the following:

```
mkdir images
```

After you create the directory, you can use the `cd images` command to change to that directory.

When you no longer need a directory, use the `rmdir` command to delete it. You can delete a directory only when the directory is empty.

![](img/5fe8f856723cde0b366f73584b9e64b8_78_1.png)

> To delete a directory and its files simultaneously, use the `rm` command’s recursive option, `-r`. So, to delete the `images` directory and all of its files with a single command, type `rm -r images`.
