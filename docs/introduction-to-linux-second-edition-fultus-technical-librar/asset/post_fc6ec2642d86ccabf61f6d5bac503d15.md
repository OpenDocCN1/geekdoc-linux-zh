
## Introduction to Linux

- Use `locate` to find documentation about the kernel.
- Find out which file contains the following entry:
  - `root:x:0:0:root:/root:/bin/bash`
  - `system: root`
- See what happens upon issuing this command:
  ```
  > time; date >> time; cat < time
  ```
- What command would you use to check which script in `/etc/init.d` starts a given process?

# Chapter 6 Text editors

In this chapter, we will discuss the importance of mastering an editor. We will focus mainly on the **Improved vi** editor.

After finishing this chapter, you will be able to:

- Open and close files in text mode
- Edit files
- Search text
- Undo errors
- Merge files
- Recover lost files
- Find a program or suite for office use

## 6.1 Text editors

### 6.1.1 Why should I use an editor?

It is very important to be able to use at least one text mode editor. Knowing how to use an editor on your system is the first step to independence.

We will need to master an editor by the next chapter as we need it to edit files that influence our environment. As an advanced user, you may want to start writing scripts, or books, develop websites or new programs. Mastering an editor will immensely improve your productivity as well as your capabilities.

### 6.1.2 Which editor should I use?

Our focus is on text editors, which can also be used on systems without a graphical environment and in terminal windows. The additional advantage of mastering a text editor is in using it on remote machines. Since you don't need to transfer the entire graphical environment over the network, working with text editors tremendously improves network speed.

There are, as usual, multiple ways to handle the problem. Let’s see what editors are commonly available:

#### 6.1.2.1 Ed

The **ed** editor is line-oriented and used to create, display, modify and otherwise manipulate text files, both interactively and by use in shell scripts.

**ed** is the original text editor on UNIX machines, and thus widely available. For most purposes, however, it is superseded by full-screen editors such as **emacs** and **vi**, see below.

#### 6.1.2.2 GNU Emacs

Emacs is the extensible, customizable, self-documenting, real-time display editor, known on many UNIX and other systems. The text being edited is visible on the screen and is updated automatically as you type your commands. It is a real-time editor because the display is updated very frequently, usually after each character or pair of characters you type. This minimizes the amount of information you must keep in your head as you edit. Emacs is called advanced because it provides facilities that go beyond simple insertion and deletion: controlling subprocesses; automatic indentation of lines; viewing two or more files at once; editing formatted text; and dealing in terms of characters, words, lines, sentences, paragraphs, and pages, as well as expressions and comments in several different programming languages.

*Self-documenting* means that at any time you can type a special character, Ctrl+H, to find out what your options are. You can also use it to find out what any command does, or to find all the commands that pertain to a topic. *Customizable* means that you can change the definitions of Emacs commands in little ways. For example, if you use a programming language in which comments start with `/**` and end with `*/`, you can tell the Emacs comment manipulation commands to use those strings. Another sort of customization is rearrangement of the command set. For example, if you prefer the four basic cursor motion commands (up, down, left and right) on keys in a diamond pattern on the keyboard, you can rebind the keys that way.

*Extensible* means that you can go beyond simple customization and write entirely new commands, programs in the Lisp language that are run by Emacs’ own Lisp interpreter. Emacs is an *online* extensible system, which means that it is divided into many functions that call each other, any of which can be redefined in the middle of an editing session. Almost any part of Emacs can be replaced without making a separate copy of all of Emacs. Most of the editing commands of Emacs are written in Lisp already; the few exceptions could have been written in Lisp but were written in C for efficiency. Although only a programmer can write an extension, anybody can use it afterward.

When run under the X Window System (started as **emacs**) Emacs provides its own menus and convenient bindings to mouse buttons. But Emacs can provide many of the benefits of a window system on a text-only terminal. For instance, you can look at or edit several files at once, move text between files, and edit files while running shell commands.

#### 6.1.2.3 Vi(m)

Vim stands for "Vi IMproved". It used to be "Vi IMitation", but there are so many improvements that a name change was appropriate. Vim is a text editor which includes almost all the commands from the UNIX program **vi** and a lot of new ones.

Commands in the **vi** editor are entered using only the keyboard, which has the advantage that you can keep your fingers on the keyboard and your eyes on the screen, rather than moving your arm repeatedly to the mouse. For those who want it, mouse support and a GUI version with scrollbars and menus can be activated.

We will refer to **vi** or **vim** throughout this book for editing files, while you are of course free to use the editor of your choice. However, we recommend to at least get the **vi** basics in the fingers, because it is the standard text editor on almost all UNIX systems, while **emacs** can be an optional package. There may be small differences between different computers and terminals, but the main point is that if you can work with **vi**, you can survive on any UNIX system.

Apart from the **vim** command, the **vim** packages may also provide **gvim**, the Gnome version of **vim**. Beginning users might find this easier to use, because the menus offer help when you forgot or don't know how to perform a particular editing task using the standard **vim** commands.

## 6.2 Using the Vim editor

### 6.2.1 Two modes

The **vi** editor is a very powerful tool and has a very extensive built-in manual, which you can activate using the **help** command when the program is started (instead of using **man** or **info**, which don't contain nearly as much information). We will only discuss the very basics here to get you started.

What makes **vi** confusing to the beginner is that it can operate in two modes: command mode and insert mode. The editor always starts in command mode.

Commands move you through the text, search, replace, mark blocks and perform other editing tasks, and some of them switch the editor to insert mode.

This means that each key has not one, but likely two meanings: it can either represent a command for the editor when in command mode, or a character that you want in a text when in insert mode.

Pronunciation

It's pronounced "vee-eye".

### 6.2.2 Basic commands

#### 6.2.2.1 Moving through the text

Moving through the text is usually possible with the arrow keys. If not, try:

- `h` to move the cursor to the left
- `l` to move it to the right
- `k` to move up
- `j` to move down

SHIFT-G will put the prompt at the end of the document.

#### 6.2.2.2 Basic operations

These are some popular vi commands:

- `n dd` will delete n lines starting from the current cursor position.
- `n dw` will delete n words at the right side of the cursor.
- `x` will delete the character on which the cursor is positioned
- `:n` moves to line n of the file.
- `:w` will save (write) the file
- `:q` will exit the editor.
- `:q!` forces the exit when you want to quit a file containing unsaved changes.
- `:wq` will save and exit
- `:w newfile` will save the text to newfile.
- `:wq!` overrides read-only permission (if you have the permission to override permissions, for instance when you are using the root account).
