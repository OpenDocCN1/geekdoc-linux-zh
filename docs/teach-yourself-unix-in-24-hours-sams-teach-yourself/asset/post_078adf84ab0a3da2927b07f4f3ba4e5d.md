
# An Introduction to the vi Editor

Type q and press the Return key, and you should be back at the shell prompt:

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_212_0.png)

- 2. If the operation worked without a problem, skip to the next section, instruction 3.
If the operation did not work, you received the unknown-terminal-type message.
You might see this on your screen:

```
% vi
% "unknown": Unknown terminal type
I don't know what type of terminal you are on. All I have "unknown"
[using open mode]
```

Alternatively, you might see this:
```
% vi
Visual needs addressable cursor or underline capability
```

Don't panic. You can fix this problem. The first step is to get back to the shell prompt. To do this, exactly what you did in instruction 1: type :q followed by the Return key. You should then see this:
```
% "unknown": Unknown terminal type
I don't know what type of terminal you are on. All I have "unknown"
[using open mode]
```

The problem here is that vi needs to know the kind of terminal you're using, but it can't figure out on its own. Therefore, you need to tell the operating system by setting the TERM environment variable. If you know what kind of terminal you have, use the value associated with the terminal; otherwise, the default of vt100

```
% setenv TERM vt100
```

If you have the $ prompt, which means you're using the Bourne shell (sh) or Korn shell (ksh), rather than the C shell (esh), try this:

```
$ TERM=vt100 : export TERM
```

Either way, you can now try vi again, and it should work.

If it does work, append the command (whichever of these two commands was successful for you) to your .login file if you use csh or to .profile if you use sh or ksh. You can do this by entering whichever of the following commands is appropriate for your system:

```bash
% echo setenv TERM vt100 >> .login
```

or

```bash
$ echo "TERM=vt100; export TERM" >> .profile
```

This way, the next time you log in, the system will remember kind of terminal you're using.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_213_0.png)

vi and other screen commands use a UNIX package called curses to control the screen. Like most UNIX applications, curses was not designed for a specific configuration; instead, it was designed to be device-independent. Therefore, to work on a specific device, you need to give it some additional information—in this case, the terminal type.
If vt100 didn't work, it is to talk to your system administrator about the problem or call your UNIX vendor to find out what the specific value should be. If you are connected through a modem or other line and you are actually using a terminal emulator or communications package, you might also try using that as a TERM setting. If that fails, call the company that makes your software and ask the company what terminal type the program expects.

- 3. Great! You have successfully launched vi, see what it looks like, and even entered the most important command: the quit command. Now create a simple file and start vi it shows you the contents of the file:

```
% ls -l demo
% vi demo
```

| total 29 | 2 taylor | 512 Nov 10:39 Archives/ |
| :--- | :--- | :--- |
| drwx------ | 2 taylor | 512 Dec 02:03 Infolist/ |
| drwx------ | 2 taylor | 1024 Dec 03:014 Mail/ |
| drwx------ | 2 taylor | 512 Oct 06:39 News/ |
| drwx------ | 4 taylor | 512 Dec 22:08 OWL/ |
| drwx-rw-- | 1 taylor | 126 Dec 3 16:34 awkscript |
| -rw-rw-- | 1 taylor | 165 Dec 3 16:42 bigfiles |
| drwx------ | 2 taylor | 512 Oct 13 10:45 bin/ |
| -rw-rw-- | 1 taylor | 0 Dec 3 22:26 demo |

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_213_1.png)

| -rw-rw---- | 1 taylor | 12556 Nov 16 09:49 keylime.pie |
| -rw-rw---- | 1 taylor | 8729 Dec 2 21:19 owl.c |
| -rw-rw---- | 1 taylor | 199 Dec 3 16:11 sample |
| -rw-rw---- | 1 taylor | 207 Dec 3 16:11 sample2 |
| drwx- | 2 taylor | 512 Oct 13 10:45 src/ |
| drwrwx- | 2 taylor | 512 Nov 8 22:20 temp/ |
| -rw-rw---- | 1 taylor | 582 Nov 27 18:29 demo |

"demo" 17 lines, 846 characters you can see that vi reads the file specified on the command line. In this example, my file is 17 lines, but my screen can hold 25 lines. To show that some lines lack text, vi uses tilde on itself. Finally, note that, at the bottom, the program shows the name of the file, the number of lines found in the file, and the total number of characters. Type :q again to quit and return to the command line for now. When you type the colon, the cursor will flash down to the bottom line and wait as it did before.

You have learned the most basic command in vi—the :q command—and experience. It's all downhill from here. Getting to a file isn't good if you can't around around it. Now you will learn how to use the cursor in vi. To move left one character, type h. To move up, type k. To move down, type j, and to move right a single character, type l (lowercase). You can move left one character by pressing the Backspace key, and you can move to the beginning of the next line.

- 1. Launch vi again, specifying the demo:
```
% vi demo
```

| total 29 | 2 taylor | 512 Nov 21 10:39 Archives/ |
| :--- | :--- | :--- |
| drwx- | 3 taylor | 512 Dec 3 02:03 Infoworld/ |
| drwx- | 2 taylor | 1024 Dec 3 01:43 Mail/ |
| drwx- | 2 taylor | 512 Oct 6 09:36 News/ |
| drwx- | 4 taylor | 512 Dec 2 22:08 OWL/ |
| -rw-rw- | 1 taylor | 126 Dec 3 16:34 awkscript |
| -rw-rw- | 1 taylor | 165 Dec 3 16:42 bigfiles |
| -rw-rw- | 2 taylor | 512 Oct 13 10:45 dev/ |
| -rw-rw- | 1 taylor | 0 Dec 3 22:26 demo |
| -rw-rw- | 1 taylor | 12556 Nov 16 09:49 keyline.py |
| -rw-rw- | 1 taylor | 8729 Dec 2 21:19 owl.c |
| -rw-rw- | 1 taylor | 198 Dec 3 16:11 sample |
| -rw-rw- | 1 taylor | 207 Dec 3 16:11 sample2 |
| drwx- | 2 taylor | 512 Oct 13 10:45 src/ |
| drwxrw- | 2 taylor | 512 Nov 8 22:20 temp/ |
| -rw-rw-- | 1 taylor | 582 Nov 27 18:29 demo |

"demo" 17 lines, 846 characters you should consider the cursor on top of the t in total on the first line or perhaps flashing underneath the t character. Perhaps you have a flashing-block cursor or one that shows up in a different color. In any case, that's your starting point in the file.

- 2. Type h once to try move left. The cursor stays in the same spot, and vi is to remind you that you can't move further on the line. Try the k key to try move up; the same thing will happen.

Now typing j to move down a character:

| total 29 | 2 taylor | 512 Nov 21 10:39 Archives/ |
| :--- | :--- | :--- |
| drwx- | 3 taylor | 512 Dec 3 02:03 Infoworld/ |
| drwx- | 2 taylor | 1024 Dec 3 01:43 Mail/ |

Now the cursor is on the directory indicator of the second line of the file.

- 3. Using the four cursor-control keys—the h, j, k, and l keys—move around in the file for a little bit, until you are comfortable with what's happening on the screen.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_215_0.png)

Now try using the Backspace and Return keys to see how they help you move around.

- 4. Move to the middle of a line:

| total 29 | 2 taylor | 512 Nov 21 10:39 Archives/ |
| :--- | :--- | :--- |
| drwx----- | 2 taylor | 512 Dec 3 02:03 Infolorld/ |
| drwx----- | 2 taylor | 1024 Dec 3 01:43 Mail/ |

Here, I am at the mid digit in the file size of the second file in the listing. Here are a couple of cursor motion keys: The 0 (zero) key moves the cursor to the beginning of the line, and $ moves it to the end of the line. First, I type:

| total 29 | 2 taylor | 512 Nov 21 10:39 Archives/ |
| :--- | :--- | :--- |
| drwx----- | 3 taylor | 512 Dec 3 02:03 Infolorld/ |
| drwx----- | 2 taylor | 1024 Dec 3 01:43 Mail/ |

Now I type$ to move to the end of the line:

| total 29 | 2 taylor | 512 Nov 21 10:39 Archives/ |
| :--- | :--- | :--- |
| drwx----- | 3 taylor | 512 Dec 3 02:03 Infolorld/ |
| drwx----- | 2 taylor | 1024 Dec 3 01:43 Mail/ |

- 5. If you have arrow keys on your keyboard, try to see if they work the same way that the h, j, k, and l keys work. If the arrow keys don't move you, they might have shifted you into insert mode. If you type characters and they're added to the file, you need to press the Escape key (or Esc, depending on your keyboard) to return to command mode. Let's wrap this up by leaving this session. Because vi now knows that you have modified the file, it will try to ensure that you don't quit without saving the changes:

```
~~
:No write since last change (:quit! overrides)
```
