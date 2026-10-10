
# Chapter 6: Using Text Editors

- Overview of Linux Text Editors
- Using vim
- Using pico
- Using jed
- The Basics of emacs
- AbiWord Personal
- KDE and GNOME Text Editors
- Using nedit
- Apex for Linux
- Spell Checking
- Checking Grammar and Readability
- Introduction to Printing

This chapter introduces text editors you will find included with nearly every Linux distribution. You will also get an introduction to spell checking with Linux, and then see how to print using Linux printing software.

There are many different editors available for the Linux console and the X Window System. The first half of this chapter will discuss editors that may be used with or without an active X session. You will then read about editors with graphical interfaces that feature traditional menus and dialog boxes.

If you are new to Linux, but have experience with Mac OS, using a graphical editor may seem more familiar during your first editing sessions when using X11. However, it is important that you learn how to use console-based text editors, because there may be times when you are not running X but still have to edit text on your system. This is especially true if you have booted into a rescue mode, or if you have accessed Linux via a dialup shell account or telnet session. There are ways, however, to run graphical clients over a network (see “Using X11 on a Network” in Chapter 8, “Using X11”).

## Overview of Linux Text Editors

There is a wealth of software available for Linux. This is also true of the number of text editors you will find for Linux. Although not all of the available editors will be discussed here, you can get an idea of the number of text editors installed on your system by using the `apropos` command with the `text editor` phrase, like this:

```
$ apropos 'text editor'
```

- ded (1) - text editor
- edior (ix) - a text editor for X with drag and drop and accents capabilities.
- elvis (1) - a clone of the ex/ev text editor
- ex (1) - Vi Improved, a programmers text editor
- gedit (1) - GTK+ based text editor
- gmp (1) - gnomepad-, a GTK-based HTML/text editor
- jove (1) - an interactive display-oriented text editor
- mcedit (1) - Full featured terminal text editor for Unix-like systems.
- mg (1) - emacs-like text editor
- nc (1) - Client program for NEdit text editor
- nedit (1) - text editor
- nvi (1) - text editors
- pico (1) - simple text editor in the style of the Pine Composer
- red (l) - text editor
- rlview (l) - Vi Improved, a programmers text editor
- rlvim (l) - Vi Improved, a programmers text editor
- textedit (lx) - Xlview window- and mouse-based text editor
- vi (l) - Vi Improved, a programmers text editor
- view (l) - Vi Improved, a programmers text editor
- vim (l) - Vi Improved, a programmers text editor
- xedit (lx) - simple text editor for X
- xvi (l) - multi-file text editor

Note that not all the output is shown here (other types of text editing commands have been deleted). You will find many others installed on your system, including several for the K Desktop Environment. Each editor has its own set of particular strengths, weaknesses, and features.

While you may typically think of an editor as an interactive program with a moving cursor and the ability to visually insert, remove, or readjust words, lines, and paragraphs on the screen, Linux also comes with editors that work from the command line or through shell scripts. Editors with this ability, such as *sed*, are known as *stream* editors, and work on text from the standard input, then send the modified text on through the standard output.

If you have a document such as *myfile.txt*, but find that a person's name has been misspelled throughout, you can use *sed* to quickly edit and replace all occurrences with a single command line. For example, if the original text looks like this:

> Mr. Ho Lee Fook, one of the largest campaign raisers for Arlington County's recent Board of Supervisors election, and a long-time resident of Lyons Village, had recently been arraigned on charges of burglary in connection with a series of break-ins in various townhouse communities in Fairfax, Va. Fook, 39, was arrested Saturday as he was leaving RT's restaurant in the Courthouse section of Arlington, Va.

You can correct the error by using *sed*'s search operator, a forward slash (/) delimiter, which is followed by the text to find, another delimiter, the text to replace, and finally the globally replace operator. The command should appear like this:

```
$ sed s/Fook/O'Brien/g myfile.txt
```

> Mr. Ho Lee O'Brien, one of the largest campaign raisers for Arlington County's recent Board of Supervisors election, and a long-time resident of Lyons Village, had recently been arraigned on charges of burglary in connection with a series of break-ins in various townhouse communities in Fairfax, Va. O'Brien, 39, was arrested Saturday as he was leaving RT's restaurant in the Courthouse section of Arlington, Va.

As you can see, the previously misspelled name has been replaced throughout the text. Note that a backslash (\) is used to distinguish and allow the use of an apostrophe on the shell command line. As the original text is undisturbed, the output of the sed command line may then be redirected to a new file, like this:

```
$ sed s/Fook/O'Brien/g myfile.txt > corrected_file.txt
```

Using the sed command for quick edits to text can be much faster than starting an editor, loading the file, and then performing a global search and replace.

## Word Processor or Editor?

What is the difference between a word processor and an editor? For many users, there is little difference, and most are happy as long as they can manipulate text with ease in a friendly software environment. Other users feel that a text editor is a word processor with fewer features, while traditionalists would never use a word processor to edit text files. The truth is that word processors and text editors share many common features.

In general, a text editor is used to edit text in ASCII (American Standard Code for Information Interchange) format. The standard ASCII character set is generally limited to 127 characters, with each letter designated by a code represented by seven bits (e.g., the limit of 127 characters). Extended character sets that use eight bits, such as the ISO Latin 1 set, provide an additional 128 characters. Word processors generally have the ability to store additional data, such as font, point size, color, and alignment information for all or a portion of a document's contents. However, you can also use a text editor to insert formatting commands into text documents by using a specification such as Rich Text Format (.rtf), rncgf manuscript commands, HTML (Hypertext Markup Language), or LaTeX.

## Choosing an Editor

Choosing an editor is a matter of personal choice, need, policy, or resources. As you have already learned, real Linux users do not even need a text editor when the `cat` command is available. You can simply use:

```
$ cat >myfile.txt <<,
```

The command line uses the `cat` command to read its input and redirect its output to the file named `myfile.txt`. Text will be read until the shell finds a period (`.`) on a line by itself. After pressing Enter, the text file will be saved.

> Of course, some Linux Tk users (such as Przemek Ktosowski of the District of Columbia’s Linux Users Group) will say that the easiest editor to use is:
>
> ```
> #!/usr/bin/wish
> pack {text .t} [button .b -text save -command save]
> proc save {} {
>     set f [open "newFile.txt" w]; puts $f [.t get 1.0 end]; close $f
> }
> ```
>
> This code snippet (modified from a posting on the ma-linux@tux.org mailing list by Ktosowski) may be used as a command. Save the code in a text file with a name such as `textit`, then use `chmod +x` `textit` to make the file executable. These few lines of text create a graphical editor with a moveable window and a Save button. All input text will be saved in the file named `newfile.txt`.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_134_0.png)

There is little point in listing all the features of a great text editor, but some features to look for in a usable Linux text editor are listed in Table 6.1.

If you find that a particular editor suits your tastes, you can choose to make that editor the default system editor for Linux. The default system editor is determined by the definition of the `EDITOR` environment variable, which is recognized by a number of programs on your system, such as `cronTab`. If you do not define your own system editor, most commands will, by default, use the `vi` editor. To use another editor, such as `nano` (see the sidebar “pico or nano?” below), you can edit your `.bashrc` in your home directory, and then add this line:

```
export EDITOR=/usr/local/bin/nano
```

Make sure that you type the correct and complete pathname to the editor! To use this variable right away, re-read your `.bashrc` file like this:

```
$ . .bashrc
```

You can also use `bash`'s `source` built-in command like this:

```
$ source ./.bashrc
```

To make these changes to the entire default system, place the `EDITOR` definition in `/etc/profile`, `/etc/skel/.bashrc`, `/etc/csh.cshrc`, or `/etc/cshrc`.
