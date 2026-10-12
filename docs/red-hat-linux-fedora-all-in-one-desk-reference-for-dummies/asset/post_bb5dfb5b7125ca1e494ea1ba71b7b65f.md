
Use the cd command without any arguments to change the current directory back to your home directory. No matter where you are, typing cd at the shell prompt brings you back home!

By the way, the tilde character (~) refers to your home directory. Thus the command cd ~ also changes the current directory to your home directory. You can also refer to another user's home directory by appending that user's name to the tilde. Thus, cd ~superman changes the current directory to the home directory of superman.

Wait, there's more. A single dot (.) and two dots (..) — often referred to as dot-dot — also have special meanings. A single dot (.) indicates the current directory, whereas two dots (..) indicate the parent directory. For example, if the current directory is /usr/share, you go up one level to /usr by typing cd ..

## Commands for directory listings and permissions

You can get a directory listing by using the ls command. By default, the ls command — without any options — displays the contents of the current directory in a compact, multicolumn format. For example, type the next two commands to see the contents of the /etc/X11 directory:

```
cd /etc/X11
ls
```

The output looks like this (on the console you'd see some items in different colors):

```
applnk          prefdm          sysconfig       XftConfig.README-OBSOLETE  xserver
desktop-menus   proxymgr        twm             xinit                       xsm
fs              rstart          X               xkb
 gdm             serverconfig    xdm             Xmodmap
lxbproxy        startthere      XF86Config      Xresources
```

From this listing (without the colors), you cannot tell whether an entry is a file or a directory. To tell the directories and files apart, use the -F option with ls and you'll get more clues:

```
ls -F
applnk/         prefdm*         sysconfig/      XftConfig.README-OBSOLETE  xserver/
desktop-menus/  proxymgr/       twm/            xinit/                      xsm/
fs/             rstart/         X@              xkb@
gdm/            serverconfig/   xdm/            Xmodmap
lxbproxy/       startthere      XF86Config      Xresources
```

The output from ls -F shows the directory names with a slash (/) appended to them. Plain filenames appear as is. The at sign (@) appended to the file named X indicates that this file is a link to another file (in other words, this filename simply refers to another file; it's a shortcut). An asterisk (*) is appended to executable files (see, for example, the prefdm file in the listing). The shell can run any executable file.

You can see even more detailed information about the files and directories with the -l option:

```
ls -l
```

For the /etc/X11 directory, a typical output from ls -l looks like the following:

```
total 80
drwxr-xr-x 4 root root 4096 Sep 24 15:52 applnk
drwxr-xr-x 2 root root 4096 Sep 24 14:59 desktop-menus
drwxr-xr-x 2 root root 4096 Sep 24 16:12 fs
drwxr-xr-x 6 root root 4096 Sep 24 15:37 gdm
drwxr-xr-x 2 root root 4096 Sep 24 15:34 lxbproxy
-rwxr-xr-x 1 root root 1298 Sep 4 13:23 prefdm
drwxr-xr-x 2 root root 4096 Sep 24 15:34 proxymgr
drwxr-xr-x 4 root root 4096 Sep 24 15:34 rstart
drwxr-xr-x 2 root root 4096 Jul 10 2001 serverconfig
drwxr-xr-x 2 root root 4096 Jul 10 2001 startthere
drwxr-xr-x 2 root root 4096 Jul 10 2001 sysconfig
drwxr-xr-x 2 root root 4096 Sep 24 15:36 twm
lrwxrwxrwx 1 root root 27 Sep 24 16:28 X -> ../usr/X11R6/bin/XFree86
drwxr-xr-x 3 root root 4096 Sep 24 15:56 xdm
-rw-r--r-- 1 root root 3323 Sep 24 16:20 XF86Config
< lines deleted >
drwxr-xr-x 2 root root 4096 Sep 24 15:34 xsm
```

This listing shows considerable information about every directory entry — each of which can be a file or another directory. Looking at a line from the right column to the left, you see that the rightmost column shows the name of the directory entry. The date and time before the name show when the last modifications to that file were made. To the left of the date and time is the size of the file, in bytes.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_195_0.png)

The file's group and owner appear to the left of the column that shows the file size. The next number to the left indicates the number of links to the file. (A link is like a shortcut in Windows.) Finally, the leftmost column shows the file's permission settings, which determine who can read, write, or execute the file.

The first letter of the leftmost column has a special meaning, as the following list shows:

- If the first letter is l, the file is a symbolic link (a shortcut) to another file.
- If the first letter is d, the file is a directory.
- If the first letter is a dash (-), the file is normal.
- If the first letter is b, the file represents a block device, such as a disk drive.
- If the first letter is c, the file represents a character device, such as a serial port or a terminal.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_196_0.png)

After that first letter, the leftmost column shows a sequence of nine characters. This appears as `rwxrwxrwx` when each letter is present. Each letter indicates a specific permission. A hyphen (-) in place of a letter indicates no permission for a specific operation on the file. Think of these nine letters as three groups of three letters (rwx), interpreted as follows:

- The leftmost group of rwx controls the read, write, and execute permission of the file's owner. In other words, if you see rwx in this position, the file's owner can read (r), write (w), and execute (x) the file. A hyphen in place of a letter indicates no permission. Thus the string rw- means the owner has read and write permission but no execute permission. Although executable programs (including shell programs) typically have execute permission, directories treat execute permission as equivalent to use permission — a user must have execute permission on a directory before he or she can open and read the contents of the directory.
- The middle three rwx letters control the read, write, and execute permission of any user belonging to that file's group.
- The rightmost group of rwx letters controls the read, write, and execute permission of all other users (collectively referred to as the world).

Thus, a file with the permission setting `rwx------` is accessible only to the file's owner, whereas the permission setting `rwxr-xr--` makes the file readable by the world.

An interesting feature of the `ls` command is that it does not list any file whose name begins with a period. To see these files, you must use the `ls` command with the `-a` option, as follows:

```
ls -a
```

Try this command in your home directory (and then compare the result with what you see when you don't use the -a option):

- 1. Type cd to change to your home directory.
- 2. Type ls -F to see the files and directories in your home directory.
- 3. Type ls -aF to see everything, including the hidden files.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_197_0.png)

Most Linux commands take single-character options, each with a minus sign (think of this sign as a hyphen) as a prefix. When you want to use several options, type a hyphen and concatenate (string together) the option letters, one after another. Thus, ls -al is equivalent to ls -a -l as well as ls -a -l.

## Commands for changing permissions and ownerships

You may need to change a file's permission settings to protect it from others. Use the chmod command to change the permission settings of a file or a directory.

To use chmod effectively, you have to learn how to specify the permission settings. A good way is to concatenate letters from the columns of Table 4-4 in the order shown (Who/Action/Permission).

Note: You use only the single character from each column — the text in parentheses is for explanation only.

Table 4-4 Letter Codes for File Permissions

| Who | Action | Permission |
|---|---|---|
| u (user) | + (add) | r (read) |
| g (group) | - (remove) | w (write) |
| o (others) | = (assign) | x (execute) |
| a (all) | s (set user ID) |  |

For example, to give everyone read access to all files in a directory, pick a (for all) from the first column, + (for add) from the second column, and r (for read) from the third column to come up with the permission setting a+r. Then use the whole set of options with chmod, like this:

```
chmod a+r *.
```

On the other hand, to permit everyone to execute one specific file, type

```
chmod a+x filename
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_197_1.png)

Suppose you have a file named mystuff that you want to protect. You can make it accessible to no one but you if you type the following commands, in this order:

```
chmod a-rwx mystuff
```

```
chmod u+rw mystuff
```
