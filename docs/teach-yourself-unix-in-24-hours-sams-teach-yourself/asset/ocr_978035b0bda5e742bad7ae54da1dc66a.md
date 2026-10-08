# An Introduction to the vi Editor

| -rw-rw---- | 1 taylor | 12556 Nov 16 09:49 keylime.pie |
| -rw-rw---- | 1 taylor | 8729 Dec 2 21:19 owl.c |
| -rw-rw---- | 1 taylor | 199 Dec 3 16:11 sample |
| -rw-rw---- | 1 taylor | 207 Dec 3 16:11 sample2 |
| drwx- | 2 taylor | 512 Oct 13 10:45 src/ |
| drwrwx- | 2 taylor | 512 Nov 8 22:20 temp/ |
| -rw-rw---- | 1 taylor | 582 Nov 27 18:29 tetme |

"demo" 17 lines, 846 characters

You can see that vi reads the file specified on the command line. In this example, my file is 17 lines long, but my screen can hold 25 lines. To show that some lines lack any text, vi uses the tilde on a line by itself. Finally, note that, at the bottom, the program shows the name of the file, the number of lines found in the file, and the total number of characters.

Type :q again to quit and return to the command line for now. When you type the colon, the cursor will flash down to the bottom line and wait for the q as it did before.

> SUMMARY You have learned the most basic command in vi—the :q command—and learned experience. It's all downhill from here.

# Task 11.2: Simple Cursor Motion in vi

DESCRIPTION Getting to a file isn't good if you can't move around in it. Now you will learn how to use the cursor keys in vi. To move left one character, type h. To move up, type k. To move down, type j, and to move right a single character, type l (lowercase L). You can move left one character by pressing the Backspace key, and you can move to the beginning of the next line with the Return key.

+   1. Launch vi again, specifying the demo file:
   % vi demo