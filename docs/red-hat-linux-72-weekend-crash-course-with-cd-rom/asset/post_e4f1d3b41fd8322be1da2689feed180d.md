
The wildcard specification `s.*s*` denotes all filenames that meet these criteria. Thus, you can perform the search with the following command:

```
grep "*typeef struct*" /usr/include/s*.h
```

The string contains a space (you want the grep command to find), so you have to enclose that string in quotation marks (`"`). This method ensures that Bash does not try to interpret each word in the string as a separate command-line argument.

Although the asterisk (*) matches any number of characters, the question mark (?) matches a single character. Suppose you have four files—`image1.pcx`, `image2.pcx`, `image3.pcx`, and `image4.pcx`—in the current directory. To copy these files to the `/mnt/floppy` directory, use the following command:

```
cp image?.pcx /mnt/floppy
```

Bash replaces the single question mark with any single character and copies the four files to `/mnt`.

The third wildcard format (`[...]`) matches a single character from a specific set. You may want to combine this format with other wildcards to narrow down the matching filenames to a smaller set. To see a list of all filenames in the `/etc/X11/Xdm` directory that start with `x` or `X`, type the following command:

```
ls /etc/X11/Xdm/[xX]*
```

![](img/5fe8f856723cde0b366f73584b9e64b8_87_0.png)

> If Bash does not find any filenames matching the [...] wildcard format when expanding it, Bash leaves the wildcard specification intact.

## Looking at the command history

To make it easy for you to repeat long commands, Bash stores up to 500 (the default) previously executed commands. This feature is called a **command history** (a list of old commands). To see the command history, type `history`. Bash displays a numbered list of the old commands, including those that you entered during previous logins. That list may resemble the following:

```
1  cd
2  ls -a
3  more /etc/X11/XF86Config
4  history
```

If the command list is too long, you may choose to see only the last few commands. To see the last 10 commands only, type this command:

```
history 10
```

To repeat a command from the list that the `history` command shows, simply type an exclamation point (`!`), followed by that command's number. To repeat command number 3, type `!3`.

You also can repeat an old command without knowing its command number. Suppose you *typed* `more /usr/lib/X11/xdm-config` a while ago, and now you want to look at that file again. To repeat the previous `more` command, type the following:

```
lmore
```

Often, you may want to repeat the last command that you typed—perhaps with a slight change. For example, perhaps you displayed the contents of the directory by using the `ls -l` command. To repeat that command, type two exclamation points as follows:

```
!!
```

Sometimes, you may want to repeat the previous command but add extra arguments to it. Suppose that `ls -l` shows too many files. Simply repeat that command, but pipe the output through the `more` command as follows:

```
!! | more
```

Bash replaces the two exclamation points with the previous command and then appends `| more` to that command.

> An easy way to recall previous commands is to press the up arrow key, which causes **Bash** to go backward in the list of commands. To move forward in the command history, press the down arrow key.

## Using aliases for commands

To see the benefit of aliases, type the following command:

```
alias gobot='"cd /usr/src/linux/arch/i386/boot"'
```

This defines `gobot` as an *alias*—another name—for the text that appears within the single quotes (`'`). That text is a command to change the *current directory* to `/usr/src/linux/arch/i386/boot`.

Now that you've defined the alias, type the following at the Bash prompt:

```
gobot
```

Type `pwd` to confirm that the *current directory* is indeed `/usr/src/linux/arch/i386/boot`.

As you can see, an *alias* is simply an alternative (and usually shorter) name for a lengthy command. Bash replaces the alias with its definition and performs the equivalent command.

If you no longer need an alias, use the `unalias` command to remove the *alias*. For example, if you no longer want to use the `gobot` alias, type:

```
unalias gobot
```

After this step, typing `gobot` causes you to get an error message like this:

```
gobot
bash: gobot: command not found
```

## Redefining Dangerous Commands

Another good use of an alias is to redefine a dangerous command, such as `rm`, to make it safer. By default, the `rm` command deletes one or more specified files. If you type `rm *` by mistake, `rm` deletes all files in your current directory. One user learned this the hard way one day when he wanted to delete all files that ended with `.xwd`. (These files contained old screen images that he no longer needed.) He intended to type `rm *.xwd`, but somehow he ended up typing `rm * .xwd`. He got the following message:

```
rm: .xwd: No such file or directory
```

Puzzled by the message, he typed `ls` to see the directory's contents again. When the listing showed nothing, he realized that he had an extra space between the `*` and `.xwd`. All the files in that directory, of course, were gone forever.

The `rm` command provides the `-i` option, which asks for confirmation before deleting a file. To make that option a default, add the following alias definition to your `.bash_profile` file in your home directory:

```
alias rm='rm -i'
```

From now on, when you use `rm` to delete a file, the command first asks for confirmation as follows:

```
rm .bash_profile
rm: remove '.bash_profile'? n
```

Press `y` to remove the file; otherwise, press `n`.

Many users take advantage of the alias feature to give more familiar names to common commands and to create shortcuts to frequently typed long commands. If you are a DOS user and you issue the `md` command to create a directory, you can simply define `md` as an alias for `mkdir` (the Linux command that creates a new directory). You do this as follows:

```
alias md='mkdir'
```

Now, you can type `md dirname` to create a new directory named `dirname`.

## Running commands in the background

![](img/5fe8f856723cde0b366f73584b9e64b8_89_0.png)

When you use MS-DOS, you have no choice but to wait for each command to complete before you enter the next one. You can type ahead a bit, but the MS-DOS system can hold only a few characters in its internal buffer. However, Linux can handle multiple tasks simultaneously. The only problem you may have is that the terminal or console is tied up until a command completes.

If you work in a terminal window and a command takes too long to complete, you can open another terminal window and continue to enter other commands. If you work in text mode, however, and a command seems to take too long, you need some other way to access your system.

Linux allows you to execute a long-running command *in the background*, which means that the shell starts the process corresponding to a command and immediately returns to accept more commands. The shell does not wait for the command to complete; the command runs as a distinct process in the background. To start a process in the background, you simply place an **ampersand** (`&`) at the end of a command line.

For example, when you want to search the entire file system for a file using the `find` command, you can run that command in the background and send the output to a file. To try out the `find` command in the background, type `cd` to change to your home directory and then type the following command:

```
find / -name "README.*" -print > all.readme &
```

You should *immediately* get a Bash prompt. You can now go on with other commands. When the `find` command finishes, the search results should appear in the file `all.readme` in your home directory.

![](img/5fe8f856723cde0b366f73584b9e64b8_90_0.png)

If a command that you did not run in the background seems to be taking a long time, press **Ctrl+Z** to stop it. Then type `bg` to put that process in the background.

## Using virtual consoles

Red Hat Linux comes with a number of *virtual consoles*. The combination of a monitor and a keyboard is called the *terminal* or *console*. Even though your Red Hat Linux system only has one physical terminal or console, it gives you the appearance of having multiple consoles. From the graphical X screen (the GNOME or KDE desktop), press **Ctrl+Alt+F1** to get to the first virtual console, press **Ctrl+Alt+F2** for the second one, and so on. Each of these virtual consoles is a text screen where you can log in and type Linux commands to perform various tasks.

Go ahead and press **Ctrl+Alt+F2** to switch to the second virtual console. Then log in and try some Linux commands. You can log out by typing `exit` at the Bash prompt. To get back to the graphical X display, press **Ctrl+Alt+F7** (or, possibly, **Alt+F7**).

## Troubleshooting

If you pass an argument made up of multiple words to a command and get an error message stating, in part, *No such file or directory*, try enclosing the argument between weak quotes (`"`) and typing again. Remember that Bash uses spaces and tab characters to distinguish between commands, options, and arguments. For example, the following command `grep "Kurt Wall" /etc/passwd` generates an error message before showing its result:

```
grep: Wall: No such file or directory
cut/passwd:kwall: x:500:500:/Kurt Wall:/home/kwall:/bin/bash
```

Enclosing `Kurt Wall` within weak quotes solves the problem.
