
## 2.3.3.1 The Info pages

In addition to the man pages, you can read the Info pages about a command, using the *info* command. These usually contain more recent information and are somewhat easier to use. The man pages for some commands refer to the Info pages.

Get started by typing *info info* in a terminal window:

```text
File: info.info,  Node: Top,  Next: Getting Started,  Up: (dir)

Info: An introduction
***************

Info is a program, which you are using now, for reading
documentation of computer programs.  The GNU Project distributes most
of its on-line manuals in the Info format, so you need a program called
"Info reader" to read the manuals.  One of such programs you are using
now.

   If you are new to Info and want to learn how to use it, type the
command 'h' now.  It brings you to a programmed instruction sequence.

   To learn advanced Info commands, type 'n' twice.  This brings you to
'Info for Experts', skipping over the 'Getting Started' chapter.

* Menu:

* Getting Started::     Getting started using an Info reader.
* Advanced Info::       Advanced commands within Info.
* Creating an Info File::     How to make your own Info file.
--zz-Info: (info.info.gz)Top,  24 lines --Top------------
Welcome to Info version 4.2. Type C-h for help, m for menu item.
```

Use the arrow keys to browse through the text and move the cursor on a line starting with an asterisk, containing the keyword about which you want info, then hit *Enter*. Use the *P* and *N* keys to go to the previous or next subject. The space bar will move you one page further, no matter whether this starts a new subject or an Info page for another command. Use *Q* to quit. The *info* program has more information.

### 2.3.3.2 The whatis and apropos commands

A short index of explanations for commands is available using the *whatis* command, like in the examples below:

```bash
[your_prompt] whatis ls
ls     (1)  - list directory contents
```

This displays short information about a command, and the first section in the collection of man pages that contains an appropriate page.

If you don't know where to get started and which man page to read, **apropos** gives more information. Say that you don't know how to start a browser, then you could enter the following command:

```text
another prompt> **apropos browser**
Galeon [galeon] (1) - gecko-based GNOME web browser
lynx (1) - a general purpose distributed information browser
for the World Wide Web
ncftp (1) - Browser program for the File Transfer Protocol
opera (1) - a graphical web browser
pilot (1) - simple file system browser in the style of the
Pine Composer
pinfo (1) - curses based lynx-style info browser
pinfo [pman] (1) - curses based lynx-style info browser
viewers (1x) - graphical class browser for Xt
```

After pressing **Enter** you will see that a lot of browser related stuff is on your machine: not only web browsers, but also file and FTP browsers, and browsers for documentation. If you have development packages installed, you may also have the accompanying man pages dealing with writing programs having to do with browsers. Generally, a command with a man page in section one, so one marked with "(1)", is suitable for trying out as a user. The user who issued the above **apropos** might consequently try to start the commands **galeon**, **lynx** or **opera**, since these clearly have to do with browsing the world wide web.

### 2.3.3.3 The --help option

Most GNU commands support the --help, which gives a short explanation about how to use the command and a list of available options. Below is the output of this option with the **cat** command:

```text
userprompt@host: cat --help
Usage: cat [OPTION] [FILE]...
Concatenate FILE(s), or standard input, to standard output.

 -A, --show-all equivalent to -vET
 -b, --number-nonblank number nonblank output lines
 -e equivalent to -vE
 -E, --show-ends display $ at end of each line
 -n, --number number all output lines
 -s, --squeeze-blank never more than one single blank line
 -t equivalent to -vT
 -T, --show-tabs display TAB characters as ^I
 -u (ignored)
 -v, --show-nonprinting use ^ and M- notation, except for LFD and TAB
 --help display this help and exit
 --version output version information and exit

With no FILE, or when FILE is -, read standard input.

Report bugs to <bug-texutils@gnu.org>.
```

### 2.3.3.4 Graphical help

Don't despair if you prefer a graphical user interface. Konqueror, the default KDE file manager, provides painless and colourful access to the man and Info pages. You may want to try `info:info` in the *Location* address bar, and you will get a browsable Info page about the **info** command. Similarly, `man:ls` will present you with the man page for the **ls** command. You even get command name completion: you will see the man pages for all the commands starting with "ls" in a scroll-down menu.

Entering `info:/dir` in the address location toolbar displays all the Info pages, arranged in utility categories. Excellent Help content, including the Konqueror Handbook. Start up from the menu or by typing the command **konqueror** in a terminal window, followed by **Enter**; see the screenshot below.

![](img/996aa590a5237ef824c7c29efdbb64f8_48_0.png)

The Gnome Help Browser is very user friendly as well. You can start it selecting Applications->Help from the Gnome menu, by clicking the lifeguard icon on your desktop or by entering the command **gnome-help** in a terminal window. The system documentation and man pages are easily browsable with a plain interface.

The **nautilus** file manager provides a searchable index of the man and Info pages, they are easily browsable and interlinked. Nautilus is started from the command line, or clicking your home directory icon, or from the Gnome menu.

The big advantage of GUIs for system documentation is that all information is completely interlinked, so you can click through in the "SEE ALSO" sections and wherever links to other man pages appear, and thus browse and acquire knowledge without interruption for hours at the time.

### 2.3.3.5 Exceptions

Some commands don't have separate documentation, because they are part of another command. **cd**, **exit**, **logout** and **pwd** are such exceptions. They are part of your shell program and are called *shell built-in* commands. For information about these, refer to the man or info page of your shell. Most beginning Linux users have a Bash shell. See Section 3.2.3.2 for more about shells.

If you have been changing your original system configuration, it might also be possible that man pages are still there, but not visible because your shell environment has changed. In that case, you will need to check the MANPATH variable. How to do this is explained in Section 7.2.1.2.

Some programs or packages only have a set of instructions or references in the directory */usr/share/doc*. See Section 3.3.4 to display.

In the worst case, you may have removed the documentation from your system by accident (hopefully by accident, because it is a very bad idea to do this on purpose). In that case, first try to make sure that there is really nothing appropriate left using a search tool, read on in Section 3.3.3. If so, you may need to re-install the package that contains the command to which the documentation applied, see Section 7.5.

## 2.4 Summary

Linux traditionally operates in text mode or in graphical mode. Since CPU power and RAM are not the cost anymore these days, every Linux user can afford to work in graphical mode and will usually do so. This does not mean that you don't have to know about text mode: we will work in the text environment throughout this course, using a terminal window.
