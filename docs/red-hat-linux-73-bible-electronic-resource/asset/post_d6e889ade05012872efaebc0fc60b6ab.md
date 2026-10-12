
grape
grapefruit
$ ls g*t
grapefruit
$ ls *e**
apple grape grapefruit watermelon
$ ls *n*
banana watermelon

The first example matches any file that begins with an a (apple). The next example matches any files that begin with g (grape, grapefruit). Next, files beginning with g and ending in t are matched (grapefruit). Next, any file that contains an e in the name is matched (apple, grape, grapefruit, watermelon). Finally, any file that contains an n is matched (banana, watermelon).

Here are a few examples of pattern matching with the question mark (?:)

$ ls ????e
apple grape
$ ls g???e*
grape grapefruit

The first example matches any five-character file that ends in e (apple, grape). The second example matches any file that begins with g and has e as its fifth character (grape, grapefruit).

Here are a few examples of using braces to do pattern matching:

$ ls [abw]*
apple banana watermelon
$ ls [agw]*[ne]
apple grape watermelon

In the first example, any file beginning with a, b, or w is matched. In the second, any file that begins with a, g, or w and also ends with either n or e is matched.

## Using file-redirection metacharacters

Commands receive data from standard input and send it to standard output. Using pipes (described earlier), you can direct standard output from one command to the standard input of another. With files, you can use less than (<) and greater than (>) signs to direct data to and from files. Here are the file redirection characters:

- < — Direct the contents of a file to the command.
- > — Direct the output of a command to a file, deleting the existing file.
- >> — Direct the output of a command to a file, adding the output to the end of the existing file.

Here are some examples of command lines where information is directed to and from files:

$ mail root < ~/.bashrc
$ nroff -man /usr/share/man/man1/chmod.1* > /tmp/chmod
$ echo "I finished the project on $(date)" > ~/projects

In the first example, the contents of the `.bashrc` file in the home directory are sent in a mail message to the computer's *root* user. The second command line formats the `chmod` man page (using the `nroff` command) and sends the output to the file `/tmp/chmod` (erasing the previous `/tmp/chmod` file, if it existed). The final command results in the following text being added to the user's project file:

I finished the project on Sun Nov 25 13:46:49 PST 2001

### Understanding file permissions

After you've worked with Linux for a while, you are almost sure to get a *Permission Denied* message. Permissions associated with files and directories in Linux were designed to keep users from accessing other users' private files and to protect important system files.

The nine bits assigned to each file for permissions define the access that you and others have to your file. Permission bits appear as `rwxrwxrwx`. The first three bits apply to the owner's permission, the next three apply to the owner's group, and the last three apply to all others. The `r` stands for *read*, the `w` stands for *write*, and the `x` stands for *execute permissions*. If a dash appears instead of the letter, it means that permission is turned off for that associated read, write, or execute.

You can see the permission for any file or directory by typing the `ls -ld` command. The named file or directory appears as those shown in the example below:

$ ls -ld ch3 test
-rw-r--r-- 1 chris sales  4983 Jan 18 22:13 ch3
drwxr-xr-x 2 chris sales  1024 Jan 24 13:47 test

The first line shows a file (`ch3`) that has read and write on for the owner and the group. All other users have read permission, which means they can view the file but cannot change its contents or remove it. The second line shows a directory (indicated by the letter `d` before the permission bits). The owner has read, write, and execute permission, while the group and other users have only read and execute permissions. As a result, only the owner can add, change, or delete files in that directory. Any other user, however, can only read the contents, change to that directory, and list the contents of the directory.

If you own a file, you can change the permission on it as you please. You can do this with the `chmod` command. For each of the three sets of permission on a file (read, write, and execute), the `r` is assigned to the number 4, `w` to 2, and `x` to 1. So to make permissions wide open for yourself as owner, you would set the first number to 7 (4 plus 2 plus 1). The same would be true for group and other permission. Any combination of permissions can result from 0 (no permission) through 7 (full permission).

Here are some examples of how to change permission on a file and what the resulting permission would be:

| Command | Resulting Permissions |
| :--- | :--- |
| chmod 777 files | -rw-rwxrwx |
| chmod 755 files | -rw-r-x-rx |
| chmod 644 files | -rw-r--r-- |
| chmod 000 files | ---------- |

When you try to create a file, by default it is given the permission rw-r--r--. A directory is given the permission rwxr-xr-x. These default values are determined by the value of umask. Type umask to see what your umask value is. For example:

$ umask
022

Subtract the number you see in each of the three sets from seven and you will see the value of each of the fields. The umask of 022 results in permission for a directory of 755 (rwxr-xr-x). That same umask results in a file permission of 644 (rw-r--r--). (Execute permissions are off by default for regular files.)

> **TIP:** Here's a great tip for changing the permission for lots of files at once. Using the -R option of chmod, you could change the permission for all of the files and directories within a directory structure at once. For example, if you wanted to open permissions completely to all files and directories in the /tmp/test directory, you could type the following:
> 
> $ chmod -R 777 /tmp/test
> 
> This command line runs chmod recursively (-R) for the /tmp/test directory, as well as any files or directories that exist below that point in the file system (for example, /tmp/test/hat, /tmp/test/hat/baseballcaps, and so on). All would be set to 777 (full read/write/execute permissions).

> **CAUTION:** The -R option of chmod works best if you are opening permissions completely or adding execute permission (as well as the appropriate read/write permission). The reason is that if you turn off execute permission recursively, you close off your ability to change to any directory in that structure. For example, chmod -R 644 /tmp/test turns off execute permission for the /tmp/test directory, then fails to change any files or directories below that point.

## Moving, copying, and deleting files

Commands for moving, copying, and deleting files are fairly straightforward. To change the location of a file, use the mv command. To copy a file from one location to another, use the cp command. To remove a file, use the rm command. Here are some examples:

$ mv abc def
$ mv abc -
$ cp abc def
$ cp abc -
$ rm abc
$ rm *

Of the two move (mv) commands, the first moves the file abc to the file def in the same directory (essentially renaming it), whereas the second moves the file abc to your home directory (~). The first copy command (cp) copies abc to the file def, whereas the second copies abc to your home directory (~). The first remove command (rm) deletes the abc file, whereas the second removes all the files in the current directory.

> **NOTE:** For the root user, the mv, cp, and rm commands are aliased to each be run with the -i option. This causes a prompt to appear asking you to confirm each move, copy, and removal, one file at a time. This is done to prevent the root user from messing up a large group of files by mistake.

## Using the vi Text Editor

It's almost impossible to use Red Hat Linux for any period of time and not need to use a text editor. If you are using a GUI, you can run xedit, which has a fairly intuitive interface for editing text. Most Red Hat Linux shell users will use either the vi or emacs commands to edit plain-text files. The advantage of using vi or emacs, instead of a graphical editor, is that you can use it from a Terminal window, a character terminal, or a character-based connection over a network (using telnet or ssh, for example). No GUI is required.

This section provides a brief tutorial of the vi text editor. Any time in this book that I suggest you manually edit a configuration file, you can use vi to do that editing (from any shell prompt). The vi editor is difficult to learn at first. But when you know it, you will be able to edit and move files around quickly and efficiently. Your fingers never have to leave the keyboard to pick up a mouse or hit a function key.

## Starting with vi

Most often, you start vi to open a particular file. For example, to open a file called /tmp/test, type the following command:

$ vi /tmp/test

If this is a new file, you should see something similar to the following:

~
~
~
~
~
~
~
~
~
"/tmp/test" [New File]
