
## Table 6.1 Essential Text Editor Features

| Feature | Description |
| :--- | :--- |
| Ability to create backups | Some text editors feature the ability to automatically create backup documents as they write, save, or close a file. |
| Ability to handle large files | Using a text editor with Linux sometimes means having to open extremely large documents with thousands of lines of text, and the ability to open large files and navigate smoothly through the text is a necessity. |
| Automatic indenting | If you are a programmer, you will appreciate the ability to have text automatically indented. This type of formatting is also known as pretty printing, and helps increase the readability of code. |
| Built-in help | Learning how to use a new text editor in an unfamiliar environment can be an obstacle to productivity. Many text editors feature built-in help, but with others, you are on your own! |
| Copy and paste | The ability to copy and paste text helps composition for writers, students, and programmers. An editor should allow for words, lines, paragraphs, or blocks of text to be easily moved within a document. |
| Ease of use | Some editors are easier to use than others. Some offer few clues about getting started or what keystrokes to use, while others offer visual or pneumatic cues. |
| File operations | All text editors should offer the ability to save, save as, or discard changes. |
| File recovery | How well does your text editor handle a catastrophic event? Although not recommended, see what happens when you are editing an important text file and someone yanks the power cord from your computer. |
| Resource requirements | Is the editor a disk and memory hog? Does it suffer “feature-bloat”? Ideal editors combine a modicum of features with a Spartan footprint. |
| Search and replace | The ability to quickly find a word or phrase in a document is essential. Manual or automatic replacement is a bonus. |
| Speed | Obviously this will not be a problem with any Linux editor you use, but you would be surprised at how slobh-like some commercial word-processors are. |
| Spell-check | Although most often found in word processing programs, the ability to spell-check can save time, especially when composing electronic mail. |
| Stability and robustness | The good news is that if you use a Linux text editor, you will rarely, if ever, have to suffer the indignity of having the program crash. A good editor will also provide at least some way to easily back out of at least one bad edit, even if only for a line deletion. |
| Use of color | Some text editors, especially programming editors, feature automatic color highlighting of selected portions of text. |
| Word-wrap | Although differences between text files on different computer platforms and operating systems exist, the ability to wrap text at preset columns or line length is essential. In some instances however, word-wrapping should be turned off, especially if editing configuration files. A good text editor will allow you to toggle this feature either through a command-line option or interactively. |

## Using vim

The classic visual editor *vi* was written by Bill Joy, co-founder of Sun Microsystems, when he was a graduate student in California and working on BSD (*Berkeley Software Distribution*) UNIX. Linux users readily adopted a variant of this editor by Bram Moolenaar as the standard minimal editor. You will find *vim* installed on every system as a required part of the base file system. The reason for this is that *vim* is generally used during file system recovery operations, and may be the only editor available when performing maintenance on system configuration files. The *vim* editor also works on many different computer operating systems, such as Apple’s now defunct A/UX, IBM’s AIX, BSD variants, NEXTSTEP, OSF, QNX Software Systems’ QNX, Sun Microsystems’ Solaris, SunOS, and others. There is even a version for Mac OS!

Although *vim* lacks many of the modern features included with today’s text editors, it has enhancements over the original *vi*. These include built-in help, color, horizontal scrolling, multiple windows, undo, automatic indenting, and a GUI version for X named *gvim*. Although *vim* may not be as powerful in features as other text editors (see “The Basics of *emacs*”), you would be hard pressed to learn all of its features in one day, a weekend, or a month.

Most Linux distributions install *vim* under the `/bin` directory, with symbolic links named *vi* under the `/bin` and `/usr/bin` directory:

```bash
$ ls -l /bin/vi*
lrwxrwxrwx  1 root  root       3 Jan 29 22:53 /bin/vi -> vim
-rwxr-xr-x  1 root  root   700320 Oct  4 20:51 /bin/vim

$ ls -l /usr/bin/vi*
lrwxrwxrwx  1 root  root       3 Jan 29 22:53 /usr/bin/vi -> vim
lrwxrwxrwx  1 root  root      13 Jan 29 22:53 /usr/bin/view -> vim
lrwxrwxrwx  1 root  root      13 Jan 29 22:53 /usr/bin/vim -> ../../bin/vim
```

Note that you may also find a link named *view*. When you run *vim* by using the *view* or *rvim* commands, files are opened to read-only. The *rvim* command is a restricted editor that will not allow you access to the shell (as is allowed by *vim* or *gvim*).

The *vi* editor and its clones, such as *vim*, seem to have polarized adherents and detractors in the Linux text editing world. To some users, the unabashed brevity and potentially confusing commands are viewed as a hindrance and unnecessary. On the other hand, these same features endear the editor to members of the *vi* camp. In all fairness, using the editor in its simplest form can be relatively easy.

For example, to create a new text file or open an existing file for editing, use **vim** on the command line like this:

```bash
$ vi myfile.txt
```

After you press Enter, the file (if it exists) will be opened and displayed on the screen. The cursor may be moved about the text, but you cannot just start typing! By using the following simple set of commands, you should be able to edit, then save your text:

- i    Start insert mode. You can enter text at the current cursor position.
- Esc    End insert mode. You can now scroll through the text.
- x    Delete a character (when out of insert mode).
- l    Move cursor right one character.
- h    Move cursor left one character.
- j    Move cursor down one line.
- k    Move cursor up one line.
- :q!    Quit, but do not save changes.
- :qw    Quit and save changes.

The editor also recognizes the cursor keys. However, these may not always be available, especially if there are problems with a system's keyboard mapping, if the keyboard does not have cursor keys, or if the terminal you are using does not recognize cursor keystrokes.

The **gvim** editor is a graphical version of **vim**, but features menus that make the editing task a bit easier. Using **vim** and **gvim** can make a lot of sense, especially if you have limited hard drive space and memory on your system. Like **vim**, you can start **gvim** from the command line like this:

```bash
$ gvim
```

If you are running an active X session, the **gvim** editor will appear, as shown in Figure 6.1.

If you prefer, you can use **vim** while running an X session by launching the program from the command line of a terminal window. Take the time to learn the basics of this command, because the knowledge will come in handy as you learn Linux!

![](img/1ea833f5a3e3c1547e3dd2891f52804a_138_0.png)

## Using pico

The `pico` editor, part of the `pine` e-mail package available with most Linux distributions, is a robust, capable editor that works well under a variety of conditions, is easy to learn, and could become your favorite Linux text editor. This editor is copyrighted by the University of Washington, which is viewed as a downside by GNU GPL adherents. You will not find `pico` included with the Debian GNU/Linux distribution.

This editor has most of the desired features of a good Linux text editor, such as built-in help, searching, the ability to toggle line-wrapping from the command line, block move, copy, delete, and spell-check. One of `pico`'s best features is its ability save your document with the name of your file and an extension of `.save` in the event of a system crash or interrupted `telnet` session.

You can start `pico` from the command line of the console or an `X` terminal window like this:

```bash
$ pico myfile.txt
```

After you press Enter, the file `myfile.txt` will be opened for editing, or the file will be created if it does not exist. You can also use `pico` while editing your system's
