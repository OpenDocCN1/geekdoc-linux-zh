
## Understanding file permissions

  After you've worked with Linux for a while, you are almost sure to get a Permission denied message. Permissions associated with files and directories in Linux were designed to keep users from accessing other users' private files and to protect important system files.

  The nine bits assigned to each file for permissions define the access that you and others have to your file. Permission bits appear as rwxrwxrwx. The first three bits apply to the owner's permission, the next three apply to the group assigned to the file, and the last three apply to all others. The r stands for read, the w stands for write, and the x stands for execute permissions. If a dash appears instead of the letter, it means that permission is turned off for that associated read, write, or execute.

  You can see the permission for any file or directory by typing the `ls -ld` command. The named file or directory appears as those shown in the following example:

```
$ ls -ld ch3 test
-rw-rw-r-- 1 chris sales 4983 Jan 18 22:13 ch3
drwxr-xr-x 2 chris sales 1024 Jan 24 13:47 test
```

  The first line shows a file (ch3) that has read and write permission for the owner and the group. All other users have read permission, which means they can view the file but cannot change its contents (although a user may be allowed to remove the file, since the ability to remove a file is based on directory permissions). The second line shows a directory (indicated by the letter d before the permission bits). The owner has read, write, and execute permission, while the group and other users have only read and execute permissions. As a result, only the owner can add, change, or delete files in that directory. Any other user, however, can only read the contents, change to that directory, and list the contents of the directory.

  If you own a file, you can change the permission on it as you please. You can do this with the `chmod` command. For each of the three sets of permission on a file (read, write, and execute), r is assigned to the number 4, w to 2, and x to 1. So to make permissions wide open for yourself as owner, you would set the first number to 7 (4 plus 2 plus 1). The same would be true for group and other permission. Any combination of permissions can result from 0 (no permission) through 7 (full permission).

  Here are some examples of how to change permission on a file and what the resulting permission would be:

```
chmod 777 files -> rwxrwxrwx
chmod 755 files -> rwxr-xr-x
chmod 644 files -> rw-r--r--
chmod 000 files -> ---------
```

  You can also turn file permissions on and off using plus (+) and minus (-) signs, respectively. This can be done for the owner user (u), owner group (g), others (o), and all users (a). For example, each time starting with a file that has all permissions open (rwxrwxrwx), here are some `chmod` examples with resulting permissions after using a minus sign:

```
chmod a-w files -> r-xr-xr-x
chmod o-x files -> rwxrwxr-w
chmod go-rwx files -> rw-------
```

  Likewise, here are some examples, starting with all permissions closed (---------) where the plus sign is used with `chmod` to turn permissions on:

```
chmod u+rw files -> rw-------
chmod a+x files -> ---x--X---
chmod ug+rx files -> -r-xrX---
```

  When you try to create a file, by default it is given the permission rw-r--r--. A directory is given the permission rwxr-xr-x. These default values are determined by the value of umask. Type umask to see what your umask value is. For example:

```
$ umask
022
```

  The umask value represents the permissions that are not given on a new file. It masks the permissions value of 666 for a file and 777 for a directory. The umask value of 022 results in permission for a directory of 755 (rwxr-xr-x). That same umask results in a file permission of 644 (rw-r--r--). (Execute permissions are off by default for regular files.)

> **TIP**: Here’s a great tip for changing the permission for lots of files at once. Using the `-R` option of chmod, you could change the permission for all of the files and directories within a directory structure at once. For example, if you wanted to open permissions completely to all files and directories in the `/tmp/test` directory, you could type the following:
> `$ chmod -R 777 /tmp/test`
> This command line runs chmod recursively (-R) for the `/tmp/test` directory, as well as any files or directories that exist below that point in the file system (for example, `/tmp/test/hat`, `/tmp/test/hat/caps`, and so on). All would be set to 777 (full read/write/execute permissions).

> **CAUTION**: The `-R` option of chmod works best if you are opening permissions completely or adding execute permission (as well as the appropriate read/write permission). The reason is that if you turn off execute permission recursively, you close off your ability to change to any directory in that structure. For example, `chmod -R 644 /tmp/test` turns off execute permission for the `/tmp/test` directory, then fails to change any files or directories below that point.

> **CROSS-REFERENCE**: If you are using Security Enhanced Linux, working with file permissions will be quite different than the method described here (with SELinux enabled). See Chapter 28 for more information.

## Moving, copying, and deleting files

  Commands for moving, copying, and deleting files are fairly straightforward. To change the location of a file, use the `mv` command. To copy a file from one location to another, use the `cp` command. To remove a file, use the `rm` command. Here are some examples:

```
$ mv abc def
$ mv abc -
$ cp abc def
$ cp abc -
$ rm abc
$ rm *
```

  Of the two move (`mv`) commands, the first moves the file `abc` to the file `def` in the same directory (essentially renaming it), whereas the second moves the file `abc` to your home directory (`-`). The first copy command (`cp`) copies `abc` to the file `def`, whereas the second copies `abc` to your home directory (`-`). The first remove command (`rm`) deletes the `abc` file; the second removes all the files in the current directory (except those that start with a dot).

> **NOTE**: For the root user, the `mv`, `cp`, and `rm` commands are aliased to each be run with the `-i` option. This causes a prompt to appear asking you to confirm each move, copy, and removal, one file at a time. This is done to prevent the root user from messing up a large group of files by mistake.

## Using the vi Text Editor

  It’s almost impossible to use Linux for any period of time and not need to use a text editor. If you are using a GUI, you can run `gedit`, which is fairly intuitive for editing text. Most Linux shell users will use either the `vi` or `emacs` commands to edit text files. The advantage of `vi` or `emacs` over a graphical editor is that you can use it from any shell, a character terminal, or a character-based connection over a network (using `telnet` or `ssh`, for example). No GUI is required.

  This section provides a brief tutorial of the `vi` text editor. Any time in this book that I suggest you manually edit a configuration file, use `vi` to do that editing (from any shell). (If `vi` doesn’t suit you, see the “Exploring Other Text Editors” sidebar for other options.)

  The `vi` editor is difficult to learn at first. But when you know it, you will be able to edit and move around quickly and efficiently within files. Your fingers never have to leave the keyboard to pick up a mouse or press a function key.

## Exploring Other Text Editors

  There are dozens of text editors available to use with Linux. Here are a few contained in Fedora that you can try out if you find `vi` to be too taxing:

- `gedit` — the GNOME text editor that runs in the GUI.
- `jed` — This screen-oriented editor was made for programmers. Using colors, jed can highlight code you create so you can easily read the code and spot syntax errors. Use the Alt key to select menus to manipulate your text.
- `joe` — The joe editor is similar to many PC text editors. Use control and arrow keys to move around. Type Ctrl+C to exit with no save or Ctrl+X to save and exit.
- `kate` — A nice-looking editor that comes in the kdebase package. It has lots of bells and whistles, such as highlighting for different types of programming languages and controls for managing word wrap.
- `kedit` — A GUI-based text editor that comes with the KDE desktop.
- `mcedit` — With mcedit, function keys help you get around, save, copy, move, and delete text. Like jed and joe, mcedit is screen-oriented.
- `nedit` — An excellent programmer's editor. You need to install the optional nedit package to get this editor.

  If you use ssh to log in to other Linux computers on your network, you can use any editor to edit files. A GUI-based editor will pop up on your screen. When no GUI is available, you will need a text editor that runs in the shell, such as vi, jed or joe.

## Starting with vi

  Most often, you start vi to open a particular file. For example, to open a file called /tmp/test, type the following command:

```
$ vi /tmp/test
```

  If this is a new file, you should see something similar to the following:

```
~
~
~
~
"/tmp/test" [New File]
```

  The box at the top represents where your cursor is. The bottom line keeps you informed about what is going on with your editing (here you just opened a new file). In between, there are tildes (~) as filler because there is no text in the file yet. Now here's the intimidating part: there are no hints, menus, or icons to tell you what to do. On top of that, you can't just start typing. If you do, the computer is likely to beep at you. And some people complain that Linux isn't friendly.
