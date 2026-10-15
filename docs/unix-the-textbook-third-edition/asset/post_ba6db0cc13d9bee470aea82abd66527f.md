
where:

^ stands for pressing <Ctrl+V> and then <Esc>; and
^M stands for pressing <Ctrl+V> and then the <Enter> key

The relative number of spaces in this map command definition controls the indentation of the skeleton construct. Also, the ^M entries put each of the skeleton construct components on a new line.

## 3.2.9.4 Vim/Gvim Macro Example

Here is a repeat of Practice Session 3.4, slightly enlarged, that uses a vim-specific macro command sequence to accomplish the same thing that Practice Session 3.4 did, but in another way.

## 3.2.9.5 Practice Session 3.6

Step 1: From the shell prompt, type vim unixos2 and then press <Enter> on the keyboard.

Step 2: In vim, type A and then type the following 10 lines of text, each on its own line:

```
computer scientists
students
hackers
systems analysts
newbies
UNIX gurus
computer programmers
systems administrators
network administrators
LINUX users
```

Step 3: Press <Esc>, then place the cursor anywhere on the first line of text.

Step 4: Type q a. This puts you in record mode and associates the macro you are about to record with the a key.

Step 5: Type I. The cursor is now at the start of the first line in Insert mode.

Step 6: Type UNIX is the operating system of choice for with a single space after the r in the word for. Press <Esc>.

Step 7: Place the cursor anywhere on the second line of text.

Step 8: Type q. This ends record mode.

Step 9: Type a@9. This “plays back” the macro defined with the a key nine times, once on each of the lines below the first line, inserting the text string UNIX is the operating system of choice for.

Step 10: Save the file, print it out, and memorize its contents.

## 3.3 THE EMACS EDITOR

The emacs editor is the most complex and customizable of the UNIX text editors, and it gives you the most freedom, flexibility, and control over the way you edit text files. It can format text for very specific technical applications, such as program source code development, more effectively than a word processor. Its use in that application makes the process of program development more efficient. In addition, from within the emacs program, in multiple windows, you can accomplish a wide variety of personal productivity and operating system tasks, such as sending e-mail and executing shell commands and scripts. But along with more control, specificity, and capabilities comes some additional learning in terms of a more complex keystroke command structure. This complexity can be offset in part for some users, and totally for others, by using the graphical forms of input and command execution that we will emphasize in the sections that follow.

To stress how the keyboard keys are used in GNU emacs, we repeat the following note shown at the beginning of this chapter here:

- 1. Pressing the Escape key is signified as <Esc>
- 2. Pressing the Enter key is signified as <Enter>
- 3. Pressing the <Ctrl> key in combination with another single key is signified as <Ctrl+X>, where you hold down the <Ctrl> key and press the X key (or any valid key for that combination) at the same time.
- 4. Pressing the <Alt> key in combination with another single key is signified as <Alt+X>, where you hold down the <Alt> key and press the X key (or any valid key for that combination) at the same time.
- 5. A variant of 3. and 4. is shown as <Ctrl+X> a [b], where you first press and release <Ctrl> and X simultaneously, and then press the a key, and optionally press the b key (or any valid combination of single keys or strings of characters.
- 6. In GNU emacs for PC-BSD and Solaris, the Meta key that is referred to in much of the literature on GNU emacs, is the <Alt> key.

It is important to realize before you begin that there are some common terms used in vi, vim, and gvim (the editors from the previous section) and emacs that describe the facilities of each editor, but the terms do not have the same meaning between the two major families of editor.

As you saw in Section 3.1.2, with vi, vim, and gvim, you can't immediately begin to enter text into the file you are editing. You have to be in Insert mode to do that, that's what typing A as the second step is doing. Vi, vim, and gvim have modes. In GNU emacs, you can start typing text into the file immediately. Emacs is a modeless editor.

Vi, vim, and gvim operate in three distinct modes: Command mode, Insert mode, and Last Line mode. Emacs is a modeless editor in the sense that, when you launch emacs, you do not have to switch modes to immediately type characters on the keyboard and enter text into a buffer, or change modes to save the buffer to a file.

For example, emacs does have major modes of operation, such as Lisp mode, Python mode, and C mode, but they are for the special formatting of text and for specialized operations when editing files for use in those language applications. This is different from allowing you to switch between significant forms of action in the editor, as the vi, vim, and gvim Command, Insert, and Last Line modes do, as seen in the previous section. The keystroke command syntax itself in emacs is different and more complex than in vi, involving use of the <Ctrl> and <Alt> prefix characters, as previously noted. The emacs concepts of point and the cursor location are also more refined and specific than in vi. In emacs, the point is the location in the buffer where you are currently doing your editing; the point is assumed to be at the left edge of the cursor, or always between characters or white space (what you enter into a text file when you press the space bar). This difference becomes an important issue when you want to use the cut/copy/paste operations. In vi, yanking removes text from the main buffer, much like cutting/copying, whereas in emacs yanking is more like pasting into the main buffer. The concept of a buffer is very important in emacs, and is very much the same in emacs as it is in vi.

Currently, there is one major "brand" of emacs for UNIX: GNU emacs. We use the graphical form of GNU emacs version 24.3.1 in both PC-BSD and Solaris, running in its own frame, in the following illustrations, exercises, practice sessions, and problems.

If you cannot run a graphical emacs because you are working in a text-only console or terminal, you can still gain access to the Menu Bar at the top of the emacs screen by pressing <Esc> on the keyboard and then pressing the single back quote (`) key. You can then descend through the menu bar choices by pressing the letter key of the menu choice you want to make. For example, pressing the f key gives you access to the File pull-down menu choices, and then pressing the s key allows you to save the current buffer. Unfortunately, you cannot access the speed button menu choices from within a text-only display of emacs. A summary of emacs commands is given in Table 3.10.

## 3.3.1 Launching Emacs, Emacs Screen Display, General Emacs Concepts and Features

The general syntax for launching the emacs program from the command line in a console window is as follows (anything enclosed in square brackets [ ] is optional):
