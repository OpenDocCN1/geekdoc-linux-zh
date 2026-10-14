
## What's New In The Second Internet Edition

This version of *The Linux Command Line* has undergone some additional polish and modernization. In particular, bash version 4.x is assumed to be the standard version and the text has been updated to reflect this. The chapter numbers in the Second Internet Edition now align with those in the No Starch Press edition. I also fixed a few bugs ;-).

Special thanks go out to the following individuals who provided valuable feedback on the first edition: Adrian Arpidez, Hu Bo, Heriberto Cantú, Joshua Escamilla, Bruce Fowler, Ma Jun, Seth King, Mike O'Donnell, Parviz Rasoulipour, Gabriel Stutzman, and Christian Wuethrich.

## Further Reading

- Here are some Wikipedia articles on the famous people mentioned in this chapter:
- http://en.wikipedia.org/wiki/Linus_Torvalds
- http://en.wikipedia.org/wiki/Richard_Stallman
- The Free Software Foundation and the GNU Project:
- http://en.wikipedia.org/wiki/Free_Software_Foundation
- http://www.fsf.org
- http://www.gnu.org
- Richard Stallman has written extensively on the “GNU/Linux” naming issue:
- http://www.gnu.org/gnu/why-gnu-linux.html
- http://www.gnu.org/gnu/gnu-linux-faq.html#tools

## Colophon

This book was originally written using OpenOffice.org Writer in Liberation Serif and Sans fonts on a Dell Inspiron 530N, factory configured with Ubuntu 8.04. The PDF version of the text was generated directly by OpenOffice.org Writer. The Second Internet Edition was produced on the same computer using LibreOffice Writer on Ubuntu 12.04.

## Part 1 – Learning The Shell

leges.

Assuming that things are good so far, let's try some typing. Enter some gibberish at the prompt like so:

```
[me@linuxbox ~]$ kaekfjaeifj
```

Since this command makes no sense, the shell will tell us so and give us another chance:

```
bash: kaekfjaeifj: command not found
[me@linuxbox ~]$
```

## Command History

If we press the up-arrow key, we will see that the previous command “kaekfjaeifj” reappears after the prompt. This is called command history. Most Linux distributions remember the last 500 commands by default. Press the down-arrow key and the previous command disappears.

## Cursor Movement

Recall the previous command with the up-arrow key again. Now try the left and right-arrow keys. See how we can position the cursor anywhere on the command line? This makes editing commands easy.

## A Few Words About Mice And Focus

While the shell is all about the keyboard, you can also use a mouse with your terminal emulator. There is a mechanism built into the X Window System (the underlying engine that makes the GUI go) that supports a quick copy and paste technique. If you highlight some text by holding down the left mouse button and dragging the mouse over it (or double clicking on a word), it is copied into a buffer maintained by X. Pressing the middle mouse button will cause the text to be pasted at the cursor location. Try it.
Note: Don't be tempted to use Ctrl-c and Ctrl-v to perform copy and paste inside a terminal window. They don't work. These control codes have different meanings to the shell and were assigned many years before Microsoft Windows.

Your graphical desktop environment (most likely KDE or GNOME), in an effort to behave like Windows, probably has its focus policy set to “click to focus.” This means for a window to get focus (become active) you need to click on it. This is contrary to the traditional X behavior of “focus follows mouse” which means that a window gets focus just by passing the mouse over it. The window will not come to the foreground until you click on it but it will be able to receive input. Setting the focus policy to “focus follows mouse” will make the copy and paste technique even more useful. Give it a try if you can (some desktop environments such as Ubuntu’s Unity no longer support it). I think if you give it a chance you will prefer it. You will find this setting in the configuration program for your window manager.

## Try Some Simple Commands

Now that we have learned to type, let's try a few simple commands. The first one is date. This command displays the current time and date.

```
[me@linuxbox ~]$ date
Thu Oct 25 13:51:54 EDT 2007
```

A related command is cal which, by default, displays a calendar of the current month.

```
[me@linuxbox ~]$ cal
    October 2007
Su Mo Tu We Th Fr Sa
      1  2  3  4  5  6
 7  8  9 10 11 12 13
14 15 16 17 18 19 20
21 22 23 24 25 26 27
28 29 30 31
```

To see the current amount of free space on your disk drives, enter df:

```
[me@linuxbox ~]$ df
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/sda2      15115452  5012392  9949716 34% /
/dev/sda5      59631908 26545424 30008432 47% /home
/dev/sda1        147764    17370   122765 13% /boot
```
