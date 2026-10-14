
## Complete Idiot's Guide to Linux:Text Editing under a Shell

```
press the j key enough times to move the cursor so that Lesson 1.1 completely fills the screen.
```

As you can see, typing those commands will put you right into a vim session with the tutorial on the screen. Follow the instructions, and you are on your way. The tutorial should take anywhere from 20 to 60 minutes, depending on how many distractions (such as phone calls) occur.

+   Previous | Table of Contents | Next

+   Products | Contact Us | About Us | Privacy | Ad Info | Home

Use of this site is subject to certain Terms & Conditions. Copyright © 1996-2000 EarthWeb Inc. All rights reserved. Reproduction whole or in part in any form or medium without express written permission of EarthWeb is prohibited.

To access the contents, click the chapter and section titles.

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Vim Basics

If you just want to get the hang of it, here’s a bare-bones tutorial.

Vim is a modal editor. All this means is that when you are using vim, the program will behave differently depending on whether you are in command mode or editing mode.

Let’s go. Create and edit a file with vim. On your command line, issue the following:

```
[alberto@digital alberto]$ vim tutorial
~
~
~
"tutorial" [New File]
```

A graphical version of vim can be started from within KDE by issuing the command gvim (graphical vim).

On issuing the command, the editor will take over your terminal. Empty lines are marked by a tilde (~) character. Vim is currently in its command mode. It is waiting for you to tell it what to do.

When in command mode, you can move around the document (assuming there’s some text to navigate, which won’t be the case in a new document) and issue commands. Table 13.1 is a list of all the cursor moving commands. (As you can see, some are mapped to special keys on your keyboard.)

### Table 13.1 Moving Around the Document

| Key | Function |
|---|---|
| l or Right Arrow | Moving forward to the next character |
| h or Left Arrow | Move back one character |
| j or Down Arrow | Move down one line |
| k or Up Arrow | Move up one line |
| w | Move one word forward |
| b | Move one word backward |

In general, you move your cursor by using the arrow keys (or its hjkl counterparts—I rarely can remember these). To scroll the document, you use the Page Up and Page Down.

The cursor will not wrap or move beyond the beginning or end of a line. When you reach the end, the computer will beep. To go to the next or previous line, use the down or up arrow keys, respectively.

When you begin a new, blank document, you don’t have much to do; there’s no text to edit or navigate. To add text, you need to get into the insert mode. This mode will allow you to enter text as you normally do in other programs; you are still able to use the arrow keys to move around. (The hjkl keys type a letter when you are in insert mode.) Type i to get into the insert mode. Table 13.2 lists a number of editing commands that you can use while in command mode.

### Table 13.2 Vi (Vim) Editing Commands

| Command | Description |
|---|---|
| i | Insert text (begin editing) |
| x | Delete the character under the cursor (command mode) |
| dw | Delete characters until the end of the word |
| d$ | Delete text until the end of the line |
| dd | Delete the current line |
| u | Undo the last command |
| U | Undo any changes to the line |
| Ctrl+R | Redo any undos |
| Esc | Return to command mode, cancel current action—repeat until vim beeps |

To return to the command mode, hold down the Esc key until vim beeps at you. Then you can type a : + command. Commands are issued by pressing the colon (:) followed by the name of the command. Table 13.3 lists the basic ones to get you out of vim.

### Table 13.3 Vi (Vim) Exiting Commands

| Command | Description |
|---|---|
| :q! | Quit without saving |
| :wq | Save and quit |
| :wfilename | Write the buffer to filename |

Vim has some editing commands—and the all-important undo. These editing commands work while vim is in command mode.

### Command Multipliers: Repeating the Action More Than Once

Commands such as delete can specify a multiplier. If you type a number before the command, the command will be repeated that number of times.

Consider the following text:

```
This is one line of text.
This is another line of text.
```

To delete the words This and is, move the cursor under the T. Make sure you are in command mode by pressing Esc until vim beeps; then type 2dw. To delete both lines of text, put the cursor anywhere on the first line and type 2dd.

Multipliers also work for moving around in the document. To move down five lines, you can type 5, followed by the down arrow.

### Accessing the Shell from Vim

You can execute shell commands by preceding them with the exclamation point (!):

```
:!shellcommand
```

When the command finishes executing, you are prompted to hit Enter to return to the editor. To get an interactive shell, enter the name of the shell as the shellcommand (bash). When finished working with the shell, type exit on the shell prompt, and you’ll return to the editor.

### Other Stuff

Vim is fairly powerful. It supports multiple documents—or buffers, as they are known—and many other features. The commands covered here are just the bare minimum you need to know to edit files using a terminal. I encourage you to go through the tutorial and to visit vim’s home page at http://www.vim.org. You’ll be happy you did.

To access the contents, click the chapter and section titles.

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## XEmacs

XEmacs is the variant of Emacs, the GNU super editor, included with Caldera OpenLinux. XEmacs provides additional enhancements when used under a graphical environment, such as X (KDE)—hence its “X” denomination. Under a terminal, it is almost exactly the same as regular Emacs. Any reference to Emacs applies in terms of usage to XEmacs.

Emacs is the most powerful of editors. It is available for UNIX, Windows, and a slew of other operating systems. It provides features too numerous to cover in 500 pages just dedicated to Emacs alone!

Emacs is an extensible editor. Using a programming language called Lisp, Emacs can be easily extended to do just about anything thinkable.

Many hardcore UNIX people use only one program: Emacs. They start it when they start their work session, and they close it when they exit their system. All their work, with very rare exceptions, is handled through Emacs, including access to the shell.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_143_0.png)

XEmacs on a console looks like this.

From Emacs you can read, write, and organize your email and calendar, manipulate and organize your files, browse the Web, read news, develop

software, transfer FTP files across the network, and much more. No matter what you do under UNIX, it is likely that you can do it through Emacs. Of course, Emacs also edits files. If you get the sense that Emacs is really an environment, you are correct. That is what separates Emacs from other editors.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_144_0.png)

Here’s XEmacs through X—notice all the buttons and menus!

Emacs does everything through modes. A mode is just a specialized interface for interacting with a specific program or for working with a specific file format such as text or programming source code. Modes are tailored to the needs of a particular task. If it sounds complicated, it really isn’t. The modes are automatically handled by Emacs depending on what you are doing and the file you are editing.

### Starting XEmacs and the XEmacs Tutorial

To enter Emacs (XEmacs), just type xemacs at the command prompt. Emacs will greet you with a welcome message and a list of options. Most keystrokes under Emacs work as follows:

```
Ctrl+letter letter
```

When you see a command listed as C-t h, it means that first you must press Ctrl+t and then h by itself. Yes, Emacs has a lot of command keys, and it requires a little time to get used to it; however, that is time well spent.

To exit Emacs, type Ctrl+c Ctrl+x; this will return you to your shell. Teaching Emacs is beyond the scope of this book, but suffice it to say that it is worth exploring if you are going to do a lot of text editing.

One impressive feature of Emacs is that you can edit files through FTP as if they were local on your disk. For users working on Web-related services, this feature rocks. If your files can be reached through FTP, they can be edited and manipulated just as if they were local files. However, that is an advanced topic for another book.

If you are a programmer, Emacs does source formatting on the fly, so your source code is always formatted in a way that you can read. When reading other people’s code, the ability to reformat the code in a way readable to you is invaluable. Emacs also provides an IDE (Integrated Development Environment): You can build your program and debug it right from Emacs.

Emacs also has an online tutorial. To access the tutorial, start Emacs, and in the welcome window type C-h t.
