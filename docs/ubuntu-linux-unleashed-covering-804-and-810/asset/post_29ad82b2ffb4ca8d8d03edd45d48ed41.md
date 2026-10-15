
As with most things, Ubuntu offers you a number of ways to access the command line. You can use the Terminal entry in Applications, Accessories, but by far the simplest way is to press Ctrl + Alt + F1. Ubuntu switches to a black screen and a traditional login prompt that resembles the following:

```
Ubuntu 8.04(Hardy) hardy-dev tty1
hardy-dev login:
```

### TIP

This is actually one of six virtual consoles that Ubuntu provides for your use. After you have accessed a virtual console, you can use the Alt key and F1 through F6 to switch to a different console. If you want to get back to the graphical interface, press Alt + F7. You can also switch between consoles by holding the Alt key and pressing either the left or the right cursor key to move down or up a console, such as tty1 to tty2.

Ubuntu is waiting for you to log in as a user, so go ahead and enter your username and press the return key. Ubuntu then prompts you for your password, which you should enter. Note that Ubuntu does not show any characters while you are typing your password in. This is a good thing because it prevents any shoulder surfers from seeing what you've typed or the length of the password.

Hitting the Return key drops you to a shell prompt, signified by the dollar sign:

```
andrew@hardy-dev ~$
```

This particular prompt tells me that I am logged in as the user andrew on the system hardy-dev and I am currently in my home directory (Linux uses the tilde as shorthand for the home directory).

### TIP

Navigating through the system at the command line can get confusing at times, especially when a directory name occurs in several different places. Fortunately, Linux includes a simple command that tells you exactly where you are in the file system. It's easy to remember because the command is just an abbreviation of present working directory, so type pwd at any point to get the full path of your location. For example, typing pwd after following these instructions shows /home/yourusername, meaning that you are currently in your home directory.
Using the pwd command can save you a lot of frustration when you have changed directory half a dozen times and have lost track.

Another way to quickly access the terminal is to go to Applications, Accessories and choose the Terminal entry. Ubuntu opens up gnome-terminal, which allows you to access
the terminal while remaining in Gnome. This time, the terminal appears as black text on a white background. Accessing the terminal this way, or by using the Ctrl + Alt + F1 method makes no difference because you are interacting directly with the terminal itself.

## Navigating Through the File System

Use the cd command to navigate through the Ubuntu file system. This command is generally used with a specific directory location or pathname, like this:

```
$ cd /etc/apt/
```

Under Ubuntu, the cd command can also be used with several shortcuts. For example, to quickly move up to the parent (higher-level) directory, use the cd command like this:

```
$ cd ..
```

To return to one's home directory from anywhere in the Linux file system, use the cd command like this:

```
$ cd
```

You can also use the $HOME shell environment variable to accomplish the same thing. Type this command and press Enter to return to your home directory:

```
$ cd $HOME
```

You can accomplish the same thing by using the tilde (~) like this:

```
$ cd ~
```

Don't forget the pwd command to remind you where you are within the file system!

Another important command to use is the ls command, which lists the contents of the current directory. It's commonly used by itself, but a number of options (or switches) available for ls give you more information. For instance, the following command returns a listing of all the files and directories within the current directory, including any hidden files (denoted by a . prefix) as well as a full listing, so it will include details such as the permissions, owner and group, size and last modified time and date:

```
$ ls -al
```

You can also issue the command

```
$ ls -R
```

which scans and lists all the contents of the sub-directories of the current directory. This might be a lot of information, so you may want to redirect the output to a text file so you can browse through it at your leisure by using the following:

```
$ ls -alR > listing.txt
```
