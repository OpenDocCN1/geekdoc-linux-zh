
Occasionally, you may need to create directories and subdirectories in "bulk." To do this, add the -p option to the `mkdir` command as shown here:

```bash
$ mkdir -p New_Dir/SubDir/UnderDir
$ ls -R New_Dir
New_Dir:
SubDir

New_Dir/SubDir:
UnderDir

New_Dir/SubDir/UnderDir:
$
```

The -p option on the `mkdir` command makes any missing *parent directories* as needed. A parent directory is a directory that contains other directories at the next level down the directory tree.

Of course, after you make something, you need to know how to delete it. This is especially useful if you created a directory in the wrong location.

## Deleting directories

Removing directories can be tricky, and for good reason. There are lots of opportunities for bad things to happen when you start deleting directories. The shell tries to protect us from accidental catastrophes as much as possible.

The basic command for removing a directory is `rmdir`:

```bash
$ mkdir Wrong_Dir
$ touch Wrong_Dir/newfile
$
$ rmdir Wrong_Dir/
rmdir: failed to remove 'Wrong_Dir/': Directory not empty
$
```

By default, the `rmdir` command works only for removing *empty* directories. Because we created a file, `newfile`, in the `Wrong_Dir` directory, the `rmdir` command refuses to remove it.

To use `rmdir` to remove this directory, we must remove the file first.

Then we can use the `rmdir` command on the now empty directory:

```bash
$ rm -i Wrong_Dir/newfile
rm: remove regular empty file 'Wrong_Dir/newfile'? y
$ rmdir Wrong_Dir/
$ ls Wrong_Dir
ls: cannot access 'Wrong_Dir': No such file or directory
$
```

The `rmdir` command has no `-i` option to ask if you want to remove the directory. This is one reason it is helpful that `rmdir` removes only empty directories.

You can also use the `rm` command on entire nonempty directories. Using the `-r` option allows the command to descend into the directory, remove the files, and then remove the directory itself:

```bash
$ mkdir TestDir
$ touch TestDir/fileone TestDir/filetwo
$ ls TestDir
fileone filetwo
$ rm -ir TestDir
rm: descend into directory 'TestDir'? y
rm: remove regular empty file 'TestDir/fileone'? y
rm: remove regular empty file 'TestDir/filetwo'? y
rm: remove directory 'TestDir'? y
$ ls TestDir
ls: cannot access 'TestDir': No such file or directory
$
```

This also works for descending into multiple subdirectories and is especially useful when you have lots of directories and files to delete:

```bash
$ touch New_Dir/testfile
$ ls -FR New_Dir
New_Dir:
SubDir/ testfile

New_Dir/SubDir:
UnderDir/

New_Dir/SubDir/UnderDir:
$
$ rm -iR New_Dir
rm: descend into directory 'New_Dir'? y
rm: descend into directory 'New_Dir/SubDir'? y
rm: remove directory 'New_Dir/SubDir/UnderDir'? y
rm: remove directory 'New_Dir/SubDir'? y
rm: remove regular empty file 'New_Dir/testfile'? y
rm: remove directory 'New_Dir'? y
$
```

Although this works, it’s somewhat awkward. Notice that you still must verify each and every file that gets removed. For a directory with lots of files and subdirectories, this can become tedious.

> **NOTE**
>
> For the `rm` command, the `-r` parameter and the `-R` parameter work exactly the same — it recursively traverses through the directory removing files. It is unusual for a shell command to have different cased parameters with the same function.

The ultimate solution for quickly deleting a directory tree is the `rm -rf` command. It gives no warnings and no messages, and it just deletes the directory specified and all its contents. This, of course, is an extremely dangerous tool to have. Use it sparingly, and only after triple checking to make sure that you’re doing exactly what you want to do!

In the last few sections, we looked at managing both files and directories. So far we’ve covered everything you need to know about files, except for how to peek inside them.

## Viewing File Contents

You can use several commands for looking inside files without having to pull out a text editor utility (see *Chapter 10*, “Working with Editors”). This section demonstrates a few of those commands.

### Viewing the file type

Before you go charging off trying to display a file, you need to get a handle on what type of file it is. If you attempt to display a binary file, you may get lots of gibberish on your screen and possibly even lock up your terminal emulator.

The `file` command is a handy little utility to have around. It can peek inside a file and determine just what kind of file it is:

```bash
$ file .bashrc
.bashrc: ASCII text
$
```

The file in the preceding example is a text file. The `file` command determined not only that the file contains text but also the character code format of the text file, ASCII.

This following example shows a file that is simply a directory. Thus, the `file` command gives you another method to distinguish a directory:

```bash
$ file Documents
Documents/: directory
$
```

This third `file` command example shows a file that is a symbolic link. Note that the `file` command even tells you to which file it is symbolically linked:

```bash
$ file slink_test_file
slink_test_file: symbolic link to test_file
$
```

The following example shows what the `file` command returns for a script file. Although the file is `ASCII text`, because it's a script file, you can execute (run) it on the system:

```bash
$ file my_script
my_script: Bourne-Again shell script, ASCII text executable
$
```

The final example is a binary executable program. The `file` command determines the platform that the program was compiled for and what types of libraries it requires. This is an especially handy feature if you have a binary executable program from an unknown source:

```bash
$ file /usr/bin/ls
/usr/bin/ls: ELF 64-bit LSB shared object, x86-64, version 1
(SYSV),
dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2,
for GNU/Linux 3.2.0, [...] $
```

Now that you know a quick method for viewing a file's type, you can start displaying and viewing files.

### Viewing the whole file

If you have a large text file on your hands, you may want to be able to see what's inside it. Linux has three different commands that can help you here.

#### Using the cat command

The `cat` command is a handy tool for displaying all the data inside a text file:

```bash
$ cat test_file
Hello World
Hello World again
Hello World a third time
How are you World?
$
```

Nothing too exciting, just the contents of the text file. However, the `cat` command has a few parameters that can help you out.

The `-n` parameter numbers all the lines for you:

```bash
$ cat -n test_file
1 Hello World
2 Hello World again
3 Hello World a third time
4 How are you World?
5 $
```

That feature will come in handy when you're examining scripts. If you just want to number the lines that have text in them, the `-b` parameter is for you:

```bash
$ cat -b test_file
1 Hello World
2 Hello World again
3 Hello World a third time
4 How are you World?
$
```

For large files, the `cat` command can be somewhat annoying. The text in the file just quickly scrolls off the display without stopping. Fortunately, we have a simple way to solve this problem.

### Using the more command

The main drawback of the `cat` command is that you can't control what's happening after you start it. To solve that problem, developers created the `more` command. The `more` command displays a text file but stops after it displays each page of data. We typed the command `more /etc/profile` to produce the sample `more` screen shown in **Figure 3-4**.

![](img/a5025f22e05b92f409563a958cac7312_130_0.png)

**FIGURE 3-4** Using the more command to display a text file

Notice at the bottom of the screen in **Figure 3-4** that the `more` command displays a tag showing that you're still in the `more` application and how far along (29%) in the text file you are. This is the prompt for the `more` command.

> **TIP**
>
> If you’re following along with the examples, and your Linux system does not have the `/etc/profile` file or it’s rather short, try using `more` on the `/etc/passwd` file instead. Type `more /etc/passwd` and press Enter at your shell prompt.

The `more` command is a pager utility. Earlier in this chapter we discussed that a pager utility displays selected Bash manual pages when you use the `man` command. Similarly to navigating through the `man` pages, you can use `more` to navigate through a text file by pressing the spacebar, or you can go forward line by line using the Enter key. When you are finished navigating through the file using `more`, type `q` to quit.

The `more` command allows some rudimentary movement through the text file. For more advanced features, try the `less` command.

### Using the less command

From its name, it sounds like it shouldn’t be as advanced as the `more` command. However, the `less` command name is actually a play on words and is an advanced version of the `more` command (the `less` command name comes from the phrase “less is more”). It provides several very handy features for scrolling both forward and backward through a text file, as well as some pretty advanced searching capabilities.

The `less` command can also display a file’s contents before it finishes reading the entire file. The `cat` and `more` commands cannot do this.

The `less` command operates much the same as the `more` command, displaying one screen of text from a file at a time. It supports the same command set as the `more` command, plus many more options.
