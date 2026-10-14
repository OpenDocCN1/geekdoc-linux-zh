
The output is actually a description of how to transform the old file into the new one. Here, diff is telling you three things:

- The fifth line of the file has undergone a change. The 5c5 message says to replace line 5 of the old file with line 5 of the new file. Both the old and new text are displayed, separated by a line of three dashes. (The less-than (<) notation means "remove this line," and the greater-than (>) sign means "add this line.")
- Line 7 of the old file does not appear in the new file. The 7d6 message says to delete line 7 from the old file, and the files will then be in sync, starting at line 6 of the new file. The text to be deleted is displayed on the next line.
- A line was added to the new file. The 21a22 message says to add a new line after line 21 of the old file. The text to be added is displayed on the final line of the output.

Two useful flags you can specify when comparing files are -b (ignore blanks) and -i (ignore case). You can use them separately or in combination. The ignore blanks feature is especially useful when you're comparing the source code for two programs, since indentation changes are rarely significant. For example, here's how you might compare two program files, urzcool.c and urzcool.backup:

```
diff -b -i urzcool.c urzcool.backup
```

Don't worry if you have some difficulty understanding the output of the diff command. It's cryptic because it was designed to be used by computers, not humans. (Some source-code control systems used by programmers use diff to keep a record of the changes made to a program over time.)

Do pay attention, though, to the less-than and greater-than indicators to see at a glance what was added or deleted; and be happy if you manage to get a general feeling for the ways the files differ.

## Remind Me at Six

Linux provides a really handy way to schedule future events so they run automatically. You can use the at command to schedule reminders or administrative tasks or to run a command later when the computer won't be busy. After you specify the time (and optional date) for your event, at prompts you for the command to run. After entering your command, press CTRL-D to finish. Here are some examples:

```
at 8:15am Jul 14
echo "Remember to call Ruth about the Amalgamated Contract!"
^D
at midnight Friday
cp project/source backup
^D
```

To find out what events you have already scheduled with at, enter the following:

```
at -l

1 1999-07-14 08:15 a
2 1999-07-16 00:00 a
```

To cancel an event scheduled with at, use the atrm command and a job number (which you can find in the first column of the at -l results). For example, to cancel job number 2 you would enter:

```
atrm 2
```

## Link Files Together

You can link files together in two ways: with hard links or symbolic links.

### Creating a Hard Link

The ln command lets a file on your disk be accessed with more than one file name by hard-linking a new file name to it. When you hard-link a file, you create a new file name and connect it with the original file. Hard-linking can let two users share the same file or provide a more convenient way of referencing files buried deep in a series of directories. Here's an example. Suppose hermie and sigmund are working on the Top Secret Snowgun Project, and the formula for the Snowgun is stored in /home/hermie/projects/snowgun/formula.txt. Sigmund doesn’t want to type that long, ugly file name every time he needs to update the file, so he creates a hard link to the file, like this:

```
ln /home/hermie/projects/snowgun/formula.txt sgformula
```

The preceding command links the file name sgformula to the file formula.txt contained at the end of that directory string. There’s still only one copy of the snowgun formula (formula.txt) on the disk, but now sigmund can access it quickly with the name sgformula (assuming hermie gives him write permission to the file). Interestingly, if hermie deletes his projects/snowgun/formula.txt file, Linux will not remove the file from the file system because sigmund still has a link to it.

Think of the ln command as a way of creating a kind of nickname for a file. By the way, there is no parallel to this file-linking concept in the DOS world—you’d have to create a second copy of the file and keep the various copies in synch manually to get a similar result.

### Creating a Symbolic Link

The type of link we just created is called a hard link. There’s another type called a symbolic link. Symbolic links (also called symlinks) work like hard links, but you can do a bit more with them. If you want to create a link to a directory (as opposed to a file), you must create a symlink. Symlinks are also required when linking to a file on a different disk partition or on a network.

To create a symbolic link, add the -s parameter to the ln command, like this:

```
ln -s /dev/fd0 A:
ln -s /etc/httpd/conf web
```

The first example allows you to access the floppy drive as drive A, just like in DOS, and the second creates a directory entry called web that can be used instead of /etc/httpd/conf.

## Wrapping Up

Learning Unix would be hard if you tried to master everything it has to offer all at once. But then so would DOS, and especially Windows. In fact, Windows’ configuration files are more complex than Unix’s. When
