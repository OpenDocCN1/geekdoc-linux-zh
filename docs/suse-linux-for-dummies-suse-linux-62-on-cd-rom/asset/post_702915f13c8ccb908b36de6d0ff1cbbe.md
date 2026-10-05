
## Chapter 8: Working with Files and Commands

## Have It Your Way

Most commands for your Linux system are flexible and can be modified to perform special tasks. You can use two devices to alter a command: command options and standard input and output redirection. You find out about command first.

You can use command options to fine-tune the actions of a Linux command. Earlier in this chapter, we introduce the ls command so that you could see the results of actions taken on the file system, but we don't explain in section how it worked or what changes it did. To see how options work, in the next example you try out the ls command several times, with different options.

Use the mkdir command to make a new directory called gregger; then, use the cd command to change your working directory to that new directory:

```
maddog@localhost:~/emptirectory> mkdir gregger
maddog@localhost:~/emptirectory> cd gregger
```

At the Linux prompt, type ls as follows:

```
maddog@localhost:~/emptirectory/gregger> ls
maddog@localhost:~/emptirectory/ 
```

That didn't do much, did it? It seems as if the account has no files. You may need an option. Try the -a option and see what happens:

```
maddog@localhost:~/emptirectory/gregger> ls -a
maddog@localhost:~/emptirectory/ 
```

Remember to type the commands and options exactly as shown. For example, the ls -a command has a space between the command and the option, and no space between the hyphen and the letter a.

Notice the two files (they're actually directories, but in Linux all directories are just files) that the ls command displayed. What? All you see are dots? Well, the single dot represents the directory you are in; the double dot represents the parent directory, typically the one above the directory you're in. (Linux creates these filenames and puts them into the directory for you. If you just installed your directory, all you have are files that begin with a period.)

Now we create a few additional files in the gregger directory, using the touch command:

```
maddog@localhost:~/emptirectory/gregger> touch file1
maddog@localhost:~/emptirectory/gregger> touch .dotfile
```

![](img/96a9ce6a13d8d15ed05f867f41574278_176_0.png)

Now if you do the same ls command (without the a option), you see the following:

```
maddog@localhost:~/emptydirectory/gregger> ls
file1
maddog@localhost:~/emptydirectory/gregger>
```

And if you redo the ls command with the -a option, you get this:

```
maddog@localhost:~/emptydirectory/gregger> ls -a
..dotfile file1
maddog@localhost:~/emptydirectory/gregger>
```

The ls command by default doesn't list files that begin with a period. By adding the -a option, you modified the action taken by ls to print filename, whether or not it begins with a dot.

The ls command has many options and you can use more than one at a time. Want to see how? Modify the -a option by adding -l to it. The command line becomes

```
maddog@localhost:~/emptydirectory/gregger>ls -al
total 5
drwxr-xr-x 3 (username)(group)(filesize) Jan 10 14:33 ../
drwxr-xr-x 6 root (filesize) Jan 04 22:15 ../
-rw-r--r-- 1(username)(group)(filesize) Jun 18 11:30 .dotfile
-rw-r--r-- 1(username)(group)(filesize) Apr 13 17:40 file1
```

As you can see, rather than just the filenames, the l option shows a more detailed listing of files. If long lists won't fit on a single line, Linux just wraps them to the next.

Most of the time, Linux doesn't care what order you type the options therefore considers ls -a and ls -la to be the same. Multiple option choices aren't available with all commands, however, and work only with commands that have single letters to specify their options.

The ls command lists files in alphabetical order as the default, but you can tailor the output. For example, ls -alt displays the files in order by date, with the most recent first; ls -ltr reverses that order.

![](img/96a9ce6a13d8d15ed05f867f41574278_177_0.png)

## Oh Boy, the Pipes...

Linux commands generate a lot of output, and if it all went to the screen without some kind of control it would scroll past. For example, type the following:

```
ls -al /etc
```

This command lists all the files in your /etc directory. Because this directory holds a lot of files, the information scrolls down your screen faster than you can read it. You can, however, use a process called piping. Linux uses the output from one command as the input for another. It's not as confusing as it might sound. In the last example, you had too much information to fit on one screen. You can take that information and put it into a program that divides the information into screen-sized pieces and displays them. To do this, use the more command, which is an appropriate name for this tool. How do you pipe? You use the space bar on your keyboard. You were wondering what that key was for. Type the command as follows:

```
ls -al /etc | more
```

Linux doesn't care about spaces around the pipe, but you may want to use them for clarity and to get in the habit of including spaces because they are important sometimes. When you press Enter, the information appears one screen at a time with the word more appearing at the bottom of each screen except the last. To move to the next screen, press the spacebar. When you finish with the last screen, the more command takes you back to the Linux prompt. The more command can do more. When the screen fills with the word more appearing at the bottom, you can type some commands to more:

- q to get out of more without wading through all those screens
- h to see a list of all commands available in more

Note that some commands to more (such as b) don't work when you are piping into the program, as opposed to using more with a file.

Everyone makes mistakes. Everyone changes his mind from time to time. For those reasons, you need to know how to delete text from the Linux line. If you want to start, press Ctrl-U to remove everything you have typed on the command line if you have not yet pressed Enter. The Backspace key erases one character at a time. The left- and right-arrow keys move the cursor along the line without erasing; when you get to the place you want to change, use the Backspace key to erase mistakes and retype them. In most cases, the up- and down-arrow keys jump the cursor back and forth through the last few commands.

![](img/96a9ce6a13d8d15ed05f867f41574278_178_0.png)

![](img/96a9ce6a13d8d15ed05f867f41574278_178_1.png)

Linux sometimes uses a command called less, which duplicates the functionality of the more command. Originally, the less command was designed to be more robust than the more command, but the more command caught up and they are now almost the same. Some Linux systems display text with the less command instead of the more command, which most UNIX programs use.

![](img/96a9ce6a13d8d15ed05f867f41574278_179_0.png)

The less and more commands have two apparent differences. One, the less command requires a q command to get back to the Linux prompt, even when you are at the end of the last page. Two, the more command always says More at the bottom of a screen, whereas less has just a : character at the bottom of the screen to indicate that it is waiting for you to input the next command. The SuSE Linux For Dummies CD-ROM, which is a SuSE distribution, uses more than less as a default.

## Chapter 9

## Working with Editors

### In This Chapter

- Working with editors
- Formatting text

Every one who writes Linux books needs a good editor. But the kinds of editors we talk about in this chapter are text editors, not the frazzled, publishing professionals who struggle mightily with books. Text editors with text files give you the ability to add, delete, search, and move text—everything from thousands of lines of text down to a single character.

Nowadays, text files are updated with word processors, but every once in a while, you may have to go in and update a file with a text editor. In addition, text editors create small, compact files of characters, which are still the cheapest way to send e-mail and store character data on disk.

Take the time to play around with these editors, getting down the basics, because they may be the only thing available. Also, the ed text editor is small enough to fit on a recovery disk, which is used to boot when all else fail. (Other editors, such as emacs and word processors, are too big to fit on a recovery floppy.)

### Text Editor Basics

A text editor is an essential tool for Linux. It enables you to create and modify an array of text files, including the following:

- User files, such as the login file
- System configuration files, such as /etc/fstab, /etc/inittab, and /etc/lilo.conf
- C and C++ programs
- Shell programs
- Mail messages
