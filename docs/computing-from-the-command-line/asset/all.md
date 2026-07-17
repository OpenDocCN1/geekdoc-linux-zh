![](media/cli_computing_ls.png)

1.  [Cover](text/cover.xhtml)
2.  [Table of contents](#nav.xhtml_toc)

# Preface

This book aims to teach Linux command line tools and Shell Scripting for beginner to intermediate level users. The focus is towards managing your files and performing text processing tasks. Topics like system administration and networking won't be discussed, but some details might get covered in future versions of this book.

## Prerequisites

You should be familiar with basic computer usage, know fundamental terms like files and directories, how to install programs and so on. You should also be already comfortable with programming basics like variables, loops and functions.

In terms of software, you should have access to the `GNU bash` shell and commonly used Linux command line tools. This could be as part of a Linux distribution or via other means such as a Virtual Machine, WSL (Windows Subsystem for Linux) and so on. More details about the working environment will be discussed in the introductory chapters.

You are also expected to get comfortable with reading manuals, searching online, visiting external links provided for further reading, tinkering with illustrated examples, asking for help when you are stuck and so on. In other words, be proactive and curious instead of just consuming the content passively.

See my curated list on [Linux CLI and Shell Scripting](https://learnbyexample.github.io/curated_resources/linux_cli_scripting.html) for more learning resources.

## Conventions

*   Code snippets shown are copy pasted from the `bash` shell (version **5.0.17**) and modified for presentation purposes. Some commands are preceded by comments to provide context and explanations, blank lines have been added to improve readability and so on.
*   External links are provided throughout the book for you to explore certain topics in more depth.
*   The [cli-computing repo](https://github.com/learnbyexample/cli-computing) has all the [example files and scripts](https://github.com/learnbyexample/cli-computing/tree/master/example_files) used in the book. The repo also includes all the [exercises](https://github.com/learnbyexample/cli-computing/blob/master/exercises/exercises.md) as a single file, along with a separate [solutions](https://github.com/learnbyexample/cli-computing/blob/master/exercises/exercise-solutions.md) file. If you are not familiar with `git` command, click the **Code** button on the webpage to get the files.
*   See the [Setup](#ch002.xhtml_setup) section for instructions to create a working environment for following along the contents presented in this book.

## Acknowledgements

*   [GNU Manuals](https://www.gnu.org/manual/manual.html) — documentation for command line tools and the `bash` shell
*   [stackoverflow](https://stackoverflow.com/) and [unix.stackexchange](https://unix.stackexchange.com/) — for getting answers on pertinent questions related to CLI tools
*   [tex.stackexchange](https://tex.stackexchange.com/) — for help on [pandoc](https://github.com/jgm/pandoc/) and `tex` related questions
*   [/r/commandline/](https://old.reddit.com/r/commandline), [/r/linux4noobs/](https://old.reddit.com/r/linux4noobs/), [/r/linuxquestions/](https://old.reddit.com/r/linuxquestions/) and [/r/linux/](https://old.reddit.com/r/linux/) — helpful forums
*   [canva](https://www.canva.com/) — cover image
*   [Warning](https://commons.wikimedia.org/wiki/File:Warning_icon.svg) and [Info](https://commons.wikimedia.org/wiki/File:Info_icon_002.svg) icons by [Amada44](https://commons.wikimedia.org/wiki/User:Amada44) under public domain
*   [carbon](https://carbon.now.sh/) — creating terminal screenshots with highlighted text
*   [oxipng](https://github.com/shssoichiro/oxipng), [pngquant](https://pngquant.org/) and [svgcleaner](https://github.com/RazrFalcon/svgcleaner) — optimizing images

## Feedback and Errata

I would highly appreciate if you'd let me know how you felt about this book. It could be anything from a simple thank you, pointing out a typo, mistakes in code snippets, which aspects of the book worked for you (or didn't!) and so on. Reader feedback is essential and especially so for self-published authors.

You can reach me via:

*   Issue Manager: [https://github.com/learnbyexample/cli-computing/issues](https://github.com/learnbyexample/cli-computing/issues)
*   E-mail: [learnbyexample.net@gmail.com](mailto:learnbyexample.net@gmail.com)
*   Twitter: [https://twitter.com/learn_byexample](https://twitter.com/learn_byexample)

## Author info

Sundeep Agarwal is a lazy being who prefers to work just enough to support his modest lifestyle. He accumulated vast wealth working as a Design Engineer at Analog Devices and retired from the corporate world at the ripe age of twenty-eight. Unfortunately, he squandered his savings within a few years and had to scramble trying to earn a living. Against all odds, selling programming ebooks saved his lazy self from having to look for a job again. He can now afford all the fantasy ebooks he wants to read and spends unhealthy amount of time browsing the internet.

When the creative muse strikes, he can be found working on yet another programming ebook (which invariably ends up having at least one example with regular expressions). Researching materials for his ebooks and everyday social media usage drowned his bookmarks, so he maintains curated resource lists for sanity sake. He is thankful for free learning resources and open source tools. His own contributions can be found at [https://github.com/learnbyexample](https://github.com/learnbyexample).

**List of books:** [https://learnbyexample.github.io/books/](https://learnbyexample.github.io/books/)

## License

This work is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-nc-sa/4.0/)

Code snippets are available under [MIT License](https://github.com/learnbyexample/cli-computing/blob/master/LICENSE)

Resources mentioned in the Acknowledgements section above are available under original licenses.

## Book version

1.0

See [Version_changes.md](https://github.com/learnbyexample/cli-computing/blob/master/Version_changes.md) to track changes across book versions.

# Introduction and Setup

Back in 2007, I had a rough beginning as a design engineer at a semiconductor company in terms of utilizing software tools. Linux command line, Vim and Perl were all new to me. In addition to learning about command line tools from colleagues and supervisors, I remember going through and making notes in a photocopied book (unable to recall the title now).

The biggest pain points were not knowing about handy options (for example, `grep --color` to highlight matching portions, `find -exec` to apply commands on filtered files, etc) and tools (for example, `xargs` to workaround limitations of too many command line arguments). And then there were tools like `sed` and `awk` with intimidating syntax. I'm at a loss to reason out why I didn't utilize shell scripts much. I stuck to Perl and Vim instead of learning such handy tools. I also did not know about forums like [stackoverflow](https://stackoverflow.com/) and [unix.stackexchange](https://unix.stackexchange.com/) until after I left my job in 2014.

I started collating what I knew about Linux command line tools when I got chances to conduct scripting course workshops for college students. From 2016 to 2018, I started maintaining my tutorials on Linux command line, Vim and scripting languages as GitHub repos. As you might guess, I then started polishing these materials and [published them as ebooks](https://learnbyexample.github.io/books/). This is an ongoing process, with **Computing from the Command Line** being the thirteenth ebook.

This book aims to teach Linux command line tools and Shell Scripting for beginner to intermediate level users. Plenty of examples are provided to make it easier to understand a particular tool and its various features. External links are provided for further reading. Important notes and warnings are formatted to stand out from normal text.

Writing a book always has a few pleasant surprises for me. This time I learned handy options like `mkdir -m` and `chmod =`, got better understanding of many shell features and so on. I'm also planning to learn and present more command line tools for the next version of this book.

This chapter will give a brief introduction to Linux. You'll also see suggestions and instructions for setting up a command line environment to follow along the contents presented in this book.

## Linux overview

Quoting selective parts from [wikipedia](https://en.wikipedia.org/wiki/Linux):

> Linux is a family of open-source Unix-like operating systems based on the Linux kernel, an operating system kernel first released on September 17, 1991, by Linus Torvalds. Linux is typically packaged in a Linux distribution.
> 
> Linux was originally developed for personal computers based on the Intel x86 architecture, but has since been ported to more platforms than any other operating system. Because of the dominance of the Linux-based Android on smartphones, Linux also has the largest installed base of all general-purpose operating systems.
> 
> Linux is one of the most prominent examples of free and open-source software collaboration. The source code may be used, modified and distributed commercially or non-commercially by anyone under the terms of its respective licenses, such as the GNU General Public License.

Apart from Linux exposure during my previous job, I've been using Linux as my desktop system since 2014 and it is very well suited for my needs. Compared to my Windows experience, Linux is light weight, secure, stable, fast and more importantly doesn't force you to upgrade hardware. Read the wikipedia article linked above for a more comprehensive coverage about Linux, where it is used and so on.

## Linux Distros

Quoting again from [wikipedia](https://en.wikipedia.org/wiki/Linux_distribution):

> A Linux distribution (often abbreviated as distro) is an operating system made from a software collection that is based upon the Linux kernel and, often, a package management system. Linux users usually obtain their operating system by downloading one of the Linux distributions, which are available for a wide variety of systems ranging from embedded devices (for example, OpenWrt) and personal computers (for example, Linux Mint) to powerful supercomputers (for example, Rocks Cluster Distribution).

I use Ubuntu, which is beginner friendly. Here are some resources to help you choose a distro:

*   [/r/linux4noobs wiki](https://old.reddit.com/r/linux4noobs/wiki/distro_selection) — selection guide for noobs
*   [List of Linux distributions](https://en.wikipedia.org/wiki/List_of_Linux_distributions) — general information about notable Linux distributions in the form of a categorized list
*   [DistroWatch](https://distrowatch.com/) — website dedicated to talking about, reviewing and keeping up to date with open source operating systems. This site particularly focuses on Linux distributions and flavours of BSD, though other open source operating systems are sometimes discussed
*   [Light Weight Linux Distros](https://en.wikipedia.org/wiki/Light-weight_Linux_distribution) — uses lower memory and/or has less processor-speed requirements than a more "feature-rich" Linux distribution

## Access to Linux environment

You'll usually find installation instructions from the respective distro website you wish to install. Alternatively, you can install Linux on a [virtual machine](https://en.wikipedia.org/wiki/Virtual_machine) or try it online. Here are some resources to get you started:

*   [Install Ubuntu desktop](https://ubuntu.com/tutorials/install-ubuntu-desktop)
*   [How to run Ubuntu Desktop on a virtual machine using VirtualBox](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox)
*   [DistroTest](https://distrotest.net/index.php) — test a distro directly online without installation

If you are already on Windows or macOS, the following options can be used to get access to Linux tools:

*   [Git for Windows](https://git-scm.com/downloads) — provides a Bash emulation used to run Git from the command line
*   [Windows Subsystem for Linux](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux) — compatibility layer for running Linux binary executables natively on Windows
*   [brew](https://brew.sh/) — Package Manager for macOS (or Linux)

> ![info](media/file0.svg) ![info](media/file0.svg) ![warning](media/file1.svg) If you are completely new to command line usage, I'd recommend setting up a virtual machine. Or perhaps, a secondary computer that you are free to experiment with. Mistakes in command line can be more destructive compared to the graphical interface. For example, a single space typo can result in data loss, leave your machine unusable, etc.

## Setup

To follow along the contents presented in this book, you'll need files from my [cli-computing repo](https://github.com/learnbyexample/cli-computing). Once you have access to a Linux environment, follow the instructions shown below. If all the commands used below seem alien to you, wait until you reach the [ls](#ch004.xhtml_ls) section (you'll get a link back to these instructions at that point).

To get the files, you can clone the cli-computing repo using the `git` command or download a `zip` version. You may have to install the `git` command if you don't already have it, for example `sudo apt install git` on Debian-like systems. See [https://git-scm.com/downloads](https://git-scm.com/downloads) for other installation choices.

```
[](#cb1-1)# option 1: use git
[](#cb1-2)$ git clone --depth 1 https://github.com/learnbyexample/cli-computing.git
[](#cb1-3)
[](#cb1-4)# option 2: download zip file
[](#cb1-5)# you can also use 'curl -OL' instead of 'wget'
[](#cb1-6)$ wget https://github.com/learnbyexample/cli-computing/archive/refs/heads/master.zip
[](#cb1-7)$ unzip master.zip
[](#cb1-8)$ mv cli-computing-master cli-computing
```

Once you have the files, you'll be able to follow along the commands presented in this book. For example, you'll need to execute the `ls.sh` script for the [ls](#ch004.xhtml_ls) section.

```
[](#cb2-1)$ cd cli-computing/example_files/scripts/
[](#cb2-2)$ ls
[](#cb2-3)cp.sh  file.sh  globs.sh  ls.sh  rm.sh    tar.sh
[](#cb2-4)du.sh  find.sh  grep.sh   mv.sh  stat.sh  touch.sh
[](#cb2-5)
[](#cb2-6)$ source ls.sh
[](#cb2-7)$ ls -F
[](#cb2-8)backups/    hello_world.py*  ip.txt     report.log  todos/
[](#cb2-9)errors.log  hi*              projects/  scripts@
```

For sections like the [cat](#ch006.xhtml_cat) command, you'll need to use the sample input files provided in the `text_files` directory.

```
[](#cb3-1)$ cd cli-computing/example_files/text_files/
[](#cb3-2)$ cat greeting.txt 
[](#cb3-3)Hi there
[](#cb3-4)Have a nice day
```

## Command Line Interface

Command Line Interface (CLI) allows you to interact with the computer using text commands. For example, the `cd` command helps you navigate to a particular directory. The `ls` command shows the contents of a directory. In a graphical environment, you'd use an explorer (file manager) for navigation and directory contents are shown by default. Some tasks can be accomplished in both CLI and GUI environments, while some are suitable and effective only in one of them.

Here are some advantages of using CLI tools over GUI programs:

*   automation
*   faster execution
*   command invocations are repeatable
*   easy to save solutions and share with others
*   single environment compared to different UI/UX with graphical solutions
*   common text interface allows tools to easily communicate with each other

And here are some disadvantages:

*   steep learning curve
*   syntax can get very complicated
*   need to get comfortable with plenty of tools
*   typos have a tendency to be more destructive

You can make use of features like command history, shortcuts and autocompletion to help with plethora of commands and syntax issues. Consistent practice will help to get familiar with quirks of the command line environment. Commands with destructive potential will usually include options to allow manual confirmation and interactive usage, thus reducing or entirely avoiding the impact of typos.

## Chapters

Here's the list of remaining chapters:

*   [Command Line Overview](#ch003.xhtml_command-line-overview)
*   [Managing Files and Directories](#ch004.xhtml_managing-files-and-directories)
*   [Shell Features](#ch005.xhtml_shell-features)
*   [Viewing Part or Whole File Contents](#ch006.xhtml_viewing-part-or-whole-file-contents)
*   [Searching Files and Filenames](#ch007.xhtml_searching-files-and-filenames)
*   [File Properties](#ch008.xhtml_file-properties)
*   [Managing Processes](#ch009.xhtml_managing-processes)
*   [Multipurpose Text Processing Tools](#ch010.xhtml_multipurpose-text-processing-tools)
*   [Sorting Stuff](#ch011.xhtml_sorting-stuff)
*   [Comparing Files](#ch012.xhtml_comparing-files)
*   [Assorted Text Processing Tools](#ch013.xhtml_assorted-text-processing-tools)
*   [Shell Scripting](#ch014.xhtml_shell-scripting)
*   [Shell Customization](#ch015.xhtml_shell-customization)

## Resource lists

This book covers but a tiny portion of Linux command line usage. Topics like system administration and networking aren't discussed at all. Check out the following lists to learn about such topics and discover cool tools:

*   [Linux curated resources](https://learnbyexample.github.io/curated_resources/linux_cli_scripting.html) — my collection of resources for Linux command line, shell scripting and other related topics
*   [Awesome Linux](https://github.com/inputsh/awesome-linux) — list of awesome projects and resources that make Linux even more awesome
*   [Arch wiki: list of applications](https://wiki.archlinux.org/title/List_of_applications) — sorted by category, helps as a reference for those looking for packages

# Command Line Overview

This chapter will help you take the first steps in the command line world. Apart from command examples that you can try out, you'll also learn a few essential things about working in a text environment.

For newbies, the sudden paradigm shift to interacting with the computer using just text commands can be overwhelming, especially for those accustomed to the graphical user interface (GUI). After regular usage, things will start to look systematic and you might realize that GUI is ill suited for repetitive tasks. With continuous use, recalling various commands will become easier. Features like command line history, aliases, tab-completion and shortcuts will help too.

If you've used a scientific calculator, you'd know that it is handy with too many functionalities cramped into a tiny screen and a plethora of multipurpose buttons. Command line environment is something like that, but not limited just to mathematics. From managing files to munging data, from image manipulations to working with video, you'll likely find a tool for almost any computing task you can imagine. Always remember that command line tools appeared long before graphical ones did. The rich history shows its weight in the form of robust tools and the availability of wide variety of applications.

## Hello Command Line

Open a [Terminal Emulator](https://en.wikipedia.org/wiki/Terminal_emulator) and type the command as shown below. The `$` followed by a space character at the start is the simple command prompt that I use. It might be different for you. The actual command to type is `echo` followed by a space, then the argument `'Hello Command Line'` and finally press the `Enter` key to execute it. You should get the argument echoed back to you as the command output.

```
[](#cb4-1)$ echo 'Hello Command Line'
[](#cb4-2)Hello Command Line
```

Here's another simple illustration. This time, the command `pwd` is entered by itself (i.e. no arguments). You should get *your* current location as the output. The `/` character separates different parts of the location (more details in the upcoming sections).

```
[](#cb5-1)$ pwd
[](#cb5-2)/home/learnbyexample
```

Next, enter the `exit` command to quit the Terminal session.

```
[](#cb6-1)$ exit
```

If you are completely new to the command line world, try out the above steps a few more times until you feel comfortable with opening a Terminal Emulator, executing commands and quitting the session. More details about the command structure, customizing command prompt, etc will be discussed later.

## File System

In Linux, directory structure starts with the `/` symbol, which is referred to as the **root** directory. The `man hier` command gives description of the file system hierarchy. Here are some selected examples:

*   `/` This is the root directory. This is where the whole tree starts.
*   `/bin` This directory contains executable programs which are needed in single user mode and to bring the system up or repair it.
*   `/home` On machines with home directories for users, these are usually beneath this directory, directly or not. The structure of this directory depends on local administration decisions (optional).
*   `/tmp` This directory contains temporary files which may be deleted with no notice, such as by a regular job or at system boot up.
*   `/usr` This directory is usually mounted from a separate partition. It should hold only shareable, read-only data, so that it can be mounted by various machines running Linux.
*   `/usr/bin` This is the primary directory for executable programs. Most programs executed by normal users which are not needed for booting or for repairing the system and which are not installed locally should be placed in this directory.
*   `/usr/share` This directory contains subdirectories with specific application data, that can be shared among different architectures of the same OS.

## Absolute and Relative paths

Quoting [wikipedia](https://en.wikipedia.org/wiki/Path_%28computing%29#Absolute_and_relative_paths):

> An **absolute** or **full** path points to the same location in a file system regardless of the current working directory. To do that, it must contain the root directory.

> By contrast, a **relative** path starts from some given working directory, avoiding the need to provide the full absolute path. A filename can be considered as a relative path based at the current working directory. If the working directory is not the file's parent directory, a file not found error will result if the file is addressed by its name.

For example, `/home/learnbyexample` is an absolute path and `../design` is a relative path. You'll learn how paths are used for performing tasks in the coming chapters.

## Shells and Terminal Emulators

These terms are often used to interchangeably mean the same thing — a prompt to allow the user to execute commands. However, they are quite different:

*   **Shell** is a command line interpreter. Sets the syntax rules for invoking commands, provides operators to connect commands and redirect data, has scripting features like loops, functions and so on
*   **Terminal** is a text input/output environment. Responsible for visual details like font size, color, etc

Some of the popular shells are `bash`, `zsh` and `fish`. This book will discuss only the [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) shell. Some of the popular terminal emulators are [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal), [konsole](https://en.wikipedia.org/wiki/Konsole), [xterm](https://en.wikipedia.org/wiki/Xterm) and [alacritty](https://github.com/alacritty/alacritty).

Quoting from [wikipedia: Unix shell](https://en.wikipedia.org/wiki/Unix_shell):

> A Unix shell is a command-line interpreter or shell that provides a command line user interface for Unix-like operating systems. The shell is both an interactive command language and a scripting language, and is used by the operating system to control the execution of the system using shell scripts.
> 
> Users typically interact with a Unix shell using a terminal emulator; however, direct operation via serial hardware connections or Secure Shell are common for server systems. All Unix shells provide filename wildcarding, piping, here documents, command substitution, variables and control structures for condition-testing and iteration.

Shell features will be discussed in later sections and chapters. For now, open a terminal and try out the following commands:

```
[](#cb7-1)$ cat /etc/shells
[](#cb7-2)# /etc/shells: valid login shells
[](#cb7-3)/bin/sh
[](#cb7-4)/bin/dash
[](#cb7-5)/bin/bash
[](#cb7-6)/bin/rbash
[](#cb7-7)
[](#cb7-8)$ echo "$SHELL"
[](#cb7-9)/bin/bash
```

In the above example, the `cat` command is used to display the contents of a file and the `echo` command is used to display the contents of a variable. `SHELL` is an environment variable containing full path to the shell.

> ![info](media/file2.svg) The output of the above commands might be different for you. And as mentioned earlier, your command prompt might be different than `$` . For now, you can ignore it. Or, you could type `PS1='$ '` and press the `Enter` key to set the prompt for the current session.

**Further Reading**

*   [unix.stackexchange: What is the exact difference between a 'terminal', a 'shell', a 'tty' and a 'console'?](https://unix.stackexchange.com/q/4126/109046)
*   [wikipedia: Comparison of command shells](https://en.wikipedia.org/wiki/Comparison_of_command_shells)
*   [unix.stackexchange: Difference between login shell and non-login shell](https://unix.stackexchange.com/q/38175/109046)
*   [Features and differences between various shells](http://www.faqs.org/faqs/unix-faq/shell/shell-differences/)
*   [Syntax comparison on different shells with examples](https://hyperpolyglot.org/unix-shells)
*   [Shell, choosing shell and changing default shells](https://wiki.ubuntu.com/ChangingShells)

## Unix Philosophy

Quoting from [wikipedia: Unix Philosophy](https://en.wikipedia.org/wiki/Unix_philosophy):

> *   Write programs that do one thing and do it well.
>     
>     
> *   Write programs to work together.
>     
>     
> *   Write programs to handle text streams, because that is a universal interface.

These principles do not strictly apply to all the command line tools, but it is good to be aware of them. As you get familiar with working from the command line, you'll be able to appreciate these guidelines better.

## Command Structure

It is not necessary to fully understand the commands used in this chapter, just the broad strokes. The examples are intended to help you get a feel for the basics of using command options and arguments.

**Command invocation without any options or arguments**:

*   `clear` clear the terminal screen
*   `date` show the current date and time

**Command with options (flags)**:

*   `ls -l` list directory contents in a long listing format
*   `ls -la` list directory contents including hidden files in long listing format
    *   two short options `-l` and `-a` are combined together here as `-la`
*   `df -h` report file system disk space usage sizes in human readable format
*   `df --human-readable` same as `df -h` but using long option instead of short option

**Command with arguments**:

*   `mkdir project` create a directory named `project` in the current working directory
*   `man sort` manual page for the `sort` command
*   `diff file1.txt file2.txt` display differences between the two input files
*   `wget https://s.ntnu.no/bashguide.pdf` download a file from the internet
    *   the link passed to `wget` in the above example is real, visit [BashGuide](https://mywiki.wooledge.org/BashGuide) for details

**Command with both options and arguments**:

*   `rm -r project` remove (delete) the `project` directory recursively
*   `paste -sd, ip.txt` serialize all lines from the input file to a single line using `,` as the delimiter

**Single quotes vs Double quotes**:

*   **Single quotes** preserves the literal value of each character within the quotes
*   **Double quotes** preserves the literal value of all characters within the quotes, with the exception of `$`, `` ` ``, `\`, and, when history expansion is enabled, `!`

```
[](#cb8-1)# no character is special within single quotes
[](#cb8-2)$ echo '$SHELL'
[](#cb8-3)$SHELL
[](#cb8-4)
[](#cb8-5)# $ is special within double quotes, used to interpolate variable here
[](#cb8-6)$ echo "Full path to the shell: $SHELL"
[](#cb8-7)Full path to the shell: /bin/bash
```

More details and other types of quoting will be discussed in the [Shell Features](#ch005.xhtml_shell-features) chapter.

## Command Network

One of the *Unix Philosophy* seen earlier mentioned commands working together. The shell provides several ways to do so. A commonly used feature is redirecting the output of a command — as input of another command, to be saved in a file and so on.

*   to another command
    *   `du -sh * | sort -h` calculate size of files and folders in human-readable format using `du` and then sort them using a tool specialized for that task
*   to a file
    *   `grep 'pass' *.log > pass_list.txt` write the results to a file instead of displaying on the terminal (if the file already exists, it gets overwritten)
    *   `grep 'error' *.log >> errors.txt` append the results to the given file (creates a new file if necessary)
*   to a variable
    *   `d=$(date)` save command output in a variable named `d`

Many more of such shell features will be discussed in later chapters.

## Scripting

Not all operations can be completed using a one-liner from the terminal. In such cases, you can save the instructions in a text file and then execute them. Open your favorite text editor and write the three lines shown below:

```
[](#cb9-1)$ cat cmds.sh
[](#cb9-2)echo 'hello world'
[](#cb9-3)echo 'how are you?'
[](#cb9-4)seq 3
```

As an alternate to using a text editor, you can use either of the commands shown below to create this file.

```
[](#cb10-1)# assuming 'echo' supports '-e' option in your environment
[](#cb10-2)$ echo -e "echo 'hello world'\necho 'how are you?'\nseq 3" > cmds.sh
[](#cb10-3)
[](#cb10-4)# a more portable solution using the builtin 'printf' command
[](#cb10-5)$ printf "echo 'hello world'\necho 'how are you?'\nseq 3\n" > cmds.sh
```

The script file is named `cmds.sh` and has three commands in three separate lines. One way to execute the contents of this file is by using the `source` command:

```
[](#cb11-1)$ source cmds.sh
[](#cb11-2)hello world
[](#cb11-3)how are you?
[](#cb11-4)1
[](#cb11-5)2
[](#cb11-6)3
```

> ![info](media/file0.svg) Your Linux distro is likely to have an easy to use graphical text editor such as `gedit` and `mousepad`. See [wiki.archlinux: text editors](https://wiki.archlinux.org/title/List_of_applications#Text_editors) for a huge list of editors to choose from.

> ![info](media/file0.svg) The [Shell Scripting](#ch014.xhtml_shell-scripting) chapter will discuss scripting in more detail.

## Command Help

Most distros for personal use come with documentation for commands already installed. Learning how to use manuals from the terminal is handy and there are ways to get specific information as well.

### man

The `man` command is an interface to view manuals from within the terminal itself. This uses a `pager` (which is usually the `less` command) to display the contents. You could call these commands as terminal user interface (TUI) applications. As an example, type `man cat` and you should see something like the screenshot shown below:

![manual page for the cat command](media/file3.png)

Since the documentation has several lines that doesn't completely fit within the terminal window, you will get only the starting part of the manual. You have several options to navigate:

*   `↑` and `↓` arrow keys to move up and down by a line
    *   you can also use `k` and `j` keys (same keys as those used in the Vim text editor)
*   `f` and `b` keys to move forward and backward by a screenful of content
    *   `Space` key also moves forward by a screen
*   mouse scroll moves up and down by a few lines
*   `g` or `Home` go to the start of the manual
*   `G` or `End` go to the end of the manual
*   `/pattern` followed by `Enter` search for the given pattern in the forward direction
*   `?pattern` followed by `Enter` search for the given pattern in the backward direction
*   `n` go to the next match
*   `N` go to the previous match
*   `q` quit

As you might have noticed in the screenshot above, you can use `h` for help about the `less` command itself. Here are some useful tips related to documentation:

*   `man man` gives information about the `man` command itself
*   `man bash` will give you the manual page for the `bash` shell
    *   since this is very long, I'd recommend using the [online GNU Bash manual](https://www.gnu.org/software/bash/manual/)
*   `man find | gvim -` open the manual page in your favorite text editor
*   `man -k printf` search the short descriptions in all the manual pages for the string `printf`
    *   you can also use the `apropos` command instead of `man -k`
*   `wc --help` many commands support the `--help` option to give succinct details like options and syntax
    *   also, these details will be displayed on the terminal itself, no need to deal with `pager` interface

> ![info](media/file2.svg) See also [unix.stackexchange: How do I use man pages to learn how to use commands?](https://unix.stackexchange.com/q/193815/109046) and [unix.stackexchange: colors in man pages](https://unix.stackexchange.com/q/119/109046).

> ![info](media/file0.svg) ![info](media/file0.svg) ![info](media/file0.svg) The Linux manual pages are usually shortened version of the full documentation. You can use the `info` command to view the complete documentation for GNU tools. `info` is also a TUI application, but with different key configuration compared to the `man` command. See [GNU Manuals Online](https://www.gnu.org/manual/manual.html) if you'd prefer to read them from a web browser. You can also download them in formats like PDF for offline usage.

### type

For certain operations, the shell provides its own set of commands, known as builtin commands. The `type` command displays information about a command like its path, whether it is a builtin, alias, function and so on.

```
[](#cb12-1)$ type cd
[](#cb12-2)cd is a shell builtin
[](#cb12-3)$ type sed
[](#cb12-4)sed is /bin/sed
[](#cb12-5)$ type type
[](#cb12-6)type is a shell builtin
[](#cb12-7)
[](#cb12-8)# multiple commands can be given as arguments
[](#cb12-9)$ type pwd awk
[](#cb12-10)pwd is a shell builtin
[](#cb12-11)awk is /usr/bin/awk
```

As will be discussed in the [Shell Customization](#ch015.xhtml_shell-customization) chapter, you can create aliases to customize command invocations. You can use the `type` command to reveal the nature of such aliases. Here are some examples based on aliases I use:

```
[](#cb13-1)$ type p
[](#cb13-2)p is aliased to 'pwd'
[](#cb13-3)
[](#cb13-4)$ type ls
[](#cb13-5)ls is aliased to 'ls --color=auto'
```

The `type` command formats the command output with a backtick at the start and a single quotes at the end. That doesn't play well with syntax highlighting, so I've changed the backtick to single quotes in the above illustration.

> ![info](media/file0.svg) See also [unix.stackexchange: What is the difference between a builtin command and one that is not?](https://unix.stackexchange.com/q/11454/109046)

### help

The `help` command provides documentation for builtin commands. Unlike the `man` command, the entire text is displayed as the command output. A help page in the default format is shown below. You can add `-m` option if you want the help content in a pseudo-manpage format.

```
[](#cb14-1)$ help pwd
[](#cb14-2)pwd: pwd [-LP]
[](#cb14-3)    Print the name of the current working directory.
[](#cb14-4) 
[](#cb14-5)    Options:
[](#cb14-6)      -L        print the value of $PWD if it names the current working directory
[](#cb14-7)      -P        print the physical directory, without any symbolic links
[](#cb14-8) 
[](#cb14-9)    By default, 'pwd' behaves as if '-L' were specified.
[](#cb14-10) 
[](#cb14-11)    Exit Status:
[](#cb14-12)    Returns 0 unless an invalid option is given or the current directory
[](#cb14-13)    cannot be read.
```

You can use the `-d` option to get a short description of the command:

```
[](#cb15-1)$ help -d compgen
[](#cb15-2)compgen - Display possible completions depending on the options.
```

> ![info](media/file0.svg) Use `help help` for documentation on the `help` command. If you use `help` without any argument, it will display all the internally defined shell commands.

### whatis and whereis

Here are some more ways to get specific information about commands:

*   `whatis` displays one-line manual page descriptions
*   `whereis` locates the binary, source, and manual page files for a command

```
[](#cb16-1)$ whatis grep
[](#cb16-2)grep (1)             - print lines that match patterns
[](#cb16-3)
[](#cb16-4)$ whereis awk
[](#cb16-5)awk: /usr/bin/awk /usr/lib/x86_64-linux-gnu/awk /usr/share/awk
[](#cb16-6)/usr/share/man/man1/awk.1.gz
```

### ch

[explainshell](https://explainshell.com/) is a web app that shows the help text that matches each argument of the command you type in the app. For example, a screenshot for [tar -xzvf archive.tar.gz](https://explainshell.com/explain?cmd=tar+-xzvf+archive.tar.gz) is shown below:

![explainshell example for the tar command](media/file4.png)

Inspired by this app, I wrote a [Bash script ch](https://github.com/learnbyexample/command_help) to extract information from `man` and `help` pages. Here are some examples:

```
[](#cb17-1)$ ch ls -vX
[](#cb17-2)       ls - list directory contents
[](#cb17-3)
[](#cb17-4)       -v     natural sort of (version) numbers within text
[](#cb17-5)
[](#cb17-6)       -X     sort alphabetically by entry extension
[](#cb17-7)
[](#cb17-8)$ ch type -a
[](#cb17-9)    type - Display information about command type.
[](#cb17-10)
[](#cb17-11)      -a        display all locations containing an executable named NAME;
[](#cb17-12)                includes aliases, builtins, and functions, if and only if
[](#cb17-13)                the '-p' option is not also used
```

### Further Reading

*   [Linux man pages](https://www.mankier.com/) — one of several websites that host man pages online
*   [ArchWiki](https://wiki.archlinux.org/title/Table_of_contents) — comprehensive documentation for Arch Linux and other distributions
*   [Debian Reference](https://www.debian.org/doc/manuals/debian-reference/) — broad overview of the Debian system, covers many aspects of system administration through shell-command examples

## Shortcuts and Autocompletion

There are several shortcuts you can use to be productive at the command line. These will be discussed in the [Shell Customization](#ch015.xhtml_shell-customization) chapter. Here are some examples to give an idea:

*   `Ctrl+u` delete everything to the left of the cursor
*   `Ctrl+k` delete from the current character to the end of the line
*   `Ctrl+c` abort the currently typed command
*   `Ctrl+l` clear the terminal screen and move the prompt to the top, any characters typed as part of the current command will be retained
*   `↑` and `↓` arrow keys to navigate previously used commands from the history
    *   `Ctrl+p` and `Ctrl+n` can also be used instead of arrow keys
    *   you can modify the command before executing such lines from the history

The tab key helps you autocomplete commands, aliases, filenames and so on, depending on the context. If there is only one possible completion, it will be done on single tab press. Otherwise, you can press the tab key twice to get a list of possible matches (if there are any). Here's an example of completing a file path with multiple tab key presses at various stages. Not only does it saves time, it also helps to avoid typos since you are simultaneously verifying the path.

```
[](#cb18-1)# pressing tab after typing '/e' will autocomplete to '/etc/'
[](#cb18-2)$ ls /etc/
[](#cb18-3)
[](#cb18-4)# pressing tab after 'di' will autocomplete to 'dict'
[](#cb18-5)$ ls /etc/dict
[](#cb18-6)# pressing tab twice will show all possible completions
[](#cb18-7)$ ls /etc/dict
[](#cb18-8)dictd/               dictionaries-common/ 
[](#cb18-9)
[](#cb18-10)# type 'i' and press tab to get 'dictionaries-common'
[](#cb18-11)$ ls /etc/dictionaries-common/
[](#cb18-12)
[](#cb18-13)# type 'w' and press tab to get 'words'
[](#cb18-14)$ ls /etc/dictionaries-common/words 
```

The character at which the tab key is pressed in the above example has been cherry picked for illustration purposes. The number of steps would increase if you try pressing tab after each character. With experience, using the tab key for autocompletion will become a natural part of your command line usage.

> ![info](media/file0.svg) You can set an option to combine the features of single and double tab presses into a single tab press. This will be discussed in the [Shell Customization](#ch015.xhtml_shell-customization) chapter.

## Real world use cases

If the command line environment only had file managing features, I'd still use it. Given the wide variety of applications available, I can't imagine going back to using a different GUI application for each use case. My primary work is writing ebooks, blog posts and recording videos. Here are the major CLI tools I use:

*   text processing using `head`, `tail`, `sort`, `grep`, `sed`, `awk` and so on (you'll learn about these commands in later chapters)
*   [git](https://git-scm.com/) — version control
*   [pandoc](https://github.com/jgm/pandoc/) — generating PDF/EPUB book versions from markdown files
*   [mdBook](https://github.com/rust-lang/mdBook) — web version of the books from markdown files
*   [zola](https://github.com/getzola/zola) — static site generator
*   [ImageMagick](https://imagemagick.org/index.php) — image processing like resizing, adding borders, etc
*   [oxipng](https://github.com/shssoichiro/oxipng), [pngquant](https://pngquant.org/) and [svgcleaner](https://github.com/RazrFalcon/svgcleaner) — optimizing images
*   [auto-editor](https://github.com/WyattBlue/auto-editor) — removing silent portions from video recordings
*   [FFmpeg](https://github.com/FFmpeg/FFmpeg) — video processing, padding for example (`FFmpeg` is also a major part of the `auto-editor` solution)

Some of these workflows require additional management, for which I write shell functions or scripts. I do need GUI tools as well, for example, web browser, image viewer, PDF/EPUB viewers, [SimpleScreenRecorder](https://github.com/MaartenBaert/ssr) and so on. Some of these can be handled from within the terminal too, but I prefer GUI for such cases. I do launch some of them from the terminal, primarily for providing the file or url to be opened.

You might wonder what advantage does the command line provide for processing images and videos? Apart from being faster, the custom parameters (like border color, border size, quality percentage, etc) are automatically saved as part of the scripts I create. After that, I can just use a single call to the script instead of waiting for a GUI application to open, navigating to required files, applying custom parameters, saving them after all the required processing is done, closing the application, etc. Also, that single script can use as many tools as needed, whereas with GUI you'll have to repeat such steps with different applications.

## Exercises

> ![info](media/file2.svg) ![info](media/file0.svg) All the exercises are also collated together in one place at [exercises.md](https://github.com/learnbyexample/cli-computing/blob/master/exercises/exercises.md). For solutions, see [exercise-solutions.md](https://github.com/learnbyexample/cli-computing/blob/master/exercises/exercise-solutions.md).

**1)** By default, is `echo` a shell builtin or external command on your system? What command could you use to get an answer for this question?

**2)** What output do you get for the command shown below? Does the documentation help understand the result?

```
[](#cb19-1)$ echo apple     42 'banana     100'
```

**3)** Go through [bash manual: Tilde Expansion](https://www.gnu.org/software/bash/manual/html_node/Tilde-Expansion.html). Is `~/projects` a relative or an absolute path? See [this unix.stackexchange thread](https://unix.stackexchange.com/q/221970/109046) for answers.

**4)** Which key would you use to get help while the `less` command is active?

**5)** How would you bring the 50th line to the top of the screen while viewing a `man` page (assume `less` command is the `pager`)?

**6)** What does the `Ctrl+k` shortcut do?

**7)** Briefly explain the role of the following shell operators:

*a)* `|`
*b)* `>`
*c)* `>>`

**8)** The `whatis` command displays one-line descriptions about commands. But it doesn't seem to work for `whatis type`. What should you use instead?

```
[](#cb20-1)$ whatis cat
[](#cb20-2)cat (1)              - concatenate files and print on the standard output
[](#cb20-3)
[](#cb20-4)$ whatis type
[](#cb20-5)type: nothing appropriate.
[](#cb20-6)
[](#cb20-7)# ???
[](#cb20-8)type - Display information about command type.
```

**9)** What is the role of the `/tmp` directory?

**10)** Give an example each for absolute and relative paths.

**11)** When would you use the `man -k` command?

**12)** Are there any differences between `man` and `info` pages?

# Managing Files and Directories

This chapter presents commands to do things that are typically handled by a file manager in GUI (also known as file explorer). For example, viewing contents of a directory, navigating to other directories, cut/copy/paste files, renaming and so on. Some of the commands used for these purposes are provided by the shell itself.

As a good practice, make it a habit to go through the documentation of the commands you encounter. Getting used to looking up documentation from the command line will come in handy whenever you are stuck. You can also learn and experiment with options you haven't used yet.

> ![info](media/file0.svg) The [example_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files) directory has the scripts used in this chapter. See [Setup](#ch002.xhtml_setup) section for instructions to create the working environment.

## Builtin and External commands

From [bash manual: What is a shell?](https://www.gnu.org/software/bash/manual/bash.html#What-is-a-shell_003f)

> Shells also provide a small set of built-in commands (builtins) implementing functionality impossible or inconvenient to obtain via separate utilities. For example, `cd`, `break`, `continue`, and `exec` cannot be implemented outside of the shell because they directly manipulate the shell itself. The `history`, `getopts`, `kill`, or `pwd` builtins, among others, could be implemented in separate utilities, but they are more convenient to use as builtin commands.

Many of the commands needed for everyday use are external commands, i.e. not part of the shell. Some builtins, `pwd` for example, might also be available as external command on your system (and these might have differences in features too). In such cases the builtin version will be executed by default, which you can override by using the path of the external version.

You can use the `type` command to distinguish between builtin and external commands. The `type` command is a shell builtin, and provides other features too (which will be discussed later). You can use the `-a` option to get all details about the given command.

```
[](#cb21-1)$ type -a cd
[](#cb21-2)cd is a shell builtin
[](#cb21-3)
[](#cb21-4)$ type -a ls
[](#cb21-5)ls is /bin/ls
[](#cb21-6)
[](#cb21-7)$ type -a pwd
[](#cb21-8)pwd is a shell builtin
[](#cb21-9)pwd is /bin/pwd
```

> ![info](media/file2.svg) To look up documentation, use the `help` command for builtins and `man` for external commands (or `info` for complete documentation, where applicable). Use `help help` and `man man` for their own documentation.

> ![info](media/file2.svg) Typing just `help` will give the list of builtins, along with the command's syntax.

## pwd

`pwd` is a shell builtin command to get the current working directory. This helps to orient yourself with respect to the filesystem. The absolute path printed is often handy to copy-paste elsewhere, in a script for example. Some users prefer their terminal emulators and/or shell prompt to always display the current working directory.

```
[](#cb22-1)$ pwd
[](#cb22-2)/home/learnbyexample
```

## cd

`cd` is another shell builtin. This helps to change the current working directory. Here's an example of changing the current working directory using an absolute path:

```
[](#cb23-1)$ pwd
[](#cb23-2)/home/learnbyexample
[](#cb23-3)
[](#cb23-4)# specifying / at end of the path is optional
[](#cb23-5)$ cd /etc
[](#cb23-6)$ pwd
[](#cb23-7)/etc
```

You can use `-` as an argument to go back to the previous working directory. Continuing from the previous example:

```
[](#cb24-1)$ cd -
[](#cb24-2)/home/learnbyexample
```

> ![info](media/file0.svg) Most commands will treat strings starting with `-` as a command option. You can use `--` to tell commands that all the following arguments should *not* be treated as options even if they start with `-`. For example, if you have a folder named `-oops` in the current working directory, you can use `cd -- -oops` to switch to that directory.

Relative paths are well, relative to the current working directory:

*   `.` refers to the current directory
*   `..` refers to the directory one hierarchy above (i.e. parent directory)
*   `../..` refers to the directory two hierarchies above and so on
*   `cd ./-` will help you to switch to a directory named `-` in the current location
    *   you cannot use `cd -` since that'll take you to the previous working directory

```
[](#cb25-1)$ pwd
[](#cb25-2)/home/learnbyexample
[](#cb25-3)
[](#cb25-4)# go one hierarchy above
[](#cb25-5)$ cd ..
[](#cb25-6)$ pwd
[](#cb25-7)/home
[](#cb25-8)
[](#cb25-9)# change to 'learnbyexample' present in the current directory
[](#cb25-10)# './' is optional in this case
[](#cb25-11)$ cd ./learnbyexample
[](#cb25-12)$ pwd
[](#cb25-13)/home/learnbyexample
[](#cb25-14)
[](#cb25-15)# go two hierarchies above
[](#cb25-16)$ cd ../..
[](#cb25-17)$ pwd
[](#cb25-18)/
```

You can switch to the home directory using `cd` or `cd ~` or `cd ~/` from anywhere in the filesystem. This is determined by the value stored in the `HOME` shell variable. See also [bash manual: Tilde Expansion](https://www.gnu.org/software/bash/manual/html_node/Tilde-Expansion.html).

```
[](#cb26-1)$ pwd
[](#cb26-2)/
[](#cb26-3)$ echo "$HOME"
[](#cb26-4)/home/learnbyexample
[](#cb26-5)
[](#cb26-6)$ cd
[](#cb26-7)$ pwd
[](#cb26-8)/home/learnbyexample
```

## clear

You can use this command to clear the terminal screen. By default, the `clear` command will move the prompt to the top of the terminal as well as try to remove the contents of the scrollback buffer. You can use the `-x` option if you want to retain the scrollback buffer contents.

> ![info](media/file2.svg) The `Ctrl+l` shortcut will also move the prompt line to the top of the terminal. It will retain any text you've typed on the prompt line and scrollback buffer contents won't be cleared.

## ls

When you use a file explorer GUI application, you'll automatically see the directory contents. And such GUI apps typically have features to show file size, differentiate between files and folders and so on. `ls` is the equivalent command line tool with a plethora of options and functionality related to viewing the contents of directories.

> ![info](media/file0.svg) As mentioned earlier, the [example_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files) directory has the scripts used in this chapter. You can source the `ls.sh` script to follow along the examples shown in this section. See [Setup](#ch002.xhtml_setup) section if you haven't yet created the working environment.
> 
> ```
> [](#cb27-1)# first, cd into the 'scripts' directory
> [](#cb27-2)$ cd cli-computing/example_files/scripts
> [](#cb27-3)
> [](#cb27-4)$ ls
> [](#cb27-5)cp.sh  file.sh  globs.sh  ls.sh  rm.sh    tar.sh
> [](#cb27-6)du.sh  find.sh  grep.sh   mv.sh  stat.sh  touch.sh
> [](#cb27-7)
> [](#cb27-8)# 'ls.sh' script will create a directory named 'ls_examples'
> [](#cb27-9)# and automatically change to that directory as well
> [](#cb27-10)$ source ls.sh
> [](#cb27-11)$ pwd
> [](#cb27-12)/home/learnbyexample/cli-computing/example_files/scripts/ls_examples
> ```

By default, the current directory contents are displayed. You can pass one or more paths as arguments. Here are some examples:

```
[](#cb28-1)$ ls
[](#cb28-2)backups     hello_world.py  ip.txt    report.log  todos
[](#cb28-3)errors.log  hi              projects  scripts
[](#cb28-4)
[](#cb28-5)# example with a single path argument
[](#cb28-6)$ ls /sys
[](#cb28-7)block  class  devices   fs          kernel  power
[](#cb28-8)bus    dev    firmware  hypervisor  module
[](#cb28-9)
[](#cb28-10)# multiple paths example
[](#cb28-11)# directory listings will be preceded by their names
[](#cb28-12)$ ls projects backups ip.txt
[](#cb28-13)ip.txt
[](#cb28-14)
[](#cb28-15)backups:
[](#cb28-16)bookmarks.html  dot_files
[](#cb28-17)
[](#cb28-18)projects:
[](#cb28-19)calculator  tictactoe
```

You can use the `-1` option (`1` as in numeric one, not the alphabet `l` which does something else) to list the contents in a single column:

```
[](#cb29-1)$ ls -1 backups
[](#cb29-2)bookmarks.html
[](#cb29-3)dot_files
```

The `-F` option appends a character to each filename indicating the file type (if it is other than a regular file):

*   `/` directory
*   `*` executable file
*   `@` symbolic link
*   `|` FIFO
*   `=` socket
*   `>` door

```
[](#cb30-1)$ ls -F
[](#cb30-2)backups/    hello_world.py*  ip.txt     report.log  todos/
[](#cb30-3)errors.log  hi*              projects/  scripts@
```

If you just need to distinguish between files and directories, you can use the `-p` option:

```
[](#cb31-1)$ ls -p
[](#cb31-2)backups/    hello_world.py  ip.txt     report.log  todos/
[](#cb31-3)errors.log  hi              projects/  scripts
```

You can also use the `--color` option to visually distinguish file types:

![example with --color option](media/file5.png)

The `-l` option displays the contents using a long listing format. You'll get details like file permissions, ownership, size, timestamp and so on. The first character of the first column distinguishes file types as `d` for directories, `-` for regular files, `l` for symbolic links, etc. Under each directory listing, the first line will display the total size of the entries (in terms of KB).

```
[](#cb32-1)$ ls -l hi
[](#cb32-2)-rwxrwxr-x 1 learnbyexample learnbyexample 21 Dec  5  2019 hi
[](#cb32-3)
[](#cb32-4)# you can add -G option to avoid the group column
[](#cb32-5)$ ls -lG
[](#cb32-6)total 7516
[](#cb32-7)drwxrwxr-x 3 learnbyexample    4096 Feb  4 09:23 backups
[](#cb32-8)-rw-rw-r-- 1 learnbyexample   12345 Jan  1 03:30 errors.log
[](#cb32-9)-rwxrwxr-x 1 learnbyexample      42 Feb 29  2020 hello_world.py
[](#cb32-10)-rwxrwxr-x 1 learnbyexample      21 Dec  5  2019 hi
[](#cb32-11)-rw-rw-r-- 1 learnbyexample      10 Jul 21  2017 ip.txt
[](#cb32-12)drwxrwxr-x 4 learnbyexample    4096 Mar  5 11:21 projects
[](#cb32-13)-rw-rw-r-- 1 learnbyexample 7654321 Jan  1 01:01 report.log
[](#cb32-14)lrwxrwxrwx 1 learnbyexample      13 May  7 15:17 scripts -> ../../scripts
[](#cb32-15)drwxrwxr-x 2 learnbyexample    4096 Apr  6 13:19 todos
```

> ![info](media/file0.svg) ![warning](media/file1.svg) Note that the timestamps showing hours and minutes instead of year depends on the relative difference with respect to the current time. So, for example, you might get `Feb 4 2022` instead of `Feb 4 09:23`.

Use the `-h` option to show file sizes in human readable format (default is byte count).

```
[](#cb33-1)$ ls -lG report.log
[](#cb33-2)-rw-rw-r-- 1 learnbyexample 7654321 Jan  1 01:01 report.log
[](#cb33-3)
[](#cb33-4)$ ls -lhG report.log
[](#cb33-5)-rw-rw-r-- 1 learnbyexample 7.3M Jan  1 01:01 report.log
```

You can use the `-s` option instead of long listing if you only need allocated file sizes and names:

```
[](#cb34-1)$ ls -1sh errors.log report.log
[](#cb34-2) 16K errors.log
[](#cb34-3)7.4M report.log
```

There are several options for changing the order of listing:

*   `-t` sorts by timestamp
*   `-S` sorts by file size (not suitable for directories)
*   `-v` version sorting (suitable for filenames with numbers in them)
*   `-X` sorts by file extension (i.e. characters after the last `.` in the filename)
*   `-r` reverse the listing order

```
[](#cb35-1)$ ls -lGhtr
[](#cb35-2)total 7.4M
[](#cb35-3)-rw-rw-r-- 1 learnbyexample   10 Jul 21  2017 ip.txt
[](#cb35-4)-rwxrwxr-x 1 learnbyexample   21 Dec  5  2019 hi
[](#cb35-5)-rwxrwxr-x 1 learnbyexample   42 Feb 29  2020 hello_world.py
[](#cb35-6)-rw-rw-r-- 1 learnbyexample 7.3M Jan  1 01:01 report.log
[](#cb35-7)-rw-rw-r-- 1 learnbyexample  13K Jan  1 03:30 errors.log
[](#cb35-8)drwxrwxr-x 3 learnbyexample 4.0K Feb  4 09:23 backups
[](#cb35-9)drwxrwxr-x 4 learnbyexample 4.0K Mar  5 11:21 projects
[](#cb35-10)drwxrwxr-x 2 learnbyexample 4.0K Apr  6 13:19 todos
[](#cb35-11)lrwxrwxrwx 1 learnbyexample   13 May  7 15:17 scripts -> ../../scripts
```

Filenames starting with `.` are considered as hidden files and these are NOT shown by default. You can use the `-a` option to view them. The `-A` option is similar, but doesn't show the special `.` and `..` entries.

```
[](#cb36-1)# . and .. point to the current and parent directories
[](#cb36-2)$ ls -aF backups/dot_files/
[](#cb36-3)./  ../  .bashrc  .inputrc  .vimrc
[](#cb36-4)
[](#cb36-5)# -A will exclude . and ..
[](#cb36-6)$ ls -A backups/dot_files/
[](#cb36-7).bashrc  .inputrc  .vimrc
```

The `-R` option recursively lists sub-directories as well:

```
[](#cb37-1)$ ls -ARF
[](#cb37-2).:
[](#cb37-3)backups/    hello_world.py*  .hidden  projects/   scripts@
[](#cb37-4)errors.log  hi*              ip.txt   report.log  todos/
[](#cb37-5)
[](#cb37-6)./backups:
[](#cb37-7)bookmarks.html  dot_files/
[](#cb37-8)
[](#cb37-9)./backups/dot_files:
[](#cb37-10).bashrc  .inputrc  .vimrc
[](#cb37-11)
[](#cb37-12)./projects:
[](#cb37-13)calculator/  tictactoe/
[](#cb37-14)
[](#cb37-15)./projects/calculator:
[](#cb37-16)calc.sh
[](#cb37-17)
[](#cb37-18)./projects/tictactoe:
[](#cb37-19)game.py
[](#cb37-20)
[](#cb37-21)./todos:
[](#cb37-22)books.txt  outing.txt
```

Often you'd want to list only specific files or directories based on some criteria, file extension for example. The shell provides a matching technique called **globs** or **wildcards**. Some simple examples are shown below (see [wildcards](#ch005.xhtml_wildcards) section for more details).

`*` is a placeholder for zero or more characters:

```
[](#cb38-1)# *.py *.log will give filenames ending with '.py' or '.log'
[](#cb38-2)$ echo *.py *.log
[](#cb38-3)hello_world.py errors.log report.log
[](#cb38-4)
[](#cb38-5)# glob expansion can be prevented by using quotes
[](#cb38-6)$ echo '*.py' *.log
[](#cb38-7)*.py errors.log report.log
[](#cb38-8)
[](#cb38-9)# long list only files ending with '.log'
[](#cb38-10)$ ls -lG *.log
[](#cb38-11)-rw-rw-r-- 1 learnbyexample   12345 Jan  1 03:30 errors.log
[](#cb38-12)-rw-rw-r-- 1 learnbyexample 7654321 Jan  1 01:01 report.log
```

`[]` helps you specify a set of characters to be matched once. For example, `[ad]` matches `a` or `d` once. `[c-i]` matches a range of characters from `c` to `i`.

```
[](#cb39-1)# entries starting with 'c' to 'i'
[](#cb39-2)$ echo [c-i]*
[](#cb39-3)errors.log hello_world.py hi ip.txt
[](#cb39-4)
[](#cb39-5)$ ls -1sh [c-i]*
[](#cb39-6) 16K errors.log
[](#cb39-7)4.0K hello_world.py
[](#cb39-8)4.0K hi
[](#cb39-9)4.0K ip.txt
```

> ![info](media/file2.svg) ![info](media/file2.svg) As shown in the above examples, globs are expanded by the shell. Beginners often associate globs as something specific to the `ls` command, which is why I've deliberately used `echo` as well in the above examples.

You can use the `-d` option to *not* show directory contents:

```
[](#cb40-1)$ echo b*
[](#cb40-2)backups
[](#cb40-3)# since backups is a directory, ls will show its contents
[](#cb40-4)$ ls b*
[](#cb40-5)bookmarks.html  dot_files
[](#cb40-6)# -d will show the directory entry instead of its contents
[](#cb40-7)$ ls -d b*
[](#cb40-8)backups
[](#cb40-9)
[](#cb40-10)# a handy way to get only the directory entries
[](#cb40-11)$ echo */
[](#cb40-12)backups/ projects/ scripts/ todos/
[](#cb40-13)$ ls -1d */
[](#cb40-14)backups/
[](#cb40-15)projects/
[](#cb40-16)scripts/
[](#cb40-17)todos/
```

> ![info](media/file0.svg) I hope you have been judiciously taking notes, since there are just too many commands and features. For example, note down all the options discussed in this section. And then explore the output from the `ls --help` command.

**Further Reading**

*   [mywiki.wooledge: avoid parsing output of ls](https://mywiki.wooledge.org/ParsingLs)
*   [unix.stackexchange: why not parse ls?](https://unix.stackexchange.com/q/128985/109046)
*   [unix.stackexchange: What are ./ and ../ directories?](https://unix.stackexchange.com/q/63081/109046)

## tree

The `tree` command displays the contents of a directory recursively, in a hierarchical manner. Here's a screenshot of using `tree -a` from the `ls_examples` sample directory seen in the previous section. The `-a` option is used to show the hidden files as well.

![example for tree command](media/file6.png)

> ![info](media/file0.svg) You might have to install this command. `sudo apt install tree` can be used to get this command on Debian-like distributions.

## mkdir

The `mkdir` command helps you to create new directories. You can pass one or more paths along with the name of the directories you want to create. Quote the names if it can contain shell special characters like space, `*` and so on.

> ![info](media/file0.svg) Create a practice directory for this section:
> 
> ```
> [](#cb41-1)$ mkdir practice_mkdir
> [](#cb41-2)$ cd practice_mkdir
> ```

Here's an example of creating multiple directories:

```
[](#cb42-1)$ mkdir reports 'low power adders'
[](#cb42-2)
[](#cb42-3)$ ls -1
[](#cb42-4)'low power adders'
[](#cb42-5)reports
```

The `-p` option will help you to create multiple directory hierarchies in one shot:

```
[](#cb43-1)# error because 'a' and 'a/b' paths do not exist yet
[](#cb43-2)$ mkdir a/b/c
[](#cb43-3)mkdir: cannot create directory ‘a/b/c’: No such file or directory
[](#cb43-4)
[](#cb43-5)# -p is handy in such cases
[](#cb43-6)$ mkdir -p a/b/c
[](#cb43-7)
[](#cb43-8)$ tree
[](#cb43-9).
[](#cb43-10)├── a
[](#cb43-11)│   └── b
[](#cb43-12)│       └── c
[](#cb43-13)├── low power adders
[](#cb43-14)└── reports
[](#cb43-15)
[](#cb43-16)5 directories, 0 files
```

The `-p` option has another functionality too. It will not complain if the directory you are trying to create already exists. This is especially helpful in shell scripts.

```
[](#cb44-1)# 'reports' directory was already created in an earlier example
[](#cb44-2)$ mkdir reports
[](#cb44-3)mkdir: cannot create directory ‘reports’: File exists
[](#cb44-4)# exit status will reflect that something went wrong
[](#cb44-5)$ echo $?
[](#cb44-6)1
[](#cb44-7)
[](#cb44-8)# the -p option will override such errors
[](#cb44-9)$ mkdir -p reports
[](#cb44-10)$ echo $?
[](#cb44-11)0
```

As seen in the examples above, you can check the exit status of the last executed command using the `$?` special variable. `0` means everything went well and higher numbers indicate some sort of failure has occurred (the details of which you can look up in the command's manual).

> ![info](media/file2.svg) ![warning](media/file7.svg) Linux filenames can use any character other than `/` and the ASCII NUL character. Quote the arguments if it contains characters like space, `*`, etc to prevent shell expansion. Shell considers space as the argument separator, `*` is a wildcard character and so on. As a good practice, use only alphabets, numbers and underscores for filenames, unless you have some specific requirements. See also [unix.stackexchange: Characters best avoided in filenames](https://unix.stackexchange.com/q/269093/109046).

> ![info](media/file0.svg) You can delete the practice directory if you wish:
> 
> ```
> [](#cb45-1)$ cd ..
> [](#cb45-2)$ rm -r practice_mkdir
> ```

## touch

You'll usually create files using a text editor or by redirecting the output of a command to a file. For some cases, empty files are needed for testing purposes or to satisfy a particular build process. A real world use case is the empty `.nojekyll` file for [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#static-site-generators).

The `touch` command's main functionality is altering timestamps (which will be discussed in the [File Properties](#ch008.xhtml_file-properties) chapter). If a file doesn't exist, `touch` will create an empty file using the current timestamp. You can also pass more than one file argument if needed.

```
[](#cb46-1)$ mkdir practice_touch
[](#cb46-2)$ cd practice_touch
[](#cb46-3)
[](#cb46-4)$ ls ip.txt
[](#cb46-5)ls: cannot access 'ip.txt': No such file or directory
[](#cb46-6)
[](#cb46-7)$ touch ip.txt
[](#cb46-8)
[](#cb46-9)$ ls -s ip.txt
[](#cb46-10)0 ip.txt
```

> ![info](media/file2.svg) You can create an empty file using `> ip.txt` as well, but the redirection operator will overwrite the file if it already exists.

## rm

The `rm` command will help you to delete files and directories. You can pass one or more paths as arguments.

```
[](#cb47-1)# change to the 'scripts' directory and source the 'rm.sh' script
[](#cb47-2)$ source rm.sh
[](#cb47-3)$ ls -F
[](#cb47-4)empty_dir/  hello.py  loops.py  projects/  read_only.txt  reports/
[](#cb47-5)
[](#cb47-6)# delete files ending with .py
[](#cb47-7)$ rm *.py
[](#cb47-8)$ ls -F
[](#cb47-9)empty_dir/  projects/  read_only.txt  reports/
```

You'll need to add the `-r` option to recursively delete directory contents. You can use `rm -d` or the `rmdir` command to delete only empty directories.

```
[](#cb48-1)# -r is needed to delete directory contents recursively
[](#cb48-2)$ rm reports
[](#cb48-3)rm: cannot remove 'reports': Is a directory
[](#cb48-4)$ rm -r reports
[](#cb48-5)$ ls -F
[](#cb48-6)empty_dir/  projects/  read_only.txt
[](#cb48-7)
[](#cb48-8)# delete empty directories, same as using the 'rmdir' command
[](#cb48-9)$ rm -d empty_dir
[](#cb48-10)# you'll get an error if the directory is not empty
[](#cb48-11)$ rm -d projects
[](#cb48-12)rm: cannot remove 'projects': Directory not empty
```

Typos like misplaced space, wrong glob, etc could wipe out files not intended for deletion. Apart from having backups and snapshots, you could also take some mitigating steps:

*   using `-i` option to interactively delete each file
    *   you can also use `-I` option for lesser number of prompts
*   using `echo` as a dry run to see how the glob expands
*   using a trash command (see links below) instead of `rm`

Use `y` for confirmation and `n` to cancel deletion with `-i` or `-I` options. Here's an example of cancelling deletion:

```
[](#cb49-1)$ rm -ri projects
[](#cb49-2)rm: descend into directory 'projects'? n
[](#cb49-3)
[](#cb49-4)$ ls -F
[](#cb49-5)projects/  read_only.txt
```

And here's an example of providing confirmation at each step of the deletion process:

```
[](#cb50-1)$ tree projects
[](#cb50-2)projects
[](#cb50-3)├── calculator
[](#cb50-4)│   └── calc.sh
[](#cb50-5)└── tictactoe
[](#cb50-6)    └── game.py
[](#cb50-7)
[](#cb50-8)2 directories, 2 files
[](#cb50-9)
[](#cb50-10)$ rm -ri projects
[](#cb50-11)rm: descend into directory 'projects'? y
[](#cb50-12)rm: descend into directory 'projects/tictactoe'? y
[](#cb50-13)rm: remove regular empty file 'projects/tictactoe/game.py'? y
[](#cb50-14)rm: remove directory 'projects/tictactoe'? y
[](#cb50-15)rm: descend into directory 'projects/calculator'? y
[](#cb50-16)rm: remove regular empty file 'projects/calculator/calc.sh'? y
[](#cb50-17)rm: remove directory 'projects/calculator'? y
[](#cb50-18)rm: remove directory 'projects'? y
[](#cb50-19)
[](#cb50-20)$ ls -F
[](#cb50-21)read_only.txt
```

The `-f` option can be used to ignore complaints about non-existing files (somewhat similar to the `mkdir -p` feature). It also helps to remove write protected files (provided you have appropriate permissions to delete those files). This option is especially useful for recursive deletion of directories that have write protected files, `.git/objects` for example.

```
[](#cb51-1)$ rm xyz.txt
[](#cb51-2)rm: cannot remove 'xyz.txt': No such file or directory
[](#cb51-3)$ echo $?
[](#cb51-4)1
[](#cb51-5)$ rm -f xyz.txt
[](#cb51-6)$ echo $?
[](#cb51-7)0
[](#cb51-8)
[](#cb51-9)# example for removing write protected files
[](#cb51-10)# you'll be asked for confirmation even without the -i/-I options
[](#cb51-11)$ rm read_only.txt
[](#cb51-12)rm: remove write-protected regular empty file 'read_only.txt'? n
[](#cb51-13)# with -f, files will be deleted without asking for confirmation
[](#cb51-14)$ rm -f read_only.txt
```

**Further Reading**

*   Use a trash command (for example, `trash-cli` on Ubuntu) so that deleted files can be recovered later if needed
    *   see also [unix.stackexchange: creating a simple trash command](https://unix.stackexchange.com/q/452496/109046)
*   Files removed using `rm` can still be recovered with time and skill
    *   [unix.stackexchange: recover deleted files](https://unix.stackexchange.com/q/80270/109046)
    *   [unix.stackexchange: recovering accidentally deleted files](https://unix.stackexchange.com/q/2677/109046)
*   Use commands like `shred` if you want to make it harder to recover deleted files
    *   [wiki.archlinux: Securely wipe disk](https://wiki.archlinux.org/title/Securely_wipe_disk)
*   [My curated list](https://learnbyexample.github.io/curated_resources/git_and_github.html) for `git` and related resources

## cp

You can use the `cp` command to make copies of files and directories. With default syntax, you have to specify the source first followed by the destination. To copy multiple items, the last argument as destination can only be a directory. You'll also need to use the `-r` option to copy directories (similar to `rm -r` seen earlier).

```
[](#cb52-1)# change to the 'scripts' directory and source the 'cp.sh' script
[](#cb52-2)$ source cp.sh
[](#cb52-3)$ ls -F
[](#cb52-4)backups/  reference/
[](#cb52-5)
[](#cb52-6)# recall that . is a relative path referring to the current directory
[](#cb52-7)$ cp /usr/share/dict/words .
[](#cb52-8)$ ls -F
[](#cb52-9)backups/  reference/  words
[](#cb52-10)
[](#cb52-11)# error because -r is needed to copy directories
[](#cb52-12)# other file arguments (if present) will still be copied
[](#cb52-13)$ cp /usr/share/dict .
[](#cb52-14)cp: -r not specified; omitting directory '/usr/share/dict'
[](#cb52-15)$ cp -r /usr/share/dict .
[](#cb52-16)$ ls -F
[](#cb52-17)backups/  dict/  reference/  words
```

> ![info](media/file2.svg) ![warning](media/file7.svg) By default, `cp` will overwrite an existing file of the same name in the destination directory. You can use the `-i` option to interactively confirm or deny overwriting existing files. The `-n` option will prevent overwriting existing files without asking for confirmation.

```
[](#cb53-1)$ echo 'hello' > ip.txt
[](#cb53-2)$ ls -F
[](#cb53-3)backups/  dict/  ip.txt  reference/  words
[](#cb53-4)$ ls backups
[](#cb53-5)ip.txt  reports
[](#cb53-6)$ cat backups/ip.txt
[](#cb53-7)apple banana cherry
[](#cb53-8)# file will be overwritten without asking for confirmation!
[](#cb53-9)$ cp ip.txt backups/
[](#cb53-10)$ cat backups/ip.txt
[](#cb53-11)hello
[](#cb53-12)
[](#cb53-13)# use -i to interactively confirm or deny overwriting
[](#cb53-14)$ echo 'good morning' > ip.txt
[](#cb53-15)$ cp -i ip.txt backups/
[](#cb53-16)cp: overwrite 'backups/ip.txt'? n
[](#cb53-17)$ cat backups/ip.txt
[](#cb53-18)hello
[](#cb53-19)
[](#cb53-20)# use -n to prevent overwriting without needing confirmation
[](#cb53-21)$ cp -n ip.txt backups/
[](#cb53-22)$ cat backups/ip.txt
[](#cb53-23)hello
```

If there's a folder in the destination path with the same name as a folder being copied, the contents will be merged. If there are files of identical names in such directories, the same rules discussed above will apply.

```
[](#cb54-1)$ tree backups
[](#cb54-2)backups
[](#cb54-3)├── ip.txt
[](#cb54-4)└── reports
[](#cb54-5)    └── jan.log
[](#cb54-6)
[](#cb54-7)1 directory, 2 files
[](#cb54-8)
[](#cb54-9)$ mkdir reports
[](#cb54-10)$ touch reports/dec.log
[](#cb54-11)$ cp -r reports backups/
[](#cb54-12)$ tree backups
[](#cb54-13)backups
[](#cb54-14)├── ip.txt
[](#cb54-15)└── reports
[](#cb54-16)    ├── dec.log
[](#cb54-17)    └── jan.log
[](#cb54-18)
[](#cb54-19)1 directory, 3 files
```

Often, you'd want to copy a file (or a directory) under a different name. In such cases, you can simply use a new name while specifying the destination.

```
[](#cb55-1)# copy 'words' file from source as 'words_ref.txt' at destination
[](#cb55-2)$ cp /usr/share/dict/words words_ref.txt
[](#cb55-3)
[](#cb55-4)# copy 'words' file as 'words.txt' under the 'reference' directory
[](#cb55-5)$ cp /usr/share/dict/words reference/words.txt
[](#cb55-6)
[](#cb55-7)# copy 'dict' directory as 'word_lists'
[](#cb55-8)$ cp -r /usr/share/dict word_lists
```

As mentioned earlier, to copy multiple files and directories, you'll have to specify the destination directory as the last argument.

```
[](#cb56-1)$ cp -r ~/.bashrc /usr/share/dict backups/
[](#cb56-2)
[](#cb56-3)$ ls -AF backups
[](#cb56-4).bashrc  dict/  ip.txt  reports/
```

You can use the `-t` option if you want to specify the destination before the source paths (helpful with `find` command for example, will be discussed later). Here are some more notable options:

*   `-u` copy files from source only if they are newer or don't exist in the destination
*   `-b` and `--backup` options will allow you to create backup copies of files already existing in the destination
*   `--preserve` option will help you to copy files along with source file attributes like ownership, timestamp, etc

**Further Reading**

*   `rsync` a fast, versatile, remote (and local) file-copying tool
    *   [rsync tutorial and examples](https://www.digitalocean.com/community/tutorials/how-to-use-rsync-to-sync-local-and-remote-directories-on-a-vps)
*   [syncthing](https://github.com/syncthing/syncthing) — continuous file synchronization program

## mv

You can use the `mv` command to move one or more files and directories from one location to another. Unlike `rm` and `cp`, you do not need the `-r` option for directories.

Syntax for specifying the source and destination is same as seen earlier with `cp`. Here's an example of moving a directory into another directory:

```
[](#cb57-1)# change to the 'scripts' directory and source the 'mv.sh' script
[](#cb57-2)$ source mv.sh
[](#cb57-3)$ ls -F
[](#cb57-4)backups/  dot_files/  hello.py  ip.txt  loops.py  manuals/
[](#cb57-5)$ ls -F backups
[](#cb57-6)projects/
[](#cb57-7)
[](#cb57-8)$ mv dot_files backups
[](#cb57-9)
[](#cb57-10)$ ls -F
[](#cb57-11)backups/  hello.py  ip.txt  loops.py  manuals/
[](#cb57-12)$ ls -F backups
[](#cb57-13)dot_files/  projects/
```

Here's an example for moving multiple files and directories to another directory:

```
[](#cb58-1)$ mv *.py manuals backups
[](#cb58-2)
[](#cb58-3)$ ls -F
[](#cb58-4)backups/  ip.txt
[](#cb58-5)$ ls -F backups
[](#cb58-6)dot_files/  hello.py  loops.py  manuals/  projects/
```

When you are dealing with a single file or directory, you can also *rename* them:

```
[](#cb59-1)# within the same directory
[](#cb59-2)$ mv ip.txt report.txt
[](#cb59-3)$ ls -F
[](#cb59-4)backups/  report.txt
[](#cb59-5)
[](#cb59-6)# between different directories
[](#cb59-7)$ mv backups/dot_files rc_files
[](#cb59-8)$ ls -F
[](#cb59-9)backups/  rc_files/  report.txt
[](#cb59-10)$ ls -F backups
[](#cb59-11)hello.py  loops.py  manuals/  projects/
```

Here are some more notable options, some of which behave similar to those seen with the `cp` command:

*   `-i` interactively confirm or deny when the destination already has a file of the same name
*   `-n` always deny overwriting of files
*   `-f` always overwrite files
*   `-t` specify the destination elsewhere instead of final argument
*   `-u` move only if the files are newer or don't exist in the destination
*   `-b` and `--backup` options will allow you to create backup copies of files already existing in the destination
*   `-v` verbose option

## rename

The `mv` command is useful for simple file renaming. `rename` helps when you need to modify one or more filenames based on a pattern. There are different implementations of the `rename` command, with wildly different set of features. See [askubuntu: What's the difference between the different "rename" commands?](https://askubuntu.com/questions/956010/whats-the-difference-between-the-different-rename-commands) for details.

Perl implementation of the `rename` command will be discussed in this section. You'd need to know regular expressions to use this command. Basic explanations will be given here, more details can be found in the links mentioned at the end of this section. Here's an example to change the file extensions:

```
[](#cb60-1)$ mkdir practice_rename
[](#cb60-2)$ cd practice_rename
[](#cb60-3)# create sample files
[](#cb60-4)$ touch caves.jpeg waterfall.JPEG flower.JPG
[](#cb60-5)
[](#cb60-6)# substitution command syntax is s/search/replace/flags
[](#cb60-7)# \. matches . character literally
[](#cb60-8)# e? matches e optionally (? is a quantifier to match 0 or 1 times)
[](#cb60-9)# $ anchors the match to the end of the input
[](#cb60-10)# i flag matches the input case-insensitively
[](#cb60-11)$ rename 's/\.jpe?g$/.jpg/i' *
[](#cb60-12)
[](#cb60-13)$ ls
[](#cb60-14)caves.jpg  flower.jpg  waterfall.jpg
[](#cb60-15)$ rm *.jpg
```

As a good practice, use the `-n` option to see how the files will be renamed before actually renaming the files.

```
[](#cb61-1)$ touch 1.png 3.png 25.png 100.png
[](#cb61-2)$ ls
[](#cb61-3)100.png  1.png  25.png  3.png
[](#cb61-4)
[](#cb61-5)# use -n option for sanity check
[](#cb61-6)# note that 100.png isn't part of the output, since it isn't affected
[](#cb61-7)# \d matches a digit character
[](#cb61-8)# \d+ matches 1 or more digits (+ is a quantifier to match 1 or more times)
[](#cb61-9)# e flag treats the replacement string as Perl code
[](#cb61-10)# $& is a backreference to the matched portion
[](#cb61-11)$ rename -n 's/\d+/sprintf "%03d", $&/e' *.png
[](#cb61-12)rename(1.png, 001.png)
[](#cb61-13)rename(25.png, 025.png)
[](#cb61-14)rename(3.png, 003.png)
[](#cb61-15)
[](#cb61-16)# remove -n option after sanity check to actually rename the files
[](#cb61-17)$ rename 's/\d+/sprintf "%03d", $&/e' *.png
[](#cb61-18)$ ls
[](#cb61-19)001.png  003.png  025.png  100.png
```

If the new filename already exists, you'll get an error, which you can override with `-f` option if you wish. If you are passing filenames with path components in them, you can use the `-d` option to affect only the filename portion. Otherwise, the logic you are using might affect directory names as well.

```
[](#cb62-1)$ mkdir projects
[](#cb62-2)$ touch projects/toc.sh projects/reports.py
[](#cb62-3)
[](#cb62-4)# aim is to uppercase the non-extension part of the filename
[](#cb62-5)# [^.]+ matches 1 or more non '.' characters
[](#cb62-6)# \U changes the characters that follow to uppercase
[](#cb62-7)# $& is a backreference to the matched portion
[](#cb62-8)$ rename -n -d 's/[^.]+/\U$&/' projects/*
[](#cb62-9)rename(projects/reports.py, projects/REPORTS.py)
[](#cb62-10)rename(projects/toc.sh, projects/TOC.sh)
[](#cb62-11)
[](#cb62-12)# without -d option, directory name will also be affected
[](#cb62-13)$ rename -n 's/[^.]+/\U$&/' projects/*
[](#cb62-14)rename(projects/reports.py, PROJECTS/REPORTS.py)
[](#cb62-15)rename(projects/toc.sh, PROJECTS/TOC.sh)
```

**Further Reading**

*   [perldoc: Regexp tutorial](https://perldoc.perl.org/perlretut)
*   See my [Perl one-liners](https://github.com/learnbyexample/learn_perl_oneliners) ebook for examples and more details about the Perl substitution and `rename` commands

## ln

The `ln` command helps you create a link to another file or directory within the same or different location. There are two types of links — **symbolic** links and **hard** links. Symbolic links can point to both files and directories. Here are some characteristics:

*   if the original file is deleted or moved to another location, symbolic link will no longer work
*   if the symbolic link is moved to another location, it will still work if the link was done using absolute path (for relative path, it will depend on whether or not there's another file with the same name in that location)
*   a symbolic link file has its own inode, permissions, timestamps, etc
*   some commands will work the same when original file or the symbolic file is given as the command line argument, while some require additional options (`du -L` for example)

Usage is similar to the `cp` command. You have to specify the source first followed by the destination (which is optional if it is the current working directory).

```
[](#cb63-1)$ mkdir practice_ln
[](#cb63-2)$ cd practice_ln
[](#cb63-3)
[](#cb63-4)# destination is optional for making a link in the current directory
[](#cb63-5)# -s option is needed to make symbolic links
[](#cb63-6)$ ln -s /usr/share/dict/words
[](#cb63-7)
[](#cb63-8)# you can also rename the link if needed
[](#cb63-9)$ ln -s /usr/share/dict/words words.txt
[](#cb63-10)$ ls -1sF
[](#cb63-11)total 0
[](#cb63-12)0 words@
[](#cb63-13)0 words.txt@
```

Long listing with `ls -l` will show the path connected to links. You can also use the `readlink` command, which has features like resolving recursively to the canonical file.

```
[](#cb64-1)# to know which file the link points to
[](#cb64-2)$ ls -lG words
[](#cb64-3)lrwxrwxrwx 1 learnbyexample 21 Jul  9 13:41 words -> /usr/share/dict/words
[](#cb64-4)$ readlink words
[](#cb64-5)/usr/share/dict/words
[](#cb64-6)
[](#cb64-7)# the linked file may be another link
[](#cb64-8)# use -f option to get the original file
[](#cb64-9)$ readlink -f words
[](#cb64-10)/usr/share/dict/english
```

Hard links can only point to another file. You cannot use them for directories and the usage is also restricted to within the same filesystem. The `.` and `..` directories are exceptions, these special purpose hard links are automatically created. Here are some more details about hard links:

*   once a hard link is created, there is no distinction between the two files other than their paths. They have same inode, permissions, timestamps, etc
*   hard links will continue working even if all the other hard links are deleted
*   if a hard link is moved to another location, the links will still be in sync. Any change in one of them will be reflected in all the other links

```
[](#cb65-1)$ touch apple.txt
[](#cb65-2)$ ln apple.txt banana.txt
[](#cb65-3)
[](#cb65-4)# the -i option gives inode
[](#cb65-5)$ ls -1i apple.txt banana.txt
[](#cb65-6)649140 banana.txt
[](#cb65-7)649140 apple.txt
```

> ![info](media/file2.svg) You can use `unlink` or `rm` commands to delete links.

**Further Reading**

*   [askubuntu: What is the difference between a hard link and a symbolic link?](https://askubuntu.com/questions/108771/what-is-the-difference-between-a-hard-link-and-a-symbolic-link)
*   [unix.stackexchange: What is the difference between symbolic and hard links?](https://unix.stackexchange.com/q/9575/109046)
*   [unix.stackexchange: What is a Superblock, Inode, Dentry and a File?](https://unix.stackexchange.com/q/4402/109046)

## tar and gzip

`tar` is an archiving utility. Depending on the implementation, you can also use options to compress the archive.

Here's an example that creates a single archive file from multiple input files and directories:

```
[](#cb66-1)# change to the 'scripts' directory and source the 'tar.sh' script
[](#cb66-2)$ source tar.sh
[](#cb66-3)$ ls -F
[](#cb66-4)projects/  report.log  todos/
[](#cb66-5)
[](#cb66-6)# -c option creates a new archive, any existing archive will be overwritten
[](#cb66-7)# -f option allows to specify name of archive to be created
[](#cb66-8)# rest of the arguments are the files/directories to be archived
[](#cb66-9)$ tar -cf bkp.tar report.log projects
[](#cb66-10)
[](#cb66-11)$ ls -F
[](#cb66-12)bkp.tar  projects/  report.log  todos/
[](#cb66-13)$ ls -sh bkp.tar
[](#cb66-14)7.4M bkp.tar
```

Once you have an archive file, you can then compress it using tools like `gzip`, `bzip2`, `xz`, etc. In the below example, the command replaces the archive file with the compressed version and adds a `.gz` suffix to indicate that `gzip` was the technique used.

```
[](#cb67-1)# the input '.tar' file will be overwritten with the compressed version
[](#cb67-2)$ gzip bkp.tar
[](#cb67-3)
[](#cb67-4)$ ls -F
[](#cb67-5)bkp.tar.gz  projects/  report.log  todos/
[](#cb67-6)$ ls -sh bkp.tar.gz
[](#cb67-7)5.6M bkp.tar.gz
```

Use the `-t` option if you want to check the contents of the compressed file. This will work with the uncompressed `.tar` version as well.

```
[](#cb68-1)$ tar -tf bkp.tar.gz 
[](#cb68-2)report.log
[](#cb68-3)projects/
[](#cb68-4)projects/scripts/
[](#cb68-5)projects/scripts/calc.sh
[](#cb68-6)projects/errors.log
```

To uncompress `.gz` files, you can use `gunzip` or `gzip -d`. This will replace the compressed version with the uncompressed archive file:

```
[](#cb69-1)# this '.gz' file will be overwritten with the uncompressed version
[](#cb69-2)$ gunzip bkp.tar.gz
[](#cb69-3)
[](#cb69-4)$ ls -F
[](#cb69-5)bkp.tar  projects/  report.log  todos/
[](#cb69-6)$ ls -sh bkp.tar
[](#cb69-7)7.4M bkp.tar
```

To extract the files from an archive, use `tar` along with the `-x` option:

```
[](#cb70-1)$ mkdir test_extract
[](#cb70-2)$ mv bkp.tar test_extract
[](#cb70-3)$ cd test_extract
[](#cb70-4)$ ls
[](#cb70-5)bkp.tar
[](#cb70-6)
[](#cb70-7)$ tar -xf bkp.tar
[](#cb70-8)$ tree
[](#cb70-9).
[](#cb70-10)├── bkp.tar
[](#cb70-11)├── projects
[](#cb70-12)│   ├── errors.log
[](#cb70-13)│   └── scripts
[](#cb70-14)│       └── calc.sh
[](#cb70-15)└── report.log
[](#cb70-16)
[](#cb70-17)2 directories, 4 files
[](#cb70-18)
[](#cb70-19)$ cd ..
[](#cb70-20)$ rm -r test_extract
```

With `GNU tar`, you can compress/uncompress along with the `tar` command instead of having to use tools like `gzip` separately. For example, the `-z` option will use `gzip`, `-j` will use `bzip2` and `-J` will use `xz`. Use the `-a` option if you want `tar` to automatically select the compression technique based on the extension provided.

```
[](#cb71-1)$ ls -F
[](#cb71-2)projects/  report.log  todos/
[](#cb71-3)
[](#cb71-4)# -z option gives same compression as the gzip command
[](#cb71-5)$ tar -zcf bkp.tar.gz report.log projects
[](#cb71-6)$ ls -sh bkp.tar.gz
[](#cb71-7)5.6M bkp.tar.gz
[](#cb71-8)
[](#cb71-9)# extract original files from compressed file
[](#cb71-10)$ mkdir test_extract
[](#cb71-11)$ cd test_extract
[](#cb71-12)$ tar -zxf ../bkp.tar.gz
[](#cb71-13)$ tree
[](#cb71-14).
[](#cb71-15)├── projects
[](#cb71-16)│   ├── errors.log
[](#cb71-17)│   └── scripts
[](#cb71-18)│       └── calc.sh
[](#cb71-19)└── report.log
[](#cb71-20)
[](#cb71-21)2 directories, 3 files
[](#cb71-22)
[](#cb71-23)$ cd ..
[](#cb71-24)$ rm -r test_extract
```

`tar` has lots and lots of options for various needs. Some are listed below, see documentation for complete details.

*   `-v` verbose option
*   `-r` to append files to an existing archive
*   `--exclude=` specify files to be ignored from archiving

There are also commands starting with `z` to work with compressed files, for example:

*   `zcat` to display file contents of a compressed file
*   `zless` to display file contents of a compressed file one screenful at a time
*   `zgrep` to search compressed files

> ![info](media/file2.svg) If you need to work with `.zip` files, use `zip` and `unzip` commands.

**Further Reading**

*   [unix.stackexchange: tar files with a sorted order](https://unix.stackexchange.com/q/178127/109046)
*   [superuser: gzip without tar? Why are they used together?](https://superuser.com/questions/252065/gzip-without-tar-why-are-they-used-together)
*   [unix.stackexchange: xz a directory with tar using maximum compression?](https://unix.stackexchange.com/q/28976/109046)

## Exercises

> ![info](media/file0.svg) The `ls.sh` script will be used for some of the exercises.

**1)** Which of these commands will always display the absolute path of the home directory?

*a)* `pwd`
*b)* `echo "$PWD"`
*c)* `echo "$HOME"`

**2)** The current working directory has a folder named `-dash`. How would you switch to that directory?

*a)* `cd -- -dash`
*b)* `cd -dash`
*c)* `cd ./-dash`
*d)* `cd \-dash`
*e)* `cd '-dash'`
*f)* all of the above
*g)* only *a)* and *c)*

**3)** Given the directory structure as shown below, how would you change to the `todos` directory?

```
[](#cb72-1)# change to the 'scripts' directory and source the 'ls.sh' script
[](#cb72-2)$ source ls.sh
[](#cb72-3)
[](#cb72-4)$ ls -F
[](#cb72-5)backups/    hello_world.py*  ip.txt     report.log  todos/
[](#cb72-6)errors.log  hi*              projects/  scripts@
[](#cb72-7)$ cd projects
[](#cb72-8)$ pwd
[](#cb72-9)/home/learnbyexample/cli-computing/example_files/scripts/ls_examples/projects
[](#cb72-10)
[](#cb72-11)# ???
[](#cb72-12)$ pwd
[](#cb72-13)/home/learnbyexample/cli-computing/example_files/scripts/ls_examples/todos
```

**4)** As per the scenario shown below, how would you change to the `cli-computing` directory under the user's home directory? And then, how would you go back to the previous working directory?

```
[](#cb73-1)$ pwd
[](#cb73-2)/home/learnbyexample/all/projects/square_tictactoe
[](#cb73-3)
[](#cb73-4)# ???
[](#cb73-5)$ pwd
[](#cb73-6)/home/learnbyexample/cli-computing
[](#cb73-7)
[](#cb73-8)# ???
[](#cb73-9)$ pwd
[](#cb73-10)/home/learnbyexample/all/projects/square_tictactoe
```

**5)** How'd you list the contents of the current directory, one per line, along with the size of the entries in human readable format?

```
[](#cb74-1)# change to the 'scripts' directory and source the 'ls.sh' script
[](#cb74-2)$ source ls.sh
[](#cb74-3)
[](#cb74-4)# ???
[](#cb74-5)total 7.4M
[](#cb74-6)4.0K backups
[](#cb74-7) 16K errors.log
[](#cb74-8)4.0K hello_world.py
[](#cb74-9)4.0K hi
[](#cb74-10)4.0K ip.txt
[](#cb74-11)4.0K projects
[](#cb74-12)7.4M report.log
[](#cb74-13)   0 scripts
[](#cb74-14)4.0K todos
```

**6)** Which `ls` command option would you use for version based sorting of entries?

**7)** Which `ls` command option would you use for sorting based on entry size?

**8)** Which `ls` command option would you use for sorting based on file extension?

**9)** What does the `-G` option of `ls` command do?

**10)** What does the `-i` option of `ls` command do?

**11)** List only the directories as one entry per line.

```
[](#cb75-1)# change to the 'scripts' directory and source the 'ls.sh' script
[](#cb75-2)$ source ls.sh
[](#cb75-3)
[](#cb75-4)# ???
[](#cb75-5)backups/
[](#cb75-6)projects/
[](#cb75-7)scripts/
[](#cb75-8)todos/
```

**12)** Assume that a regular file named `notes` already exists. What would happen if you use the `mkdir -p notes` command?

```
[](#cb76-1)$ ls -1F notes
[](#cb76-2)notes
[](#cb76-3)
[](#cb76-4)# what would happen here?
[](#cb76-5)$ mkdir -p notes
```

**13)** Use one or more commands to match the scenario shown below:

```
[](#cb77-1)$ ls -1F
[](#cb77-2)cost.txt
[](#cb77-3)
[](#cb77-4)# ???
[](#cb77-5)
[](#cb77-6)$ ls -1F
[](#cb77-7)cost.txt
[](#cb77-8)ghost/
[](#cb77-9)quest/
[](#cb77-10)toast/
```

**14)** Use one or more commands to match the scenario shown below:

```
[](#cb78-1)# start with an empty directory
[](#cb78-2)$ ls -l
[](#cb78-3)total 0
[](#cb78-4)
[](#cb78-5)# ???
[](#cb78-6)
[](#cb78-7)$ tree -F
[](#cb78-8).
[](#cb78-9)├── hobbies/
[](#cb78-10)│   ├── painting/
[](#cb78-11)│   │   └── waterfall.bmp
[](#cb78-12)│   ├── trekking/
[](#cb78-13)│   │   └── himalayas.txt
[](#cb78-14)│   └── writing/
[](#cb78-15)└── shopping/
[](#cb78-16)    └── festival.xlsx
[](#cb78-17)
[](#cb78-18)5 directories, 3 files
```

> ![info](media/file0.svg) Don't delete this directory, will be needed in a later exercise.

**15)** If directories to create already exist, which `mkdir` command option would you use to not show an error?

**16)** Use one or more commands to match the scenario given below:

```
[](#cb79-1)$ ls -1F
[](#cb79-2)cost.txt
[](#cb79-3)ghost/
[](#cb79-4)quest/
[](#cb79-5)toast/
[](#cb79-6)
[](#cb79-7)# ???
[](#cb79-8)
[](#cb79-9)$ ls -1F
[](#cb79-10)quest/
```

**17)** What does the `-f` option of `rm` command do?

**18)** Which option would you use to interactively delete files using the `rm` command?

**19)** Can the files removed by `rm` easily be restored? Do you need to take some extra steps or use special commands to make the files more difficult to recover?

**20)** Does your Linux distribution provide a tool to send deleted files to the trash (which would help to recover deleted files)?

**21)** Which option would you use to interactively accept/prevent the `cp` command from overwriting a file of the same name? And which option would prevent overwriting without needing manual confirmation?

**22)** Does the `cp` command allow you to rename the file or directory being copied? If so, can you rename multiple files/directories being copied?

**23)** What do the `-u`, `-b` and `-t` options of `cp` command do?

**24)** What's the difference between the two commands shown below?

```
[](#cb80-1)$ cp ip.txt op.txt
[](#cb80-2)
[](#cb80-3)$ mv ip.txt op.txt
```

**25)** Which option would you use to interactively accept/prevent the `mv` command from overwriting a file of the same name?

**26)** Use one or more commands to match the scenario shown below. You should have already created this directory structure in an earlier exercise.

```
[](#cb81-1)$ tree -F
[](#cb81-2).
[](#cb81-3)├── hobbies/
[](#cb81-4)│   ├── painting/
[](#cb81-5)│   │   └── waterfall.bmp
[](#cb81-6)│   ├── trekking/
[](#cb81-7)│   │   └── himalayas.txt
[](#cb81-8)│   └── writing/
[](#cb81-9)└── shopping/
[](#cb81-10)    └── festival.xlsx
[](#cb81-11)
[](#cb81-12)5 directories, 3 files
[](#cb81-13)
[](#cb81-14)# ???
[](#cb81-15)
[](#cb81-16)$ tree -F
[](#cb81-17).
[](#cb81-18)├── hobbies/
[](#cb81-19)│   ├── himalayas.txt
[](#cb81-20)│   └── waterfall.bmp
[](#cb81-21)└── shopping/
[](#cb81-22)    └── festival.xlsx
[](#cb81-23)
[](#cb81-24)2 directories, 3 files
```

**27)** What does the `-t` option of `mv` command do?

**28)** Determine and implement the `rename` logic based on the filenames and expected output shown below.

```
[](#cb82-1)$ touch '(2020) report part 1.txt' 'analysis part 3 (2018).log'
[](#cb82-2)$ ls -1
[](#cb82-3)'(2020) report part 1.txt'
[](#cb82-4)'analysis part 3 (2018).log'
[](#cb82-5)
[](#cb82-6)# ???
[](#cb82-7)
[](#cb82-8)$ ls -1
[](#cb82-9)2020_report_part_1.txt
[](#cb82-10)analysis_part_3_2018.log
```

**29)** Does the `ln` command follow the same order to specify source and destination as the `cp` and `mv` commands?

**30)** Which `tar` option helps to compress archives based on filename extension? This option can be used instead of `-z` for `gzip`, `-j` for `bzip2` and `-J` for `xz`.

# Shell Features

This chapter focuses on Bash shell features like quoting mechanisms, wildcards, redirections, command grouping, process substitution, command substitution, etc. Others will be discussed in later chapters.

> ![info](media/file0.svg) The [example_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files) directory has the scripts and sample input files used in this chapter.

> ![info](media/file0.svg) Some of the examples in this chapter use commands that will be discussed in later chapters. Basic description of what such commands do have been added here and you'll also see more examples in the rest of the chapters.

## Quoting mechanisms

This section will quote (*heh*) the relevant definitions from the [bash manual](https://www.gnu.org/software/bash/manual/bash.html#Quoting) and provide some examples for each of the four mechanisms.

*1)* **Escape Character**

> A non-quoted backslash `\` is the Bash escape character. It preserves the literal value of the next character that follows, with the exception of newline.
> 
> **metacharacter**: A character that, when unquoted, separates words. A metacharacter is a space, tab, newline, or one of the following characters: `|`, `&`, `;`, `(`, `)`, `<`, or `>`.

Here's an example where unquoted shell metacharacter causes an error:

```
[](#cb83-1)$ echo apple;cherry
[](#cb83-2)apple
[](#cb83-3)cherry: command not found
[](#cb83-4)
[](#cb83-5)# using '\;' helps you use ';' as an ordinary character
[](#cb83-6)$ echo apple\;cherry
[](#cb83-7)apple;cherry
```

And here's an example where the subtler issue might not be apparent at first glance:

```
[](#cb84-1)# this will create two files named 'new' and 'file.txt'
[](#cb84-2)# aim was to create a single file named 'new file.txt'
[](#cb84-3)$ touch new file.txt
[](#cb84-4)$ ls new*txt
[](#cb84-5)ls: cannot access 'new*txt': No such file or directory
[](#cb84-6)$ rm file.txt new
[](#cb84-7)
[](#cb84-8)# escaping the space will create a single file named 'new file.txt'
[](#cb84-9)$ touch new\ file.txt
[](#cb84-10)$ ls new*txt
[](#cb84-11)'new file.txt'
[](#cb84-12)$ rm new\ file.txt
```

*2)* **Single Quotes**

> Enclosing characters in single quotes (`'`) preserves the literal value of each character within the quotes. A single quote may not occur between single quotes, even when preceded by a backslash.

No character is special within single quoted strings. Here's an example:

```
[](#cb85-1)$ echo 'apple;cherry'
[](#cb85-2)apple;cherry
```

You can place strings represented by different quoting mechanisms next to each other to concatenate them together. Here's an example:

```
[](#cb86-1)# concatenation of four strings
[](#cb86-2)# 1: '@fruits = '
[](#cb86-3)# 2: \'
[](#cb86-4)# 3: 'apple and banana'
[](#cb86-5)# 4: \'
[](#cb86-6)$ echo '@fruits = '\''apple and banana'\'
[](#cb86-7)@fruits = 'apple and banana'
```

*3)* **Double Quotes**

> Enclosing characters in double quotes (`"`) preserves the literal value of all characters within the quotes, with the exception of `$`, `` ` ``, `\`, and, when history expansion is enabled, `!`.

Here's an example showing variable interpolation within double quotes:

```
[](#cb87-1)$ qty='5'
[](#cb87-2)
[](#cb87-3)# as seen earlier, no character is special within single quotes
[](#cb87-4)$ echo 'I bought $qty apples'
[](#cb87-5)I bought $qty apples
[](#cb87-6)
[](#cb87-7)# a typical use of double quotes is to enable variable interpolation
[](#cb87-8)$ echo "I bought $qty apples"
[](#cb87-9)I bought 5 apples
```

Unless you specifically want the shell to interpret the contents of a variable, you should always quote the variable to avoid issues due to the presence of shell metacharacters.

```
[](#cb88-1)$ f='new file.txt'
[](#cb88-2)
[](#cb88-3)# same as: echo 'apple banana' > new file.txt
[](#cb88-4)$ echo 'apple banana' > $f
[](#cb88-5)bash: $f: ambiguous redirect
[](#cb88-6)
[](#cb88-7)# same as: echo 'apple banana' > 'new file.txt'
[](#cb88-8)$ echo 'apple banana' > "$f"
[](#cb88-9)$ cat "$f"
[](#cb88-10)apple banana
[](#cb88-11)$ rm "$f"
```

> ![info](media/file0.svg) See also [unix.stackexchange: Why does my shell script choke on whitespace or other special characters?](https://unix.stackexchange.com/q/131766/109046).

*4)* **ANSI-C Quoting**

> Words of the form `$'string'` are treated specially. The word expands to string, with backslash-escaped characters replaced as specified by the ANSI C standard.

This form of quoting helps you use escape sequences like `\t` for tab, `\n` for newline and so on. You can also represent characters using their codepoint values in octal and hexadecimal formats.

```
[](#cb89-1)# can also use echo -e 'fig:\t42' or printf 'fig:\t42\n'
[](#cb89-2)$ echo $'fig:\t42'
[](#cb89-3)fig:    42
[](#cb89-4)
[](#cb89-5)# \x27 represents single quote character in hexadecimal format
[](#cb89-6)$ echo $'@fruits = \x27apple and banana\x27'
[](#cb89-7)@fruits = 'apple and banana'
[](#cb89-8)
[](#cb89-9)# 'grep' helps you to filter lines based on the given pattern
[](#cb89-10)# but it doesn't recognize escapes like '\t' for tab characters
[](#cb89-11)$ printf 'fig\t42\napple 100\nball\t20\n' | grep '\t'
[](#cb89-12)# in such cases, one workaround is use to ANSI-C quoting
[](#cb89-13)$ printf 'fig\t42\napple 100\nball\t20\n' | grep $'\t'
[](#cb89-14)fig     42
[](#cb89-15)ball    20
```

`printf` is a shell builtin which you can use to format arguments (similar to `C` programming language `printf()` function). This command will be used in many more examples to come.

> ![info](media/file0.svg) See [bash manual: ANSI-C Quoting](https://www.gnu.org/software/bash/manual/bash.html#ANSI_002dC-Quoting) for complete list of supported escape sequences. See `man ascii` for a table of ASCII characters and their numerical representations.

## Wildcards

It is relatively easy to specify complete filenames as command arguments when they are few in number. And you could use features like tab completion and middle mouse button click (which pastes the last highlighted text) to assist in such cases.

But what to do if you have to deal with tens and hundreds of files (or even more)? If applicable, one way is to match all the files based on a common pattern in their filenames, for example extensions like `.py`, `.txt` and so on. Wildcards (globs) will help in such cases. This feature is provided by the shell, and thus individual commands need not worry about implementing them. Pattern matching supported by wildcards are somewhat similar to regular expressions, but there are fundamental and syntactical differences between them.

Some of the commonly used wildcards are listed below:

*   `*` match any character, zero or more times
    *   as a special case, `*` won't match the starting `.` of hidden files unless the `dotglob` shell option is set
*   `?` match any character exactly once
*   `[set149]` match any of these characters once
*   `[^set149]` match any characters *except* the given set of characters
    *   you can also use `[!set149]` to negate the character class
*   `[a-z]` match a range of characters from `a` to `z`
*   `[0-9a-fA-F]` match any hexadecimal character

And here are some examples:

```
[](#cb90-1)# change to the 'scripts' directory and source the 'globs.sh' script
[](#cb90-2)$ source globs.sh
[](#cb90-3)$ ls
[](#cb90-4)100.sh   f1.txt      f4.txt    hi.sh   math.h         report-02.log
[](#cb90-5)42.txt   f2_old.txt  f7.txt    ip.txt  notes.txt      report-04.log
[](#cb90-6)calc.py  f2.txt      hello.py  main.c  report-00.log  report-98.log
[](#cb90-7)
[](#cb90-8)# beginning with 'c' or 'h' or 't'
[](#cb90-9)$ ls [cht]*
[](#cb90-10)calc.py  hello.py  hi.sh
[](#cb90-11)
[](#cb90-12)# only hidden files and directories
[](#cb90-13)$ ls -d .*
[](#cb90-14).  ..  .hidden  .somerc
[](#cb90-15)
[](#cb90-16)# ending with '.c' or '.py'
[](#cb90-17)$ ls *.c *.py
[](#cb90-18)calc.py  hello.py  main.c
[](#cb90-19)
[](#cb90-20)# containing 'o' as well as 'x' or 'y' or 'z' afterwards
[](#cb90-21)$ ls *o*[xyz]*
[](#cb90-22)f2_old.txt  hello.py  notes.txt
[](#cb90-23)
[](#cb90-24)# ending with '.' and two more characters
[](#cb90-25)$ ls *.??
[](#cb90-26)100.sh  calc.py  hello.py  hi.sh
[](#cb90-27)
[](#cb90-28)# shouldn't start with 'f' and ends with '.txt'
[](#cb90-29)$ ls [^f]*.txt
[](#cb90-30)42.txt  ip.txt  notes.txt
[](#cb90-31)
[](#cb90-32)# containing digits '1' to '5' and ending with 'log'
[](#cb90-33)$ ls *[1-5]*log
[](#cb90-34)report-02.log  report-04.log
```

Since some characters are special inside the character class, you need special placement to treat them as ordinary characters:

*   `-` should be the first or the last character in the set
*   `^` should be other than the first character
*   `]` should be the first character

```
[](#cb91-1)$ ls *[ns-]*
[](#cb91-2)100.sh  main.c     report-00.log  report-04.log
[](#cb91-3)hi.sh   notes.txt  report-02.log  report-98.log
[](#cb91-4)
[](#cb91-5)$ touch 'a^b' 'mars[planet].txt'
[](#cb91-6)$ rm -i *[]^]*
[](#cb91-7)rm: remove regular empty file 'a^b'? y
[](#cb91-8)rm: remove regular empty file 'mars[planet].txt'? y
```

A **named character set** is defined by a name enclosed between `[:` and `:]` and has to be used within a character class `[]`, along with any other characters as needed.

| Named set | Description |
| --- | --- |
| `[:digit:]` | `[0-9]` |
| `[:lower:]` | `[a-z]` |
| `[:upper:]` | `[A-Z]` |
| `[:alpha:]` | `[a-zA-Z]` |
| `[:alnum:]` | `[0-9a-zA-Z]` |
| `[:word:]` | `[0-9a-zA-Z_]` |
| `[:xdigit:]` | `[0-9a-fA-F]` |
| `[:cntrl:]` | control characters — first 32 ASCII characters and 127th (DEL) |
| `[:punct:]` | all the punctuation characters |
| `[:graph:]` | `[:alnum:]` and `[:punct:]` |
| `[:print:]` | `[:alnum:]`, `[:punct:]` and space |
| `[:ascii:]` | all the ASCII characters |
| `[:blank:]` | space and tab characters |
| `[:space:]` | whitespace characters |

```
[](#cb92-1)# starting with a digit character, same as: [0-9]*
[](#cb92-2)$ ls [[:digit:]]*
[](#cb92-3)100.sh  42.txt
[](#cb92-4)
[](#cb92-5)# starting with a digit character or 'c'
[](#cb92-6)# same as: [0-9c]*
[](#cb92-7)$ ls [[:digit:]c]*
[](#cb92-8)100.sh  42.txt  calc.py
[](#cb92-9)
[](#cb92-10)# starting with a non-alphabet character
[](#cb92-11)$ ls [^[:alpha:]]*
[](#cb92-12)100.sh  42.txt
```

> ![info](media/file2.svg) As mentioned before, you can use `echo` to test how the wildcards will expand before using a command to act upon the matching files. For example, `echo *.txt` before using commands like `rm *.txt`. One difference compared to `ls` is that `echo` will display the wildcard as is instead of showing an error if there's no match.

> ![info](media/file0.svg) See [bash manual: Pattern Matching](https://www.gnu.org/software/bash/manual/bash.html#Pattern-Matching) for more details, information on locale stuff and so on.

## Brace Expansion

This is not a wildcard feature, you just get expanded strings. Brace expansion has two mechanisms for reducing typing:

*   taking out common portions among multiple strings
*   generating a range of characters

Say you want to create two files named `test_x.txt` and `test_y.txt`. These two strings have something in common at the start and the end. You can specify the unique portions as comma separated strings within a pair of curly braces and put the common parts around the braces. Multiple braces can be used as needed. Use `echo` for testing purposes.

```
[](#cb93-1)$ mkdir practice_brace
[](#cb93-2)$ cd practice_brace
[](#cb93-3)
[](#cb93-4)# same as: touch ip1.txt ip3.txt ip7.txt
[](#cb93-5)$ touch ip{1,3,7}.txt
[](#cb93-6)$ ls ip*txt
[](#cb93-7)ip1.txt  ip3.txt  ip7.txt
[](#cb93-8)
[](#cb93-9)# same as: mv ip1.txt ip_a.txt
[](#cb93-10)$ mv ip{1,_a}.txt
[](#cb93-11)$ ls ip*txt
[](#cb93-12)ip3.txt  ip7.txt  ip_a.txt
[](#cb93-13)
[](#cb93-14)$ echo adders/{half,full}_adder.v
[](#cb93-15)adders/half_adder.v adders/full_adder.v
[](#cb93-16)
[](#cb93-17)$ echo file{0,1}.{txt,log}
[](#cb93-18)file0.txt file0.log file1.txt file1.log
[](#cb93-19)
[](#cb93-20)# empty alternate is allowed too
[](#cb93-21)$ echo file{,1}.txt
[](#cb93-22)file.txt file1.txt
[](#cb93-23)
[](#cb93-24)# example with nested braces
[](#cb93-25)$ echo file.{txt,log{,.bkp}}
[](#cb93-26)file.txt file.log file.log.bkp
```

To generate a range, specify numbers or single characters separated by `..` and an optional third argument as the step value. Here are some examples:

```
[](#cb94-1)$ echo {1..4}
[](#cb94-2)1 2 3 4
[](#cb94-3)$ echo {4..1}
[](#cb94-4)4 3 2 1
[](#cb94-5)
[](#cb94-6)$ echo {1..2}{a..b}
[](#cb94-7)1a 1b 2a 2b
[](#cb94-8)
[](#cb94-9)$ echo file{1..4}.txt
[](#cb94-10)file1.txt file2.txt file3.txt file4.txt
[](#cb94-11)
[](#cb94-12)$ echo file{1..10..2}.txt
[](#cb94-13)file1.txt file3.txt file5.txt file7.txt file9.txt
[](#cb94-14)
[](#cb94-15)$ echo file_{x..z}.txt
[](#cb94-16)file_x.txt file_y.txt file_z.txt
[](#cb94-17)
[](#cb94-18)$ echo {z..j..-3}
[](#cb94-19)z w t q n k
[](#cb94-20)
[](#cb94-21)# '0' prefix
[](#cb94-22)$ echo {008..10}
[](#cb94-23)008 009 010
```

If the use of braces doesn't match the expansion syntax, it will be left as is:

```
[](#cb95-1)$ echo file{1}.txt
[](#cb95-2)file{1}.txt
[](#cb95-3)
[](#cb95-4)$ echo file{1-4}.txt
[](#cb95-5)file{1-4}.txt
```

## Extended and Recursive globs

From `man bash`:

| Extended glob | Description |
| --- | --- |
| `?(pattern-list)` | Matches zero or one occurrence of the given patterns |
| `*(pattern-list)` | Matches zero or more occurrences of the given patterns |
| `+(pattern-list)` | Matches one or more occurrences of the given patterns |
| `@(pattern-list)` | Matches one of the given patterns |
| `!(pattern-list)` | Matches anything except one of the given patterns |

Extended globs are disabled by default. You can use the `shopt` builtin to set/unset **sh**ell **opt**ions like `extglob`, `globstar`, etc. You can also check what is the current status of such options.

```
[](#cb96-1)$ shopt extglob 
[](#cb96-2)extglob         off
[](#cb96-3)
[](#cb96-4)# set extglob
[](#cb96-5)$ shopt -s extglob 
[](#cb96-6)$ shopt extglob 
[](#cb96-7)extglob         on
[](#cb96-8)
[](#cb96-9)# unset extglob
[](#cb96-10)$ shopt -u extglob 
[](#cb96-11)$ shopt extglob 
[](#cb96-12)extglob         off
```

Here are some examples, assuming `extglob` option has already been set:

```
[](#cb97-1)# change to the 'scripts' directory and source the 'globs.sh' script
[](#cb97-2)$ source globs.sh
[](#cb97-3)$ ls
[](#cb97-4)100.sh   f1.txt      f4.txt    hi.sh   math.h         report-02.log
[](#cb97-5)42.txt   f2_old.txt  f7.txt    ip.txt  notes.txt      report-04.log
[](#cb97-6)calc.py  f2.txt      hello.py  main.c  report-00.log  report-98.log
[](#cb97-7)
[](#cb97-8)# one or more digits followed by '.' and then zero or more characters
[](#cb97-9)$ ls +([0-9]).*
[](#cb97-10)100.sh  42.txt
[](#cb97-11)
[](#cb97-12)# same as: ls *.c *.sh
[](#cb97-13)$ ls *.@(c|sh)
[](#cb97-14)100.sh  hi.sh  main.c
[](#cb97-15)
[](#cb97-16)# not ending with '.txt'
[](#cb97-17)$ ls !(*.txt)
[](#cb97-18)100.sh   hello.py  main.c  report-00.log  report-04.log
[](#cb97-19)calc.py  hi.sh     math.h  report-02.log  report-98.log
[](#cb97-20)
[](#cb97-21)# not ending with '.txt' or '.log'
[](#cb97-22)$ ls *.!(txt|log)
[](#cb97-23)100.sh  calc.py  hello.py  hi.sh  main.c  math.h
```

If you enable the `globstar` option, you can recursively match filenames within a specified path.

```
[](#cb98-1)# change to the 'scripts' directory and source the 'ls.sh' script
[](#cb98-2)$ source ls.sh
[](#cb98-3)
[](#cb98-4)# with 'find' command (this will be explained in a later chapter)
[](#cb98-5)$ find -name '*.txt'
[](#cb98-6)./todos/books.txt
[](#cb98-7)./todos/outing.txt
[](#cb98-8)./ip.txt
[](#cb98-9)
[](#cb98-10)# with 'globstar' enabled
[](#cb98-11)$ shopt -s globstar
[](#cb98-12)$ ls **/*.txt
[](#cb98-13)ip.txt  todos/books.txt  todos/outing.txt
[](#cb98-14)
[](#cb98-15)# another example
[](#cb98-16)$ ls -1 **/*.@(py|html)
[](#cb98-17)backups/bookmarks.html
[](#cb98-18)hello_world.py
[](#cb98-19)projects/tictactoe/game.py
```

> ![info](media/file2.svg) Add the `shopt` invocations to `~/.bashrc` if you want these settings applied at terminal startup. This will be discussed in the [Shell Customization](#ch015.xhtml_shell-customization) chapter.

## set

The `set` builtin command helps you to set or unset values of shell options and positional parameters. Here are some examples for shell options:

```
[](#cb99-1)# disables logging command history from this point onwards
[](#cb99-2)$ set +o history
[](#cb99-3)# enable history logging
[](#cb99-4)$ set -o history
[](#cb99-5)
[](#cb99-6)# use vi-style CLI editing interface
[](#cb99-7)$ set -o vi
[](#cb99-8)# use emancs-style interface, this is usually the default
[](#cb99-9)$ set -o emacs
```

You'll see more examples (for example, `set -x`) in later chapters. See [bash manual: Set Builtin](https://www.gnu.org/software/bash/manual/bash.html#The-Set-Builtin) for documentation.

## Pipelines

The pipe control operator `|` helps you connect the output of a command as the input of another command. This operator vastly reduces the need for temporary intermediate files. As discussed previously in the [Unix Philosophy](#ch003.xhtml_unix-philosophy) section, command line tools specialize in one task. If you can break down a problem into smaller tasks, the pipe operator will come in handy often. Here are some examples:

```
[](#cb100-1)# change to the 'scripts' directory and source the 'du.sh' script
[](#cb100-2)$ source du.sh
[](#cb100-3)
[](#cb100-4)# list of files
[](#cb100-5)$ ls
[](#cb100-6)projects  report.log  todos
[](#cb100-7)# count the number of files
[](#cb100-8)# you can also use: printf '%q\n' * | wc -l
[](#cb100-9)$ ls -q | wc -l
[](#cb100-10)3
[](#cb100-11)
[](#cb100-12)# report size of files/folders in human readable format
[](#cb100-13)# and then sort them based on human readable sizes in ascending order
[](#cb100-14)$ du -sh * | sort -h
[](#cb100-15)8.0K    todos
[](#cb100-16)48K     projects
[](#cb100-17)7.4M    report.log
```

In the above examples, `ls` and `du` perform their own tasks of displaying list of files and showing file sizes respectively. After that, the `wc` and `sort` commands take care of calculating number of lines and sorting respectively. In such cases, the pipe operator saves you the trouble of dealing with temporary data.

Note that the `%q` format specifier in `printf` helps you quote the arguments in a way that is recognizable by the shell. The `-q` option for `ls` substitutes nongraphic characters in the filenames with a `?` character. Both of these are workarounds to prevent the counting process from getting sidetracked due to characters like newline in the filenames.

> ![info](media/file0.svg) The pipe control operator `|&` will be discussed later in this chapter.

### tee

Sometimes, you might want to display the command output on the terminal as well as require the results for later use. In such cases, you can use the `tee` command:

```
[](#cb101-1)$ du -sh * | tee sizes.log
[](#cb101-2)48K     projects
[](#cb101-3)7.4M    report.log
[](#cb101-4)8.0K    todos
[](#cb101-5)
[](#cb101-6)$ cat sizes.log
[](#cb101-7)48K     projects
[](#cb101-8)7.4M    report.log
[](#cb101-9)8.0K    todos
[](#cb101-10)
[](#cb101-11)$ rm sizes.log
```

## Redirection

From [bash manual: Redirections](https://www.gnu.org/software/bash/manual/bash.html#Redirections):

> Before a command is executed, its input and output may be *redirected* using a special notation interpreted by the shell. Redirection allows commands' file handles to be duplicated, opened, closed, made to refer to different files, and can change the files the command reads from and writes to. Redirection may also be used to modify file handles in the current shell execution environment.

There are three standard data streams:

*   **standard input** (`stdin` — file descriptor 0)
*   **standard output** (`stdout` — file descriptor 1)
*   **standard error** (`stderr` — file descriptor 2)

Both standard output and error are displayed on the terminal by default. The `stderr` stream is used when something goes wrong with the command usage. Each of these three streams have a predefined [file descriptor](https://en.wikipedia.org/wiki/File_descriptor) as mentioned above. In this section, you'll see how to redirect these three streams.

> ![info](media/file0.svg) Redirections can be placed anywhere, but they are usually used at the start or end of a command. For example, the following two commands are equivalent:
> 
> ```
> [](#cb102-1)>op.txt grep 'error' report.log
> [](#cb102-2)
> [](#cb102-3)grep 'error' report.log >op.txt
> ```

> ![info](media/file2.svg) Space characters between the redirection operators and the filename are optional.

### Redirecting output

You can use the `>` operator to redirect the standard output of a command to a file. A number prefix can be added to the `>` operator to work with that particular file descriptor. Default is `1` (recall that the file descriptor for `stdout` is `1`), so `1>` and `>` perform the same operation. Use `>>` to append the output to a file.

The filename provided to the `>` and `>>` operators will be created if a regular file of that name doesn't exist yet. If the file already exists, `>` will overwrite that file and `>>` will append contents to that file.

```
[](#cb103-1)# change to the 'example_files/text_files' directory for this section
[](#cb103-2)
[](#cb103-3)# save first three lines of 'sample.txt' to 'op.txt'
[](#cb103-4)$ head -n3 sample.txt > op.txt
[](#cb103-5)$ cat op.txt
[](#cb103-6) 1) Hello World
[](#cb103-7) 2) 
[](#cb103-8) 3) Hi there
[](#cb103-9)
[](#cb103-10)# append last two lines of 'sample.txt' to 'op.txt'
[](#cb103-11)$ tail -n2 sample.txt >> op.txt
[](#cb103-12)$ cat op.txt
[](#cb103-13) 1) Hello World
[](#cb103-14) 2) 
[](#cb103-15) 3) Hi there
[](#cb103-16)14) He he he
[](#cb103-17)15) Adios amigo
[](#cb103-18)
[](#cb103-19)$ rm op.txt
```

> ![info](media/file0.svg) You can use `/dev/null` as a filename to discard the output, to provide an empty file for a command, etc.

> ![info](media/file2.svg) You can use `set noclobber` to prevent overwriting if a file already exists. When the `noclobber` option is set, you can still overwrite a file by using `>|` instead of the `>` operator.

### Redirecting input

Some commands like `tr` and `datamash` can only work with data from the standard input. This isn't an issue when you are piping data from another command, for example:

```
[](#cb104-1)# filter lines containing 'the' from the input file 'greeting.txt'
[](#cb104-2)# and then display the results in uppercase using the 'tr' command
[](#cb104-3)$ grep 'the' greeting.txt | tr 'a-z' 'A-Z'
[](#cb104-4)HI THERE
```

You can use the `<` redirection operator if you want to pass data from a file to such commands. The default prefix here is `0`, which is the file descriptor for `stdin` data. Here's an example:

```
[](#cb105-1)$ tr 'a-z' 'A-Z' <greeting.txt
[](#cb105-2)HI THERE
[](#cb105-3)HAVE A NICE DAY
```

In some cases, a tool behaves differently when processing `stdin` data compared to file input. Here's an example with `wc -l` to report the total number of lines in the input:

```
[](#cb106-1)# line count, filename is part of the output as well
[](#cb106-2)$ wc -l purchases.txt
[](#cb106-3)8 purchases.txt
[](#cb106-4)
[](#cb106-5)# filename won't be part of the output for stdin data
[](#cb106-6)# helpful for assigning the number to a variable for scripting purposes
[](#cb106-7)$ wc -l <purchases.txt
[](#cb106-8)8
```

Sometimes, you need to pass `stdin` data as well as other file inputs to a command. In such cases, you can use `-` to represent data from the standard input. Here's an example:

```
[](#cb107-1)$ cat scores.csv
[](#cb107-2)Name,Maths,Physics,Chemistry
[](#cb107-3)Ith,100,100,100
[](#cb107-4)Cy,97,98,95
[](#cb107-5)Lin,78,83,80
[](#cb107-6)
[](#cb107-7)# insert a column at the start
[](#cb107-8)$ printf 'ID\n1\n2\n3' | paste -d, - scores.csv
[](#cb107-9)ID,Name,Maths,Physics,Chemistry
[](#cb107-10)1,Ith,100,100,100
[](#cb107-11)2,Cy,97,98,95
[](#cb107-12)3,Lin,78,83,80
```

Even though a command accepts file input directly as an argument, redirecting can help for interactive usage. Here's an example:

```
[](#cb108-1)# display only the third field
[](#cb108-2)$ <scores.csv cut -d, -f3
[](#cb108-3)Physics
[](#cb108-4)100
[](#cb108-5)98
[](#cb108-6)83
[](#cb108-7)
[](#cb108-8)# later, you realize that you need the first field too
[](#cb108-9)# use 'up' arrow key to bring the previous command
[](#cb108-10)# and modify the argument easily at the end
[](#cb108-11)# if you had used cut -d, -f3 scores.csv instead,
[](#cb108-12)# you'd have to navigate past the filename to modify the argument
[](#cb108-13)$ <scores.csv cut -d, -f1,3
[](#cb108-14)Name,Physics
[](#cb108-15)Ith,100
[](#cb108-16)Cy,98
[](#cb108-17)Lin,83
```

> ![info](media/file0.svg) ![warning](media/file1.svg) Don't use `cat filename | cmd` for passing file content as `stdin` data, unless you need to concatenate data from multiple input files. See [wikipedia: UUOC](https://en.wikipedia.org/wiki/Cat_(Unix)#Useless_use_of_cat) and [Useless Use of Cat Award](https://porkmail.org/era/unix/award.html) for more details.

### Redirecting error

Recall that the file descriptor for `stderr` is `2`. So, you can use `2>` to redirect standard error to a file. Use `2>>` if you need to append the contents. Here's an example:

```
[](#cb109-1)# assume 'abcdxyz' doesn't exist as a shell command
[](#cb109-2)$ abcdxyz
[](#cb109-3)abcdxyz: command not found
[](#cb109-4)
[](#cb109-5)# the error in such cases will be part of the stderr stream, not stdout
[](#cb109-6)# so, you'll need to use 2> here
[](#cb109-7)$ abcdxyz 2> cmderror.log
[](#cb109-8)$ cat cmderror.log
[](#cb109-9)abcdxyz: command not found
[](#cb109-10)
[](#cb109-11)$ rm cmderror.log
```

> ![info](media/file0.svg) Use `/dev/null` as a filename if you need to discard the results.

### Combining stdout and stderr

Newer versions of Bash provide these handy shortcuts:

*   `&>` redirect both `stdout` and `stderr` (overwrites an existing file)
*   `&>>` redirect both `stdout` and `stderr` (appends to existing file)
*   `|&` pipe both `stdout` and `stderr` as input to another command

Here's an example which assumes `xyz.txt` doesn't exist, thus leading to errors:

```
[](#cb110-1)# using '>' will redirect only the stdout stream
[](#cb110-2)# stderr will be displayed on the terminal
[](#cb110-3)$ grep 'log' file_size.txt xyz.txt > op.txt
[](#cb110-4)grep: xyz.txt: No such file or directory
[](#cb110-5)
[](#cb110-6)# using '&>' will redirect both the stdout and stderr streams
[](#cb110-7)$ grep 'log' file_size.txt xyz.txt &> op.txt
[](#cb110-8)$ cat op.txt
[](#cb110-9)file_size.txt:104K    power.log
[](#cb110-10)file_size.txt:746K    report.log
[](#cb110-11)grep: xyz.txt: No such file or directory
[](#cb110-12)
[](#cb110-13)$ rm op.txt
```

And here's an example with the `|&` operator:

```
[](#cb111-1)# filter lines containing 'log' from the given file arguments
[](#cb111-2)# and then filter lines containing 'or' from the combined stdout and stderr
[](#cb111-3)$ grep 'log' file_size.txt xyz.txt |& grep 'or'
[](#cb111-4)file_size.txt:746K    report.log
[](#cb111-5)grep: xyz.txt: No such file or directory
```

For earlier Bash versions, you'll have to manually redirect the streams:

*   `1>&2` redirects file descriptor `1` (`stdout`) to the file descriptor `2` (`stderr`)
*   `2>&1` redirects file descriptor `2` (`stderr`) to the file descriptor `1` (`stdout`)

Here are some examples:

```
[](#cb112-1)# note that the order of redirections is important here
[](#cb112-2)# you can also use: 2> op.txt 1>&2
[](#cb112-3)$ grep 'log' file_size.txt xyz.txt > op.txt 2>&1
[](#cb112-4)$ cat op.txt
[](#cb112-5)file_size.txt:104K    power.log
[](#cb112-6)file_size.txt:746K    report.log
[](#cb112-7)grep: xyz.txt: No such file or directory
[](#cb112-8)$ rm op.txt
[](#cb112-9)
[](#cb112-10)$ grep 'log' file_size.txt xyz.txt 2>&1 | grep 'or'
[](#cb112-11)file_size.txt:746K    report.log
[](#cb112-12)grep: xyz.txt: No such file or directory
```

### Waiting for stdin

Sometimes, you might mistype a command without providing input. And instead of getting an error, you'll see the cursor patiently waiting for something. This isn't the shell hanging up on you. The command is waiting for you to type data, so that it can perform its task.

Say, you typed `cat` and pressed the Enter key. Seeing the blinking cursor, you type some text and press the Enter key again. You'll see the text you just typed echoed back to you as `stdout` (which is the functionality of the `cat` command). This will continue again and again, until you tell the shell that you are done. How to do that? Press `Ctrl+d` on a fresh line or press `Ctrl+d` twice at the end of a line. In the latter case, you'll not get a newline character at the end of the data.

```
[](#cb113-1)# press Enter key and Ctrl+d after typing all the required characters
[](#cb113-2)$ cat
[](#cb113-3)knock knock
[](#cb113-4)knock knock
[](#cb113-5)anybody here?
[](#cb113-6)anybody here?
[](#cb113-7)
[](#cb113-8)# 'tr' command here translates lowercase to uppercase
[](#cb113-9)$ tr 'a-z' 'A-Z'
[](#cb113-10)knock knock 
[](#cb113-11)KNOCK KNOCK
[](#cb113-12)anybody here?
[](#cb113-13)ANYBODY HERE?
```

> ![info](media/file0.svg) Getting output immediately after each input line depends on the command's functionality. Commands like `sort` and `shuf` will wait for the entire input data before producing the output.
> 
> ```
> [](#cb114-1)# press Ctrl+d after the third input line
> [](#cb114-2)$ sort
> [](#cb114-3)lion
> [](#cb114-4)zebra
> [](#cb114-5)bee
> [](#cb114-6)bee
> [](#cb114-7)lion
> [](#cb114-8)zebra
> ```

Here's an example which has output redirection as well:

```
[](#cb115-1)# press Ctrl+d after the line containing 'histogram'
[](#cb115-2)# filter lines containing 'is'
[](#cb115-3)$ grep 'is' > op.txt
[](#cb115-4)hi there
[](#cb115-5)this is a sample line
[](#cb115-6)have a nice day
[](#cb115-7)histogram
[](#cb115-8)
[](#cb115-9)$ cat op.txt
[](#cb115-10)this is a sample line
[](#cb115-11)histogram
[](#cb115-12)
[](#cb115-13)$ rm op.txt
```

> ![info](media/file0.svg) See also [unix.stackexchange: difference between Ctrl+c and Ctrl+d](https://unix.stackexchange.com/q/16333/109046).

### Here Documents

Here Documents is another way to provide `stdin` data. In this case, the termination condition is a line matching a predefined string which is specified after the `<<` redirection operator. This is especially helpful for automation, since pressing `Ctrl+d` interactively isn't desirable. Here's an example:

```
[](#cb116-1)# EOF is typically used as the special string
[](#cb116-2)$ cat << 'EOF' > fruits.txt
[](#cb116-3)> banana 2
[](#cb116-4)> papaya 3
[](#cb116-5)> mango  10
[](#cb116-6)> EOF
[](#cb116-7)
[](#cb116-8)$ cat fruits.txt
[](#cb116-9)banana 2
[](#cb116-10)papaya 3
[](#cb116-11)mango  10
[](#cb116-12)$ rm fruits.txt
```

In the above example, the termination string was enclosed in single quotes to prevent parameter expansion, command substitution, etc. You can also use `\string` for this purpose. If you use `<<-` instead of `<<`, leading tab characters can be added at the start of input lines without being part of the actual data.

> ![info](media/file0.svg) Just like `$` and a space represents the primary prompt (`PS1` shell variable), `>` and a space at the start of lines represents the secondary prompt `PS2` (applicable for multiline commands). Don't type these characters when you use Here Documents in a shell script.

> ![info](media/file0.svg) See [bash manual: Here Documents](https://www.gnu.org/software/bash/manual/bash.html#Here-Documents) and [stackoverflow: here documents](https://stackoverflow.com/q/2953081/4082052) for more examples and details.

### Here Strings

This is similar to Here Documents, but the termination string isn't used. The redirection operator is `<<<`. Here are some examples:

```
[](#cb117-1)$ tr 'a-z' 'A-Z' <<< hello
[](#cb117-2)HELLO
[](#cb117-3)$ tr 'a-z' 'A-Z' <<< 'hello world'
[](#cb117-4)HELLO WORLD
[](#cb117-5)
[](#cb117-6)$ greeting='hello world'
[](#cb117-7)$ tr 'a-z' 'A-Z' > op.txt <<< "$greeting"
[](#cb117-8)$ cat op.txt
[](#cb117-9)HELLO WORLD
[](#cb117-10)$ rm op.txt
```

### Further Reading

*   [Short introduction to shell redirection](https://mywiki.wooledge.org/BashGuide/InputAndOutput#Redirection)
*   [Illustrated Redirection Tutorial](https://wiki.bash-hackers.org/howto/redirection_tutorial)
*   [stackoverflow: Redirect a stream to another file descriptor using >&](https://stackoverflow.com/q/818255/4082052)
*   [Difference between 2>&1 >foo and >foo 2>&1](https://mywiki.wooledge.org/BashFAQ/055)
*   [stackoverflow: Redirect and append both stdout and stderr to a file](https://stackoverflow.com/q/876239/4082052)
*   [unix.stackexchange: Examples for <> redirection](https://unix.stackexchange.com/q/164391/109046)

## Grouping commands

You can use `(list)` and `{ list; }` compound commands to redirect content for several commands. The former is executed in a subshell whereas the latter is executed in the current shell context. Spaces around `()` are optional but necessary for the `{}` version. From [bash manual: Lists of Commands](https://www.gnu.org/software/bash/manual/bash.html#Lists):

> A `list` is a sequence of one or more pipelines separated by one of the operators `;`, `&`, `&&`, or `||`, and optionally terminated by one of `;`, `&`, or a newline.

Here are some examples of command groupings:

```
[](#cb118-1)# change to the 'example_files/text_files' directory for this section
[](#cb118-2)
[](#cb118-3)# the 'sed' command here gives the first line of the input
[](#cb118-4)# rest of the lines are then processed by the 'sort' command
[](#cb118-5)# thus, the header will always be the first line in the output
[](#cb118-6)$ (sed -u '1q' ; sort) < scores.csv
[](#cb118-7)Name,Maths,Physics,Chemistry
[](#cb118-8)Cy,97,98,95
[](#cb118-9)Ith,100,100,100
[](#cb118-10)Lin,78,83,80
[](#cb118-11)
[](#cb118-12)# save first three and last two lines from 'sample.txt' to 'op.txt'
[](#cb118-13)$ { head -n3 sample.txt; tail -n2 sample.txt; } > op.txt
[](#cb118-14)$ cat op.txt
[](#cb118-15) 1) Hello World
[](#cb118-16) 2) 
[](#cb118-17) 3) Hi there
[](#cb118-18)14) He he he
[](#cb118-19)15) Adios amigo
[](#cb118-20)$ rm op.txt
```

You might wonder why the second command did not use `< sample.txt` instead of repeating the filename twice. The reason is that some commands might read more than what is required (for buffering purposes) and thus cause issues for the remaining commands. In the `sed+sort` example, the `-u` option guarantees that `sed` will not to read more than the required data. See [unix.stackexchange: sort but keep header line at the top](https://unix.stackexchange.com/q/11856/109046) for more examples and details.

> ![info](media/file0.svg) You don't need the `()` or `{}` groups to see the results of multiple commands on the terminal. Just the `;` separator between the commands would be enough. See also [bash manual: Command Execution Environment](https://www.gnu.org/software/bash/manual/bash.html#Command-Execution-Environment).
> 
> ```
> [](#cb119-1)$ head -n1 sample.txt ; echo 'have a nice day'
> [](#cb119-2) 1) Hello World
> [](#cb119-3)have a nice day
> ```

## List control operators

You can use these operators to control the execution of the subsequent command depending on the exit status of the first command. From [bash manual: Lists of Commands](https://www.gnu.org/software/bash/manual/bash.html#Lists):

> AND and OR lists are sequences of one or more pipelines separated by the control operators `&&` and `||`, respectively. AND and OR lists are executed with left associativity.

For AND list, the second command will be executed if and only if the first command exits with `0` status.

```
[](#cb120-1)# first command succeeds here, so the second command is also executed
[](#cb120-2)$ echo 'hello' && echo 'have a nice day'
[](#cb120-3)hello
[](#cb120-4)have a nice day
[](#cb120-5)
[](#cb120-6)# assume 'abcdxyz' doesn't exist as a shell command
[](#cb120-7)# the second command will not be executed
[](#cb120-8)$ abcdxyz && echo 'have a nice day'
[](#cb120-9)abcdxyz: command not found
[](#cb120-10)
[](#cb120-11)# if you use ';' instead, the second command will still be executed
[](#cb120-12)$ abcdxyz ; echo 'have a nice day'
[](#cb120-13)abcdxyz: command not found
[](#cb120-14)have a nice day
```

For OR list, the second command will be executed if and only if the first command does *not* exit with `0` status.

```
[](#cb121-1)# since the first command succeeds, the second one won't run
[](#cb121-2)$ echo 'hello' || echo 'have a nice day'
[](#cb121-3)hello
[](#cb121-4)
[](#cb121-5)# assume 'abcdxyz' doesn't exist as a shell command
[](#cb121-6)# since the first command fails, the second one will run
[](#cb121-7)$ abcdxyz || echo 'have a nice day'
[](#cb121-8)abcdxyz: command not found
[](#cb121-9)have a nice day
```

## Command substitution

Command substitution allows you to use the standard output of a command as part of another command. Trailing newlines, if any, will be removed. You can use the newer and preferred syntax `$(command)` or the older syntax `` `command` ``. Here are some examples:

```
[](#cb122-1)# sample input
[](#cb122-2)$ printf 'hello\ntoday is: \n'
[](#cb122-3)hello
[](#cb122-4)today is:
[](#cb122-5)# append output from the 'date' command to the line containing 'today'
[](#cb122-6)$ printf 'hello\ntoday is: \n' | sed '/today/ s/$/'"$(date +%A)"'/'
[](#cb122-7)hello
[](#cb122-8)today is: Monday
[](#cb122-9)
[](#cb122-10)# save the output of 'wc' command to a variable
[](#cb122-11)# same as: line_count=`wc -l <sample.txt`
[](#cb122-12)$ line_count=$(wc -l <sample.txt)
[](#cb122-13)$ echo "$line_count"
[](#cb122-14)15
```

Here's an example with nested substitutions:

```
[](#cb123-1)# dirname removes the trailing path component
[](#cb123-2)$ dirname projects/tictactoe/game.py
[](#cb123-3)projects/tictactoe
[](#cb123-4)# basename removes the leading directory component
[](#cb123-5)$ basename projects/tictactoe
[](#cb123-6)tictactoe
[](#cb123-7)
[](#cb123-8)$ proj=$(basename $(dirname projects/tictactoe/game.py))
[](#cb123-9)$ echo "$proj"
[](#cb123-10)tictactoe
```

Difference between the two types of syntax is quoted below from [bash manual: Command Substitution](https://www.gnu.org/software/bash/manual/bash.html#Command-Substitution):

> When the old-style backquote form of substitution is used, backslash retains its literal meaning except when followed by `$`, `` ` ``, or `\`. The first backquote not preceded by a backslash terminates the command substitution. When using the $(command) form, all characters between the parentheses make up the command; none are treated specially.
> 
> Command substitutions may be nested. To nest when using the backquoted form, escape the inner backquotes with backslashes.

## Process substitution

Instead of a file argument, you can use the output of commands with process substitution. The syntax is `<(list)`. The shell will take care of passing a filename with the standard output of those commands. Here's an example:

```
[](#cb124-1)# change to the 'example_files/text_files' directory for this section
[](#cb124-2)
[](#cb124-3)$ cat scores.csv
[](#cb124-4)Name,Maths,Physics,Chemistry
[](#cb124-5)Ith,100,100,100
[](#cb124-6)Cy,97,98,95
[](#cb124-7)Lin,78,83,80
[](#cb124-8)
[](#cb124-9)# can also use: paste -d, <(echo 'ID'; seq 3) scores.csv
[](#cb124-10)$ paste -d, <(printf 'ID\n1\n2\n3') scores.csv 
[](#cb124-11)ID,Name,Maths,Physics,Chemistry
[](#cb124-12)1,Ith,100,100,100
[](#cb124-13)2,Cy,97,98,95
[](#cb124-14)3,Lin,78,83,80
```

For the above example, you could also have used `-` to represent `stdin` piped data as seen in an earlier section. Here's an example where two substitutions are used. This essentially helps you to avoid managing multiple temporary files, similar to how the `|` pipe operator helps for single temporary file.

```
[](#cb125-1)# side-by-side view of sample input files
[](#cb125-2)$ paste f1.txt f2.txt
[](#cb125-3)1       1
[](#cb125-4)2       hello
[](#cb125-5)3       3
[](#cb125-6)world   4
[](#cb125-7)
[](#cb125-8)# this command gives the common lines between two files
[](#cb125-9)# the files have to be sorted for the command to work properly
[](#cb125-10)$ comm -12 <(sort f1.txt) <(sort f2.txt)
[](#cb125-11)1
[](#cb125-12)3
```

> ![info](media/file0.svg) See [this unix.stackexchange thread](https://unix.stackexchange.com/q/609375/109046) for examples with `>(list)` form.

## Exercises

> ![info](media/file0.svg) Use the `globs.sh` script for wildcards related exercises, unless otherwise mentioned.

> ![info](media/file0.svg) Create a temporary directory for exercises that may require you to create some files. You can delete such practice directories afterwards.

**1)** Use the `echo` command to display the text as shown below. Use appropriate quoting as necessary.

```
[](#cb126-1)# ???
[](#cb126-2)that's    great! $x = $y + $z
```

**2)** Use the `echo` command to display the values of the three variables in the format as shown below.

```
[](#cb127-1)$ n1=10
[](#cb127-2)$ n2=90
[](#cb127-3)$ op=100
[](#cb127-4)
[](#cb127-5)# ???
[](#cb127-6)10 + 90 = 100
```

**3)** What will be the output of the command shown below?

```
[](#cb128-1)$ echo $'\x22apple\x22: \x2710\x27'
```

**4)** List filenames starting with a digit character.

```
[](#cb129-1)# change to the 'scripts' directory and source the 'globs.sh' script
[](#cb129-2)$ source globs.sh
[](#cb129-3)
[](#cb129-4)# ???
[](#cb129-5)100.sh  42.txt
```

**5)** List filenames whose extension do not begin with `t` or `l`. Assume extensions will have at least one character.

```
[](#cb130-1)# ???
[](#cb130-2)100.sh  calc.py  hello.py  hi.sh  main.c  math.h
```

**6)** List filenames whose extension only have a single character.

```
[](#cb131-1)# ???
[](#cb131-2)main.c  math.h
```

**7)** List filenames whose extension is not `txt`.

```
[](#cb132-1)# ???
[](#cb132-2)100.sh   hello.py  main.c  report-00.log  report-04.log
[](#cb132-3)calc.py  hi.sh     math.h  report-02.log  report-98.log
```

**8)** Describe the wildcard pattern used in the command shown below.

```
[](#cb133-1)$ ls *[^[:word:]]*.*
[](#cb133-2)report-00.log  report-02.log  report-04.log  report-98.log
```

**9)** List filenames having only lowercase alphabets before the extension.

```
[](#cb134-1)# ???
[](#cb134-2)calc.py  hello.py  hi.sh  ip.txt  main.c  math.h  notes.txt
```

**10)** List filenames starting with `ma` or `he` or `hi`.

```
[](#cb135-1)# ???
[](#cb135-2)hello.py  hi.sh  main.c  math.h
```

**11)** What commands would you use to get the outputs shown below? Assume that you do not know the depth of sub-directories.

```
[](#cb136-1)# change to the 'scripts' directory and source the 'ls.sh' script
[](#cb136-2)$ source ls.sh
[](#cb136-3)
[](#cb136-4)# filenames ending with '.txt'
[](#cb136-5)# ???
[](#cb136-6)ip.txt  todos/books.txt  todos/outing.txt
[](#cb136-7)
[](#cb136-8)# directories starting with 'c' or 'd' or 'g' or 'r' or 't'
[](#cb136-9)# ???
[](#cb136-10)backups/dot_files/
[](#cb136-11)projects/calculator/
[](#cb136-12)projects/tictactoe/
[](#cb136-13)todos/
```

**12)** Create and change to an empty directory. Then, use brace expansion along with relevant commands to get the results shown below.

```
[](#cb137-1)# ???
[](#cb137-2)$ ls report*
[](#cb137-3)report_2020.txt  report_2021.txt  report_2022.txt
[](#cb137-4)
[](#cb137-5)# use 'cp' command here
[](#cb137-6)# ???
[](#cb137-7)$ ls report*
[](#cb137-8)report_2020.txt  report_2021.txt  report_2021.txt.bkp  report_2022.txt
```

**13)** What does the `set` builtin command do?

**14)** What does the `|` pipe operator do? And when would you add the `tee` command?

**15)** Can you infer what the following command does? *Hint*: see `help printf`.

```
[](#cb138-1)$ printf '%s\n' apple car dragon
[](#cb138-2)apple
[](#cb138-3)car
[](#cb138-4)dragon
```

**16)** Use brace expansion along with relevant commands and shell features to get the result shown below. *Hint*: see previous question.

```
[](#cb139-1)$ ls ip.txt
[](#cb139-2)ls: cannot access 'ip.txt': No such file or directory
[](#cb139-3)
[](#cb139-4)# ???
[](#cb139-5)$ cat ip.txt
[](#cb139-6)item_10
[](#cb139-7)item_12
[](#cb139-8)item_14
[](#cb139-9)item_16
[](#cb139-10)item_18
[](#cb139-11)item_20
```

**17)** With `ip.txt` containing text as shown in the previous question, use brace expansion and relevant commands to get the result shown below.

```
[](#cb140-1)# ???
[](#cb140-2)$ cat ip.txt
[](#cb140-3)item_10
[](#cb140-4)item_12
[](#cb140-5)item_14
[](#cb140-6)item_16
[](#cb140-7)item_18
[](#cb140-8)item_20
[](#cb140-9)apple_1_banana_6
[](#cb140-10)apple_1_banana_7
[](#cb140-11)apple_1_banana_8
[](#cb140-12)apple_2_banana_6
[](#cb140-13)apple_2_banana_7
[](#cb140-14)apple_2_banana_8
[](#cb140-15)apple_3_banana_6
[](#cb140-16)apple_3_banana_7
[](#cb140-17)apple_3_banana_8
```

**18)** What are the differences between `<` and `|` shell operators, if any?

**19)** Which character is typically used to represent `stdin` data as a file argument?

**20)** What do the following operators do?

*a)* `1>`
*b)* `2>`
*c)* `&>`
*d)* `&>>`
*e)* `|&`

**21)** What will be the contents of `op.txt` if you use the following `grep` command?

```
[](#cb141-1)# press Ctrl+d after the line containing 'histogram'
[](#cb141-2)$ grep 'hi' > op.txt
[](#cb141-3)hi there
[](#cb141-4)this is a sample line
[](#cb141-5)have a nice day
[](#cb141-6)histogram
[](#cb141-7)
[](#cb141-8)$ cat op.txt
```

**22)** What will be the contents of `op.txt` if you use the following commands?

```
[](#cb142-1)$ qty=42
[](#cb142-2)$ cat << end > op.txt
[](#cb142-3)> dragon
[](#cb142-4)> unicorn
[](#cb142-5)> apple $qty
[](#cb142-6)> ice cream
[](#cb142-7)> end
[](#cb142-8)
[](#cb142-9)$ cat op.txt
```

**23)** Correct the command to get the expected output shown below.

```
[](#cb143-1)$ books='cradle piranesi soulhome bastion'
[](#cb143-2)
[](#cb143-3)# something is wrong with this command
[](#cb143-4)$ sed 's/\b\w/\u&/g' <<< '$books'
[](#cb143-5)$Books
[](#cb143-6)
[](#cb143-7)# ???
[](#cb143-8)Cradle Piranesi Soulhome Bastion
```

**24)** Correct the command to get the expected output shown below.

```
[](#cb144-1)# something is wrong with this command
[](#cb144-2)$ echo 'hello' ; seq 3 > op.txt
[](#cb144-3)hello
[](#cb144-4)$ cat op.txt
[](#cb144-5)1
[](#cb144-6)2
[](#cb144-7)3
[](#cb144-8)
[](#cb144-9)# ???
[](#cb144-10)$ cat op.txt
[](#cb144-11)hello
[](#cb144-12)1
[](#cb144-13)2
[](#cb144-14)3
```

**25)** What will be the output of the following commands?

```
[](#cb145-1)$ printf 'hello' | tr 'a-z' 'A-Z' && echo ' there'
[](#cb145-2)
[](#cb145-3)$ printf 'hello' | tr 'a-z' 'A-Z' || echo ' there'
```

**26)** Correct the command(s) to get the expected output shown below.

```
[](#cb146-1)# something is wrong with these commands
[](#cb146-2)$ nums=$(seq 3)
[](#cb146-3)$ echo $nums
[](#cb146-4)1 2 3
[](#cb146-5)
[](#cb146-6)# ???
[](#cb146-7)1
[](#cb146-8)2
[](#cb146-9)3
```

**27)** Will the following two commands produce equivalent output? If not, why not?

```
[](#cb147-1)$ paste -d, <(seq 3) <(printf '%s\n' item_{1..3})
[](#cb147-2)
[](#cb147-3)$ printf '%s\n' {1..3},item_{1..3}
```

# Viewing Part or Whole File Contents

In this chapter, you'll learn how to view contents of files from within the terminal. If the contents are too long, you can choose to view one screenful at a time or get only the starting/ending portions of the input. The commands used for these purposes also have other functionalities, some of which will be discussed in this chapter as well.

> ![info](media/file0.svg) The [example_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files) directory has the sample input files used in this chapter.

## cat

The `cat` command derives its name from con**cat**enate. It is primarily used to combine the contents of multiple files to be saved in a file or sent as input to another command.

Commonly used options are shown below:

*   `-n` prefix line number and a tab character to each input line
*   `-b` like `-n` but doesn't number empty lines
*   `-s` squeeze consecutive empty lines to a single empty line
*   `-v` view special characters like NUL using the [caret notation](https://en.wikipedia.org/wiki/ASCII_control_characters#Control_code_chart)
*   `-e` view special characters as well as mark the end of line
*   `-A` includes `-e` and also helps to spot tab characters

Here are some examples to showcase `cat`'s main utility. One or more files can be given as arguments.

> ![info](media/file0.svg) As mentioned earlier, the [example_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files) directory has the sample input files used in this chapter. You need to `cd` into the `example_files/text_files` directory to follow along the examples shown in this chapter.

```
[](#cb148-1)# view contents of a single file
[](#cb148-2)$ cat greeting.txt
[](#cb148-3)Hi there
[](#cb148-4)Have a nice day
[](#cb148-5)
[](#cb148-6)# another example
[](#cb148-7)$ cat fruits.txt
[](#cb148-8)banana
[](#cb148-9)papaya
[](#cb148-10)mango
[](#cb148-11)
[](#cb148-12)# concatenate multiple files
[](#cb148-13)$ cat greeting.txt fruits.txt
[](#cb148-14)Hi there
[](#cb148-15)Have a nice day
[](#cb148-16)banana
[](#cb148-17)papaya
[](#cb148-18)mango
```

To save the output of concatenation, use redirection:

```
[](#cb149-1)$ cat greeting.txt fruits.txt > op.txt
[](#cb149-2)
[](#cb149-3)$ cat op.txt
[](#cb149-4)Hi there
[](#cb149-5)Have a nice day
[](#cb149-6)banana
[](#cb149-7)papaya
[](#cb149-8)mango
```

You can represent `stdin` data using `-` as a file argument. If file arguments are not present, `cat` will read from `stdin` data if present or wait for interactive input. Note that `-` is also supported by many more commands to indicate `stdin` data.

```
[](#cb150-1)# concatenate contents of 'greeting.txt' and 'stdin' data
[](#cb150-2)$ echo 'apple banana cherry' | cat greeting.txt -
[](#cb150-3)Hi there
[](#cb150-4)Have a nice day
[](#cb150-5)apple banana cherry
```

> ![info](media/file0.svg) Using `cat` to view the contents of a file, to concatenate them, etc is well and good. But, using `cat` when it is not needed is a bad habit that you should avoid. See [wikipedia: UUOC](https://en.wikipedia.org/wiki/Cat_(Unix)#Useless_use_of_cat) and [Useless Use of Cat Award](https://porkmail.org/era/unix/award.html) for more details.

`cat` also helps you spot special characters using the [caret notation](https://en.wikipedia.org/wiki/ASCII_control_characters#Control_code_chart):

```
[](#cb151-1)# example for backspace and carriage return characters
[](#cb151-2)$ printf 'car\bd\nbike\rp\n'
[](#cb151-3)cad
[](#cb151-4)pike
[](#cb151-5)$ printf 'car\bd\nbike\rp\n' | cat -v
[](#cb151-6)car^Hd
[](#cb151-7)bike^Mp
[](#cb151-8)
[](#cb151-9)# example with tab characters and end-of-line marker
[](#cb151-10)$ printf '1 2\t3\f4\v5   \n' | cat -A
[](#cb151-11)1 2^I3^L4^K5   $
```

## tac

You can concatenate files using `tac` as well, but the output will be printed in the reverse (line wise). If you pass multiple input files, each file content will be reversed separately. Here are some examples:

```
[](#cb152-1)$ printf 'apple\nbanana\ncherry\n' | tac
[](#cb152-2)cherry
[](#cb152-3)banana
[](#cb152-4)apple
[](#cb152-5)
[](#cb152-6)# won't be same as: cat greeting.txt fruits.txt | tac
[](#cb152-7)$ tac greeting.txt fruits.txt
[](#cb152-8)Have a nice day
[](#cb152-9)Hi there
[](#cb152-10)mango
[](#cb152-11)papaya
[](#cb152-12)banana
```

> ![warning](media/file1.svg) If the last line of input doesn't end with a newline, the output will also not have that newline character.

```
[](#cb153-1)$ printf 'apple\nbanana\ncherry' | tac
[](#cb153-2)cherrybanana
[](#cb153-3)apple
```

## less

The `cat` command is not suitable for viewing contents of large files in the terminal. The `less` command automatically fits the content to the size of terminal, allows scrolling and has nifty features for effective viewing. Usually, `man` command uses `less` as the `pager` to display the documentation. The navigation options are similar to the Vim text editor.

Commonly used commands are given below. You can press the `h` key for builtin help.

*   `↑` and `↓` arrow keys to move up and down by a line
    *   you can also use `k` and `j` keys (same keys as those used in the Vim text editor)
*   `f` and `b` keys to move forward and backward by a screenful of content
    *   `Space` key also moves forward by a screen
*   mouse scroll moves up and down by a few lines
*   `g` or `Home` go to the start of the file
*   `G` or `End` go to the end of the file
*   `/pattern` followed by `Enter` search for the given pattern in the forward direction
    *   pattern refers to regular expressions and depends on the regex library in your system
    *   the flavor is Extended Regular Expressions (ERE) on my system
    *   see `man re_format` for more details
*   `?pattern` followed by `Enter` search for the given pattern in the backward direction
*   `n` go to the next match
*   `N` go to the previous match
*   `q` quit

As an example, use `less /usr/share/dict/words` to open a dictionary file and practice the commands discussed above. If your `pager` is set to `less` for manual pages, you can also try something like `man ls` for practice.

Similar to the `cat` command, you can use the `-s` option to squeeze consecutive blank lines. But unlike `cat -n`, you need to use `less -N` to prefix line numbers. The lowercase `-n` option will turn off numbering.

**Further Reading**

*   `less` command is an [improved version](https://unix.stackexchange.com/q/604/109046) of the `more` command
*   [unix.stackexchange: differences between most, more and less](https://unix.stackexchange.com/q/81129/109046)
*   My [Vim Reference Guide](https://github.com/learnbyexample/vim_reference) ebook

## tail

By default, `tail` displays the last 10 lines of input file(s). If there are less than 10 lines in the input, only those lines will be displayed. You can use the `-n` option to change the number of lines displayed. By using `tail -n +N`, you can get all the lines starting from the `N`th line.

Here's an example file that'll be used for illustration purposes:

```
[](#cb154-1)$ cat sample.txt 
[](#cb154-2) 1) Hello World
[](#cb154-3) 2) 
[](#cb154-4) 3) Hi there
[](#cb154-5) 4) How are you
[](#cb154-6) 5) 
[](#cb154-7) 6) Just do-it
[](#cb154-8) 7) Believe it
[](#cb154-9) 8) 
[](#cb154-10) 9) banana
[](#cb154-11)10) papaya
[](#cb154-12)11) mango
[](#cb154-13)12) 
[](#cb154-14)13) Much ado about nothing
[](#cb154-15)14) He he he
[](#cb154-16)15) Adios amigo
```

Here are some examples with `-n` option:

```
[](#cb155-1)# last two lines (input has 15 lines)
[](#cb155-2)$ tail -n2 sample.txt
[](#cb155-3)14) He he he
[](#cb155-4)15) Adios amigo
[](#cb155-5)
[](#cb155-6)# all lines starting from the 11th line
[](#cb155-7)# space between -n and +N is optional
[](#cb155-8)$ tail -n +11 sample.txt
[](#cb155-9)11) mango
[](#cb155-10)12) 
[](#cb155-11)13) Much ado about nothing
[](#cb155-12)14) He he he
[](#cb155-13)15) Adios amigo
```

If you pass multiple input files, each file will be processed separately. By default, the output is nicely formatted with filename headers and empty line separators which you can override with the `-q` (quiet) option.

```
[](#cb156-1)$ tail -n2 fruits.txt sample.txt 
[](#cb156-2)==> fruits.txt <==
[](#cb156-3)papaya
[](#cb156-4)banana
[](#cb156-5)
[](#cb156-6)==> sample.txt <==
[](#cb156-7)14) He he he
[](#cb156-8)15) Adios amigo
```

The `-c` option works similar to the `-n` option, but with bytes instead of lines:

```
[](#cb157-1)# last three bytes
[](#cb157-2)# note that the input doesn't end with a newline character
[](#cb157-3)$ printf 'apple pie' | tail -c3
[](#cb157-4)pie
[](#cb157-5)
[](#cb157-6)# starting from the fifth byte
[](#cb157-7)$ printf 'car\njeep\nbus\n' | tail -c +5
[](#cb157-8)jeep
[](#cb157-9)bus
```

**Further Reading**

*   [wikipedia: File monitoring with tail -f and -F options](https://en.wikipedia.org/wiki/Tail_(Unix)#File_monitoring)
*   [unix.stackexchange: How does the tail -f option work?](https://unix.stackexchange.com/q/18760/109046)
*   [How to deal with output buffering?](https://mywiki.wooledge.org/BashFAQ/009)

## head

By default, `head` displays the first 10 lines of input file(s). If there are less than 10 lines in the input, only those lines will be displayed. You can use the `-n` option to change the number of lines displayed. By using `head -n -N`, you can get all the input lines except the last `N` lines.

```
[](#cb158-1)# first three lines
[](#cb158-2)$ head -n3 sample.txt
[](#cb158-3) 1) Hello World
[](#cb158-4) 2) 
[](#cb158-5) 3) Hi there
[](#cb158-6)
[](#cb158-7)# except the last 11 lines
[](#cb158-8)$ head -n -11 sample.txt
[](#cb158-9) 1) Hello World
[](#cb158-10) 2) 
[](#cb158-11) 3) Hi there
[](#cb158-12) 4) How are you
```

You can select a range of lines by combining both `head` and `tail` commands.

```
[](#cb159-1)# 9th to 11th lines
[](#cb159-2)# same as: tail -n +9 sample.txt | head -n3
[](#cb159-3)$ head -n11 sample.txt | tail -n +9
[](#cb159-4) 9) banana
[](#cb159-5)10) papaya
[](#cb159-6)11) mango
```

If you pass multiple input files, each file will be processed separately. By default, the output is nicely formatted with filename headers and empty line separators which you can override with the `-q` (quiet) option.

```
[](#cb160-1)$ printf '1\n2\n' | head -n1 greeting.txt -
[](#cb160-2)==> greeting.txt <==
[](#cb160-3)Hi there
[](#cb160-4)
[](#cb160-5)==> standard input <==
[](#cb160-6)1
```

The `-c` option works similar to the `-n` option, but with bytes instead of lines:

```
[](#cb161-1)# first three bytes
[](#cb161-2)$ printf 'apple pie' | head -c3
[](#cb161-3)app
[](#cb161-4)
[](#cb161-5)# excluding the last four bytes
[](#cb161-6)$ printf 'car\njeep\nbus\n' | head -c -4
[](#cb161-7)car
[](#cb161-8)jeep
```

## Exercises

> ![info](media/file0.svg) Use [example_files/text_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files/text_files) directory for input files used in the following exercises.

**1)** Which option(s) would you use to get the output shown below?

```
[](#cb162-1)$ printf '\n\n\ndragon\n\n\nunicorn\n\n\n' | cat # ???
[](#cb162-2)
[](#cb162-3)     1  dragon
[](#cb162-4)
[](#cb162-5)     2  unicorn
```

**2)** Pass appropriate arguments to the `cat` command to get the output shown below.

```
[](#cb163-1)$ cat greeting.txt
[](#cb163-2)Hi there
[](#cb163-3)Have a nice day
[](#cb163-4)
[](#cb163-5)$ echo '42 apples and 100 bananas' | cat # ???
[](#cb163-6)42 apples and 100 bananas
[](#cb163-7)Hi there
[](#cb163-8)Have a nice day
```

**3)** Will the two commands shown below produce the same output? If not, why not?

```
[](#cb164-1)$ cat fruits.txt ip.txt | tac
[](#cb164-2)
[](#cb164-3)$ tac fruits.txt ip.txt 
```

**4)** Go through the manual for the `tac` command and use appropriate options and arguments to get the output shown below.

```
[](#cb165-1)$ cat blocks.txt
[](#cb165-2)%=%=
[](#cb165-3)apple
[](#cb165-4)banana
[](#cb165-5)%=%=
[](#cb165-6)brown
[](#cb165-7)green
[](#cb165-8)
[](#cb165-9)# ???
[](#cb165-10)%=%=
[](#cb165-11)brown
[](#cb165-12)green
[](#cb165-13)%=%=
[](#cb165-14)apple
[](#cb165-15)banana
```

**5)** What is the difference between `less -n` and `less -N` options? Do `cat -n` and `less -n` have similar functionality?

**6)** Which command would you use to open another file from within an existing `less` session? And which commands would you use to navigate between previous and next files?

**7)** Use appropriate commands and shell features to get the output shown below.

```
[](#cb166-1)$ printf 'carpet\njeep\nbus\n'
[](#cb166-2)carpet
[](#cb166-3)jeep
[](#cb166-4)bus
[](#cb166-5)
[](#cb166-6)# use the above 'printf' command for input data
[](#cb166-7)$ c=# ???
[](#cb166-8)$ echo "$c"
[](#cb166-9)car
```

**8)** How would you display all the input lines except the first one?

```
[](#cb167-1)$ printf 'apple\nfig\ncarpet\njeep\nbus\n' | # ???
[](#cb167-2)fig
[](#cb167-3)carpet
[](#cb167-4)jeep
[](#cb167-5)bus
```

**9)** Which command(s) would you use to get the output shown below?

```
[](#cb168-1)$ cat fruits.txt
[](#cb168-2)banana
[](#cb168-3)papaya
[](#cb168-4)mango
[](#cb168-5)$ cat blocks.txt
[](#cb168-6)%=%=
[](#cb168-7)apple
[](#cb168-8)banana
[](#cb168-9)%=%=
[](#cb168-10)brown
[](#cb168-11)green
[](#cb168-12)
[](#cb168-13)# ???
[](#cb168-14)banana
[](#cb168-15)papaya
[](#cb168-16)%=%=
[](#cb168-17)apple
```

**10)** Use a combination of `head` and `tail` commands to get the 11th to 14th characters from the given input.

```
[](#cb169-1)$ printf 'apple\nfig\ncarpet\njeep\nbus\n' | # ???
[](#cb169-2)carp
```

**11)** Extract starting six bytes from the input files `table.txt` and `fruits.txt`.

```
[](#cb170-1)# ???
[](#cb170-2)brown banana
```

**12)** Extract last six bytes from the input files `fruits.txt` and `table.txt`.

```
[](#cb171-1)# ???
[](#cb171-2)mango
[](#cb171-3) 3.14
```

# Searching Files and Filenames

This chapter will show how to search file contents based on literal strings or regular expressions. After that, you'll learn how to locate files based on their names and other properties like size, last modified timestamp and so on.

> ![info](media/file0.svg) The [example_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files) directory has the scripts used in this chapter.

## grep

Quoting from [wikipedia](https://en.wikipedia.org/wiki/Grep):

> **`grep`** is a command-line utility for searching plain-text data sets for lines that match a regular expression. Its name comes from the `ed` command `g/re/p` (**g**lobally search a **r**egular **e**xpression and **p**rint), which has the same effect.

The `grep` command has lots and lots of features, so much so that I wrote [a book](https://github.com/learnbyexample/learn_gnugrep_ripgrep) about it. The most common usage is filtering lines from the input using a regular expression (regexp).

### Common options

Commonly used options are shown below. Examples will be discussed in later sections.

*   `--color=auto` highlight the matching portions, filenames, line numbers, etc using colors
*   `-i` ignore case while matching
*   `-v` print only non-matching lines
*   `-n` prefix line numbers for output lines
*   `-c` display only the count of output lines
*   `-l` print only the filenames matching the given expression
*   `-L` print filenames *not* matching the pattern
*   `-w` match pattern only as whole words
*   `-x` match pattern only as whole lines
*   `-F` interpret pattern as a fixed string (i.e. not a regular expression)
*   `-o` print only matching parts
*   `-A N` print matching line and `N` number of lines after the matched line
*   `-B N` print matching line and `N` number of lines before the matched line
*   `-C N` print matching line and `N` number of lines before and after the matched line
*   `-m N` print a maximum of `N` matching lines
*   `-q` no standard output, quit immediately if match found, useful in scripts
*   `-s` suppress error messages, useful in scripts
*   `-r` recursively search all files in the specified input folders (by default searches current directory)
*   `-R` like `-r`, but follows symbolic links as well
*   `-h` do not prefix filename for matching lines (default behavior for single input file)
*   `-H` prefix filename for matching lines (default behavior for multiple input files)

### Literal search

The following examples would all be suited for `-F` option as these do not use regular expressions. `grep` is smart enough to do the right thing in such cases.

```
[](#cb172-1)# lines containing 'an'
[](#cb172-2)$ printf 'apple\nbanana\nmango\nfig\ntango\n' | grep 'an'
[](#cb172-3)banana
[](#cb172-4)mango
[](#cb172-5)tango
[](#cb172-6)
[](#cb172-7)# case insensitive matching
[](#cb172-8)$ printf 'Cat\ncut\ncOnCaT\nfour cats\n' | grep -i 'cat'
[](#cb172-9)Cat
[](#cb172-10)cOnCaT
[](#cb172-11)four cats
[](#cb172-12)
[](#cb172-13)# match only whole words
[](#cb172-14)$ printf 'par value\nheir apparent\ntar-par' | grep -w 'par'
[](#cb172-15)par value
[](#cb172-16)tar-par
[](#cb172-17)
[](#cb172-18)# count empty lines
[](#cb172-19)$ printf 'hi\n\nhello\n\n\n\nbye\n' | grep -cx ''
[](#cb172-20)4
[](#cb172-21)
[](#cb172-22)# matching line and two lines after
[](#cb172-23)$ printf 'red\nblue\ngreen\nbrown\nyellow' | grep -A2 'blue'
[](#cb172-24)blue
[](#cb172-25)green
[](#cb172-26)brown
```

Here's an example with line numbers and matched portions in color:

![example with --color option](media/file8.png)

### Regular Expressions

By default, `grep` treats the search pattern as Basic Regular Expression (BRE)

*   `-G` option can be used to specify explicitly that BRE is needed
*   `-E` option will enable Extended Regular Expression (ERE)
    *   in `GNU grep`, BRE and ERE only differ in how metacharacters are specified, no difference in features
*   `-F` option will cause the search patterns to be treated literally
*   `-P` if available, this option will enable Perl Compatible Regular Expression (PCRE)

The following reference is for **Extended Regular Expressions**.

**Anchors**

*   `^` restricts the match to the start of the string
*   `$` restricts the match to the end of the string
*   `\<` restricts the match to the start of word
*   `\>` restricts the match to the end of word
*   `\b` restricts the match to the start/end of words
*   `\B` matches wherever `\b` doesn't match

**Dot metacharacter and Quantifiers**

*   `.` match any character, including the newline character
*   `?` match `0` or `1` times
*   `*` match `0` or more times
*   `+` match `1` or more times
*   `{m,n}` match `m` to `n` times
*   `{m,}` match at least `m` times
*   `{,n}` match up to `n` times (including `0` times)
*   `{n}` match exactly `n` times

**Character classes**

*   `[set123]` match any of these characters once
*   `[^set123]` match except any of these characters once
*   `[3-7AM-X]` range of characters from `3` to `7`, `A`, another range from `M` to `X`
*   `\w` similar to `[a-zA-Z0-9_]` for matching word characters
*   `\s` similar to `[ \t\n\r\f\v]` for matching whitespace characters
*   `\W` match non-word characters
*   `\S` match non-whitespace characters
*   `[[:digit:]]` similar to `[0-9]`
*   `[[:alnum:]_]` similar to `\w`
    *   see [grep manual](https://www.gnu.org/software/grep/manual/grep.html#Character-Classes-and-Bracket-Expressions) for full list

**Alternation and Grouping**

*   `pat1|pat2|pat3` match `pat1` or `pat2` or `pat3`
*   `()` group patterns, `a(b|c)d` is same as `abd|acd`
    *   also serves as a capture group
*   `\N` backreference, gives matched portion of `N`th capture group
    *   `\1` backreference to the first capture group
    *   `\2` backreference to the second capture group and so on up to `\9`

Quoting from the manual for BRE vs ERE differences:

> In basic regular expressions the meta-characters `?`, `+`, `{`, `|`, `(`, and `)` lose their special meaning; instead use the backslashed versions `\?`, `\+`, `\{`, `\|`, `\(`, and `\)`.

### Regexp examples

```
[](#cb173-1)# lines ending with 'ar'
[](#cb173-2)$ printf 'spared no one\npar\nspar\ndare' | grep 'ar$'
[](#cb173-3)par
[](#cb173-4)spar
[](#cb173-5)
[](#cb173-6)# extract 'part' or 'parrot' or 'parent' case insensitively
[](#cb173-7)$ echo 'par apartment PARROT parent' | grep -ioE 'par(en|ro)?t'
[](#cb173-8)part
[](#cb173-9)PARROT
[](#cb173-10)parent
[](#cb173-11)
[](#cb173-12)# extract quoted text
[](#cb173-13)$ echo 'I like "mango" and "guava"' | grep -oE '"[^"]+"'
[](#cb173-14)"mango"
[](#cb173-15)"guava"
[](#cb173-16)
[](#cb173-17)# 8 character lines having same 3 lowercase letters at start and end
[](#cb173-18)$ grep -xE '([a-z]{3})..\1' /usr/share/dict/words
[](#cb173-19)mesdames
[](#cb173-20)respires
[](#cb173-21)restores
[](#cb173-22)testates
```

### Line comparisons between files

The `-f` and `-x` options can be combined to get common lines between two files or the difference when `-v` is used as well. Add `-F` if you want to treat the search strings literally (recall that regexp is the default).

```
[](#cb174-1)# change to the 'scripts' directory and source the 'grep.sh' script
[](#cb174-2)$ source grep.sh
[](#cb174-3)
[](#cb174-4)# common lines between two files
[](#cb174-5)$ grep -Fxf colors_1 colors_2
[](#cb174-6)yellow
[](#cb174-7)
[](#cb174-8)# lines present in colors_2 but not in colors_1
[](#cb174-9)$ grep -Fvxf colors_1 colors_2
[](#cb174-10)blue
[](#cb174-11)black
[](#cb174-12)dark green
[](#cb174-13)
[](#cb174-14)# lines present in colors_1 but not in colors_2
[](#cb174-15)$ grep -Fvxf colors_2 colors_1
[](#cb174-16)teal
[](#cb174-17)light blue
[](#cb174-18)brown
```

### Perl Compatible Regular Expression

PCRE has many advanced features compared to BRE/ERE. Here are some examples:

```
[](#cb175-1)# numbers >= 100, uses possessive quantifiers
[](#cb175-2)$ echo '0501 035 154 12 26 98234' | grep -oP '0*+\d{3,}'
[](#cb175-3)0501
[](#cb175-4)154
[](#cb175-5)98234
[](#cb175-6)
[](#cb175-7)# extract digits only if preceded by =
[](#cb175-8)$ echo '100 apple=42, fig=314 red:255' | grep -oP '=\K\d+'
[](#cb175-9)42
[](#cb175-10)314
[](#cb175-11)
[](#cb175-12)# all digits and optional hyphen combo from the start of the line
[](#cb175-13)$ echo '123-87-593 42 fig 314-12-111' | grep -oP '\G\d+-?'
[](#cb175-14)123-
[](#cb175-15)87-
[](#cb175-16)593
[](#cb175-17)
[](#cb175-18)# all whole words except 'bat' and 'map'
[](#cb175-19)$ echo 'car2 bat cod map combat' | grep -oP '\b(bat|map)\b(*SKIP)(*F)|\w+'
[](#cb175-20)car2
[](#cb175-21)cod
[](#cb175-22)combat
```

See `man pcrepattern` or [PCRE online manual](https://www.pcre.org/original/doc/html/pcrepattern.html) for documentation.

### Recursive search

You can use the `-r` option to search recursively within the specified directories. By default, the current directory will be searched. Use `-R` if you want symbolic links found within the input directories to be followed as well. You do not need the `-R` option for specifying symbolic links as arguments.

Here are some basic examples. Recursive search will work as if `-H` option was specified as well, even if only one file was matched. Also, hidden files are included by default.

```
[](#cb176-1)# change to the 'scripts' directory and source the 'grep.sh' script
[](#cb176-2)$ source grep.sh
[](#cb176-3)$ ls -AF
[](#cb176-4)backups/  colors_1  colors_2  .hidden  projects/
[](#cb176-5)
[](#cb176-6)# recursively search in the 'backups' directory
[](#cb176-7)$ grep -r 'clear' backups
[](#cb176-8)backups/dot_files/.bash_aliases:alias c=clear
[](#cb176-9)# add -h option to prevent filename prefix in the output
[](#cb176-10)$ grep -rh 'clear' backups
[](#cb176-11)alias c=clear
[](#cb176-12)
[](#cb176-13)# by default, the current directory is used for recursive search
[](#cb176-14)$ grep -rl 'clear'
[](#cb176-15).hidden
[](#cb176-16)backups/dot_files/.bash_aliases
```

You can further prune the files to be searched using the *include/exclude* options. Note that these options will work even if recursive search is not active.

| Option | Description |
| --- | --- |
| --include=GLOB | search only files that match GLOB |
| --exclude=GLOB | skip files that match GLOB |
| --exclude-from=FILE | skip files that match any file pattern from FILE |
| --exclude-dir=GLOB | skip directories that match GLOB |

```
[](#cb177-1)# default recursive search
[](#cb177-2)$ grep -r 'Hello'
[](#cb177-3)projects/python/hello.py:print("Hello, Python!")
[](#cb177-4)projects/shell/hello.sh:echo "Hello, Bash!"
[](#cb177-5)
[](#cb177-6)# limit the search to only filenames ending with '.py'
[](#cb177-7)$ grep -r --include='*.py' 'Hello'
[](#cb177-8)projects/python/hello.py:print("Hello, Python!")
[](#cb177-9)
[](#cb177-10)# alternatively, you can use shell globs instead of recursive+include/exclude
[](#cb177-11)$ shopt -s globstar
[](#cb177-12)$ grep -H 'Hello' **/*.py
[](#cb177-13)projects/python/hello.py:print("Hello, Python!")
```

> ![info](media/file0.svg) [ripgrep](https://github.com/BurntSushi/ripgrep) is a recommended alternative to `GNU grep` with a highly optimized regexp engine, parallel search, ignoring files based on `.gitignore` and so on.

### grep and xargs

You can use the shell `|` operator to pass the output of a command as input to another command. Suppose a command gives you a list of filenames and you want to pass this list as input *arguments* to another command, what would you do? One solution is to use the `xargs` command. Here's a basic example (assuming filenames won't conflict with shell metacharacters):

```
[](#cb178-1)# an example command producing a list of filenames
[](#cb178-2)$ grep -rl 'clear'
[](#cb178-3).hidden
[](#cb178-4)backups/dot_files/.bash_aliases
[](#cb178-5)
[](#cb178-6)# same as: head -n1 .hidden backups/dot_files/.bash_aliases
[](#cb178-7)$ grep -rl 'clear' | xargs head -n1
[](#cb178-8)==> .hidden <==
[](#cb178-9)ghost
[](#cb178-10)
[](#cb178-11)==> backups/dot_files/.bash_aliases <==
[](#cb178-12)alias p=pwd
```

Characters like space, newline, semicolon, etc are special to the shell. So, filenames containing these characters have to be properly quoted. Or, where applicable, you can use a list of filenames separated by the ASCII NUL character (since filenames cannot have the NUL character). You can use `grep -Z` to separate the output with NUL and `xargs -0` to treat the input as NUL separated. Here's an example:

```
[](#cb179-1)# consider this command that generates a list of filenames
[](#cb179-2)$ grep -rl 'blue'
[](#cb179-3).hidden
[](#cb179-4)colors_1
[](#cb179-5)colors_2
[](#cb179-6)backups/color list.txt
[](#cb179-7)
[](#cb179-8)# example to show issues due to filenames containing shell metacharacters
[](#cb179-9)# 'backups/color list.txt' is treated as two different files
[](#cb179-10)$ grep -rl 'blue' | xargs grep -l 'teal'
[](#cb179-11)colors_2
[](#cb179-12)grep: backups/color: No such file or directory
[](#cb179-13)grep: list.txt: No such file or directory
[](#cb179-14)
[](#cb179-15)# use 'grep -Z' + 'xargs -0' combo for a robust solution
[](#cb179-16)# match files containing both 'blue' and 'teal'
[](#cb179-17)$ grep -rlZ 'blue' | xargs -0 grep -l 'teal'
[](#cb179-18)colors_1
```

Note that the command passed to `xargs` doesn't accept custom made aliases and functions. So, if you had aliased `grep` to `grep --color=auto`, don't be surprised if the output isn't colorized. See [unix.stackexchange: have xargs use alias instead of binary](https://unix.stackexchange.com/q/141367/109046) for details and workarounds.

> ![info](media/file0.svg) You can use `xargs -r` to avoid running the command when the filename list doesn't have any non-blank character (i.e. when the list is empty).
> 
> ```
> [](#cb180-1)# there's no file containing 'violet'
> [](#cb180-2)# so, xargs doesn't get any filename, but grep is still run
> [](#cb180-3)$ grep -rlZ 'violet' | xargs -0 grep -L 'brown'
> [](#cb180-4)(standard input)
> [](#cb180-5)
> [](#cb180-6)# using -r option avoids running the command in such cases
> [](#cb180-7)$ grep -rlZ 'violet' | xargs -r0 grep -L 'brown'
> ```

> ![warning](media/file7.svg) ![warning](media/file7.svg) Do not use `xargs -P` to combine the output of parallel runs, as you are likely to get a mangled result. The [parallel](https://www.gnu.org/software/parallel/) command would be a better option. See [unix.stackexchange: xargs vs parallel](https://unix.stackexchange.com/q/104778/109046) for more details. See also [unix.stackexchange: when to use xargs](https://unix.stackexchange.com/q/24954/109046).

### Further Reading

*   My ebook [GNU GREP and RIPGREP](https://github.com/learnbyexample/learn_gnugrep_ripgrep)
    *   See also my blog post [GNU BRE/ERE cheatsheet](https://learnbyexample.github.io/gnu-bre-ere-cheatsheet/)
*   [Why GNU grep is fast](https://lists.freebsd.org/pipermail/freebsd-current/2010-August/019310.html)
*   [unix.stackexchange: grep -r vs find+grep](https://unix.stackexchange.com/q/131535/109046)

## find

The `find` command has comprehensive features to filter files and directories based on their name, size, timestamp and so on. And more importantly, `find` helps you to perform actions on such filtered files.

### Filenames

By default, you'll get every entry (including hidden ones) in the current directory and sub-directories when you use `find` without any options or paths. To search within specific path(s), they should be immediately mentioned after `find`, i.e. before any options.

```
[](#cb181-1)# change to the 'scripts' directory and source the 'find.sh' script
[](#cb181-2)$ source find.sh
[](#cb181-3)$ ls -F
[](#cb181-4)backups/    hello_world.py*  ip.txt     report.log  todos/
[](#cb181-5)errors.log  hi.sh*           projects/  scripts@
[](#cb181-6)
[](#cb181-7)$ cd projects
[](#cb181-8)# same as: find .
[](#cb181-9)$ find
[](#cb181-10).
[](#cb181-11)./.venv
[](#cb181-12)./tictactoe
[](#cb181-13)./tictactoe/game.py
[](#cb181-14)./calculator
[](#cb181-15)./calculator/calc.sh
[](#cb181-16)
[](#cb181-17)$ cd ..
[](#cb181-18)$ find todos
[](#cb181-19)todos
[](#cb181-20)todos/books.txt
[](#cb181-21)todos/TRIP.txt
[](#cb181-22)todos/wow.txt
```

> ![info](media/file0.svg) Note that symbolic links won't be followed by default. You can use `-L` option for such cases.

To match filenames based on a particular criteria, you can use wildcards or regular expressions. For wildcards, you can use `-name` or the case-insensitive version `-iname`. These will match only the basename, so you'll get a warning if you use `/` as part of the pattern. You can use `-path` and `-ipath` if you need to include `/` as well in the pattern. Unlike `grep`, the glob pattern is matched against the entire basename (as there are no start/end anchors in globs).

```
[](#cb182-1)# filenames ending with '.log'
[](#cb182-2)# 'find .' indicates current working directory (CWD) as the path to search
[](#cb182-3)$ find . -name '*.log'
[](#cb182-4)./report.log
[](#cb182-5)./backups/aug.log
[](#cb182-6)./backups/jan.log
[](#cb182-7)./errors.log
[](#cb182-8)
[](#cb182-9)# match filenames containing 'ip' case-insensitively
[](#cb182-10)# note the use of '*' on both sides of 'ip' to match the whole filename
[](#cb182-11)# . is optional when CWD is the only path to search
[](#cb182-12)$ find -iname '*ip*'
[](#cb182-13)./todos/TRIP.txt
[](#cb182-14)./scripts
[](#cb182-15)./ip.txt
[](#cb182-16)
[](#cb182-17)# names containing 'k' within 'backups' and 'todos' directories
[](#cb182-18)$ find backups todos -name '*k*'
[](#cb182-19)backups
[](#cb182-20)backups/bookmarks.html
[](#cb182-21)todos/books.txt
```

You can use the `-not` (or `!`) operator to invert the matching condition:

```
[](#cb183-1)# same as: find todos ! -name '*[A-Z]*'
[](#cb183-2)$ find todos -not -name '*[A-Z]*'
[](#cb183-3)todos
[](#cb183-4)todos/books.txt
[](#cb183-5)todos/wow.txt
```

You can use `-regex` and `-iregex` (case-insensitive) to match filenames based on regular expressions. In this case, the pattern will match the entire path, so use of `/` is possible without needing to use special options. The default regexp flavor is `emacs` which you can change by using the `-regextype` option.

```
[](#cb184-1)# filename containing only uppercase alphabets and file extension is '.txt'
[](#cb184-2)# note the use of '.*/' to match the entire file path
[](#cb184-3)$ find -regex '.*/[A-Z]+\.txt'
[](#cb184-4)./todos/TRIP.txt
[](#cb184-5)
[](#cb184-6)# here 'egrep' flavor is being used
[](#cb184-7)# filename starting and ending with the same word character (case-insensitive)
[](#cb184-8)# and file extension is '.txt'
[](#cb184-9)$ find -regextype egrep -iregex '.*/(\w).*\1\.txt'
[](#cb184-10)./todos/wow.txt
```

### File type

The `-type` option helps to filter files based on their types like regular file, directory, symbolic link, etc.

```
[](#cb185-1)# regular files
[](#cb185-2)$ find projects -type f
[](#cb185-3)projects/tictactoe/game.py
[](#cb185-4)projects/calculator/calc.sh
[](#cb185-5)
[](#cb185-6)# regular files that are hidden as well
[](#cb185-7)$ find -type f -name '.*'
[](#cb185-8)./.hidden
[](#cb185-9)./backups/dot_files/.bashrc
[](#cb185-10)./backups/dot_files/.inputrc
[](#cb185-11)./backups/dot_files/.vimrc
[](#cb185-12)
[](#cb185-13)# directories
[](#cb185-14)$ find projects -type d
[](#cb185-15)projects
[](#cb185-16)projects/.venv
[](#cb185-17)projects/tictactoe
[](#cb185-18)projects/calculator
[](#cb185-19)
[](#cb185-20)# symbolic links
[](#cb185-21)$ find -type l
[](#cb185-22)./scripts
```

> ![info](media/file0.svg) You can use `,` to separate multiple file types. For example, `-type f,l` will match both regular files and symbolic links.

### Depth

The path being searched is considered as depth `0`, files within the search path are at depth `1`, files within a sub-directory are at depth `2` and so on. Note that these global options should be specified before other kind of options like `-type`, `-name`, etc.

`-maxdepth` option restricts the search to the specified maximum depth:

```
[](#cb186-1)# non-hidden regular files only in the current directory
[](#cb186-2)# sub-directories will not be checked
[](#cb186-3)# -not -name '.*' can also be used instead of -name '[^.]*'
[](#cb186-4)$ find -maxdepth 1 -type f -name '[^.]*'
[](#cb186-5)./report.log
[](#cb186-6)./hi.sh
[](#cb186-7)./errors.log
[](#cb186-8)./hello_world.py
[](#cb186-9)./ip.txt
```

`-mindepth` option specifies the minimum depth:

```
[](#cb187-1)# recall that path being searched is considered as depth 0
[](#cb187-2)# and contents within the search path are at depth 1
[](#cb187-3)$ find -mindepth 1 -maxdepth 1 -type d
[](#cb187-4)./projects
[](#cb187-5)./todos
[](#cb187-6)./backups
[](#cb187-7)
[](#cb187-8)$ find -mindepth 3 -type f
[](#cb187-9)./projects/tictactoe/game.py
[](#cb187-10)./projects/calculator/calc.sh
[](#cb187-11)./backups/dot_files/.bashrc
[](#cb187-12)./backups/dot_files/.inputrc
[](#cb187-13)./backups/dot_files/.vimrc
```

### Age

Consider the following file properties:

*   `a` accessed
*   `c` status changed
*   `m` modified

The above prefixes need to be combined with `time` (based on 24 hour periods) or `min` (based on minutes) options. For example, `-mtime` (24 hour) option checks for last modified timestamp and `-amin` (minute) checks for last accessed timestamp. These options accept a number (integer or fractional) argument, that can be further prefixed by `+` or `-` symbols. Here are some examples:

```
[](#cb188-1)# modified less than 24 hours ago
[](#cb188-2)$ find -maxdepth 1 -type f -mtime 0
[](#cb188-3)./hello_world.py
[](#cb188-4)./ip.txt
[](#cb188-5)
[](#cb188-6)# accessed between 24 to 48 hours ago
[](#cb188-7)$ find -maxdepth 1 -type f -atime 1
[](#cb188-8)./ip.txt
[](#cb188-9)# accessed within the last 24 hours
[](#cb188-10)$ find -maxdepth 1 -type f -atime -1
[](#cb188-11)./hello_world.py
[](#cb188-12)# accessed within the last 48 hours
[](#cb188-13)$ find -maxdepth 1 -type f -atime -2
[](#cb188-14)./hello_world.py
[](#cb188-15)./ip.txt
[](#cb188-16)
[](#cb188-17)# modified more than 20 days back
[](#cb188-18)$ find -maxdepth 1 -type f -mtime +20
[](#cb188-19)./.hidden
[](#cb188-20)./report.log
[](#cb188-21)./errors.log
```

> ![info](media/file0.svg) The `-daystart` qualifier will measure time only from the beginning of the day. For example, `-daystart -mtime 1` will check the files that were modified yesterday.

### Size

You can use the `-size` option to filter based on file sizes. By default, the number argument will be considered as 512-byte blocks. You can use the suffix `c` to specify the size in bytes. The suffixes `k` (kilo), `M` (mega) and `G` (giga) are calculated in powers of 1024.

```
[](#cb189-1)# greater than 10 * 1024 bytes
[](#cb189-2)$ find -type f -size +10k
[](#cb189-3)./report.log
[](#cb189-4)./errors.log
[](#cb189-5)
[](#cb189-6)# greater than 9 bytes and less than 50 bytes
[](#cb189-7)$ find -type f -size +9c -size -50c
[](#cb189-8)./hi.sh
[](#cb189-9)./hello_world.py
[](#cb189-10)./ip.txt
[](#cb189-11)
[](#cb189-12)# exactly 10 bytes
[](#cb189-13)$ find -type f -size 10c
[](#cb189-14)./ip.txt
```

> ![info](media/file0.svg) You can also use the `-empty` option instead of `-size 0`.

### Acting on matched files

The `-exec` option helps you to pass the matching files to another command. You can choose to execute the command once for every file (by using `\;`) or just once for all the matching files (by using `+`). However, if the number of files are too many, `find` will use more command invocations as necessary. The `;` character is escaped since it is a shell metacharacter (you can also quote it as an alternative to escaping).

You need to use `{}` to represent the file(s) passed as argument(s) to the command being executed. Here are some examples:

```
[](#cb190-1)# count the number of characters for each matching file
[](#cb190-2)# wc is called separately for each matching file
[](#cb190-3)$ find -type f -size +9k -exec wc -c {} \;
[](#cb190-4)1234567 ./report.log
[](#cb190-5)54321 ./errors.log
[](#cb190-6)
[](#cb190-7)# here, both matching files are passed together to the wc command
[](#cb190-8)$ find -type f -size +9k -exec wc -c {} +
[](#cb190-9)1234567 ./report.log
[](#cb190-10)  54321 ./errors.log
[](#cb190-11)1288888 total
```

As mentioned in the [Managing Files and Directories](#ch004.xhtml_managing-files-and-directories) chapter, the `-t` option for `cp` and `mv` commands will help you specify the target directory before the source files. Here's an example:

```
[](#cb191-1)$ mkdir rc_files
[](#cb191-2)$ find backups/dot_files -type f -exec cp -t rc_files {} +
[](#cb191-3)
[](#cb191-4)$ find rc_files -type f
[](#cb191-5)rc_files/.bashrc
[](#cb191-6)rc_files/.inputrc
[](#cb191-7)rc_files/.vimrc
[](#cb191-8)
[](#cb191-9)$ rm -r rc_files
```

> ![info](media/file0.svg) You can use the `-delete` option instead of calling the `rm` command to delete the matching files. However, it cannot remove non-empty directories and there are other gotchas to be considered. See the manual for more details.

### Multiple criteria

You can specify multiple matching criteria such as `-name`, `-size`, `-mtime`, etc. You can use operators between them and group them within `\(` and `\)` to construct complex expressions.

*   `-a` or `-and` or absence of an operator means both expressions have to be satisfied
    *   second expression won't be evaluated if the first one is false
*   `-o` or `-or` means either of the expressions have to be satisfied
    *   second expression won't be evaluated if the first one is true
*   `-not` inverts the result of the expression
    *   you can also use `!` but that might need escaping or quoting depending on the shell

```
[](#cb192-1)# names containing both 'x' and 'ip' in any order (case-insensitive)
[](#cb192-2)$ find -iname '*x*' -iname '*ip*'
[](#cb192-3)./todos/TRIP.txt
[](#cb192-4)./ip.txt
[](#cb192-5)
[](#cb192-6)# names containing 'sc' or size greater than 10k
[](#cb192-7)$ find -name '*sc*' -or -size +10k
[](#cb192-8)./report.log
[](#cb192-9)./scripts
[](#cb192-10)./errors.log
[](#cb192-11)
[](#cb192-12)# except filenames containing 'o' or 'r' or 'txt'
[](#cb192-13)$ find -type f -not \( -name '*[or]*' -or -name '*txt*' \)
[](#cb192-14)./projects/tictactoe/game.py
[](#cb192-15)./projects/calculator/calc.sh
[](#cb192-16)./.hidden
[](#cb192-17)./hi.sh
```

### Prune

The `-prune` option is helpful when you want to prevent `find` from descending into specific directories. By default, `find` will traverse all the files even if the given conditions will result in throwing away those results from the output. So, using `-prune` not only helps in speeding up the process, it could also help in cases where trying to access a file within the exclusion path would've resulted in an error.

```
[](#cb193-1)# regular files ending with '.log'
[](#cb193-2)$ find -type f -name '*.log'
[](#cb193-3)./report.log
[](#cb193-4)./backups/aug.log
[](#cb193-5)./backups/jan.log
[](#cb193-6)./errors.log
[](#cb193-7)
[](#cb193-8)# exclude the 'backups' directory
[](#cb193-9)# note the use of -path when '/' is needed in the pattern
[](#cb193-10)$ find -type f -not -path './backups/*' -prune -name '*.log'
[](#cb193-11)./report.log
[](#cb193-12)./errors.log
```

Using `-not -path '*/.git/*' -prune` can be handy when dealing with Git based version control projects.

### find and xargs

Similar to `grep -Z` and `xargs -0` combination seen earlier, you can use `find -print0` and `xargs -0` combination. The `-exec` option is sufficient for most use cases, but `xargs -P` (or the [parallel](https://www.gnu.org/software/parallel/) command) can be handy if you need parallel execution for performance reasons.

Here's an example of passing filtered files to `sed` (**s**tream **ed**itor, will be discussed in the [Multipurpose Text Processing Tools](#ch010.xhtml_multipurpose-text-processing-tools) chapter):

```
[](#cb194-1)$ find -name '*.log'
[](#cb194-2)./report.log
[](#cb194-3)./backups/aug.log
[](#cb194-4)./backups/jan.log
[](#cb194-5)./errors.log
[](#cb194-6)
[](#cb194-7)# for the filtered files, replace all occurrences of 'apple' with 'fig'
[](#cb194-8)# 'sed -i' will edit the files inplace, so no output on the terminal
[](#cb194-9)$ find -name '*.log' -print0 | xargs -r0 -n2 -P2 sed -i 's/apple/fig/g'
```

In the above example, `-P2` is used to allow `xargs` to run two processes at a time (default is one process). You can use `-P0` to allow `xargs` to launch as many processes as possible. The `-n2` option is used to limit the number of file arguments passed to each `sed` call to `2`, otherwise `xargs` is likely to pass as many arguments as possible and thus reduce/negate the effect of parallelism. Note that the values used for `-n` and `-P` in the above illustration are just random examples, you'll have to fine tune them for your particular use case.

### Further Reading

*   [mywiki.wooledge: using find](https://mywiki.wooledge.org/UsingFind)
*   [unix.stackexchange: find and tar example](https://unix.stackexchange.com/q/282762/109046)
*   [unix.stackexchange: Why is looping over find's output bad practice?](https://unix.stackexchange.com/q/321697/109046)

## locate

`locate` is a faster alternative to the `find` command for searching files by name. It is based on a database, which gets updated by a [cron](https://en.wikipedia.org/wiki/Cron) job. So, newer files may be not present in results unless you update the database. Use this command if it is available in your distro (for example, `sudo apt install mlocate` on Debian-like systems) and you remember some part of filename. Very useful if you have to search the entire filesystem in which case `find` command will take a very long time compared to `locate`.

Here are some examples:

*   `locate 'power'` print path of filenames containing `power` in the whole filesystem
    *   implicitly, `locate` would change the string to `*power*` as no globbing characters are present in the string specified
*   `locate -b '\power.log'` print path matching the string `power.log` exactly at the end of the path
    *   `/home/learnbyexample/power.log` matches
    *   `/home/learnbyexample/lowpower.log'` will not match since there are other characters at the start of the filename
    *   use of `\` prevents the search string from implicitly being replaced by `*power.log*`
*   `locate -b '\proj_adder'` the `-b` option is also handy to print only the matching directory name, otherwise every file under that folder would also be displayed

> ![info](media/file0.svg) See also [unix.stackexchange: pros and cons of find and locate](https://unix.stackexchange.com/q/60205/109046).

## Exercises

> ![info](media/file0.svg) For `grep` exercises, use [example_files/text_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files/text_files) directory for input files, unless otherwise specified.

> ![info](media/file0.svg) For `find` exercises, use the `find.sh` script, unless otherwise specified.

**1)** Display lines containing `an` from the input files `blocks.txt`, `ip.txt` and `uniform.txt`. Show the results with and without filename prefix.

```
[](#cb195-1)# ???
[](#cb195-2)blocks.txt:banana
[](#cb195-3)ip.txt:light orange
[](#cb195-4)uniform.txt:mango
[](#cb195-5)
[](#cb195-6)# ???
[](#cb195-7)banana
[](#cb195-8)light orange
[](#cb195-9)mango
```

**2)** Display lines containing the whole word `he` from the `sample.txt` input file.

```
[](#cb196-1)# ???
[](#cb196-2)14) He he he
```

**3)** Match only whole lines containing `car` irrespective of case. The matching lines should be displayed with line number prefix as well.

```
[](#cb197-1)$ printf 'car\nscared\ntar car par\nCar\n' | grep # ???
[](#cb197-2)1:car
[](#cb197-3)4:Car
```

**4)** Display all lines from `purchases.txt` except those that contain `tea`.

```
[](#cb198-1)# ???
[](#cb198-2)coffee
[](#cb198-3)washing powder
[](#cb198-4)coffee
[](#cb198-5)toothpaste
[](#cb198-6)soap
```

**5)** Display all lines from `sample.txt` that contain `do` but not `it`.

```
[](#cb199-1)# ???
[](#cb199-2)13) Much ado about nothing
```

**6)** For the input file `sample.txt`, filter lines containing `do` and also display the line that comes after such a matching line.

```
[](#cb200-1)# ???
[](#cb200-2) 6) Just do-it
[](#cb200-3) 7) Believe it
[](#cb200-4)--
[](#cb200-5)13) Much ado about nothing
[](#cb200-6)14) He he he
```

**7)** For the input file `sample.txt`, filter lines containing `are` or `he` as whole words as well as the line that comes before such a matching line. Go through `info grep` or the [online manual](https://www.gnu.org/software/grep/manual/grep.html) and use appropriate options such that there's no separator between the groups of matching lines in the output.

```
[](#cb201-1)# ???
[](#cb201-2) 3) Hi there
[](#cb201-3) 4) How are you
[](#cb201-4)13) Much ado about nothing
[](#cb201-5)14) He he he
```

**8)** Extract all pairs of `()` with/without text inside them, provided they do not contain `()` characters inside.

```
[](#cb202-1)$ echo 'I got (12) apples' | grep # ???
[](#cb202-2)(12)
[](#cb202-3)
[](#cb202-4)$ echo '((2 +3)*5)=25 and (4.3/2*()' | grep # ???
[](#cb202-5)(2 +3)
[](#cb202-6)()
```

**9)** For the given input, match all lines that start with `den` or end with `ly`.

```
[](#cb203-1)$ lines='reply\n1 dentist\n2 lonely\neden\nfly away\ndent\n'
[](#cb203-2)
[](#cb203-3)$ printf '%b' "$lines" | grep # ???
[](#cb203-4)reply
[](#cb203-5)2 lonely
[](#cb203-6)dent
```

**10)** Extract words starting with `s` and containing both `e` and `t` in any order.

```
[](#cb204-1)$ words='sequoia subtle exhibit sets tests sit store_2'
[](#cb204-2)
[](#cb204-3)$ echo "$words" | grep # ???
[](#cb204-4)subtle
[](#cb204-5)sets
[](#cb204-6)store_2
```

**11)** Extract all whole words having the same first and last word character.

```
[](#cb205-1)$ echo 'oreo not a _oh_ pip roar took 22' | grep # ???
[](#cb205-2)oreo
[](#cb205-3)a
[](#cb205-4)_oh_
[](#cb205-5)pip
[](#cb205-6)roar
[](#cb205-7)22
```

**12)** Match all input lines containing `*[5]` literally.

```
[](#cb206-1)$ printf '4*5]\n(9-2)*[5]\n[5]*3\nr*[5\n' | grep # ???
[](#cb206-2)(9-2)*[5]
```

**13)** Match whole lines that start with `hand` and immediately followed by `s` or `y` or `le` or no further character.

```
[](#cb207-1)$ lines='handed\nhand\nhandy\nunhand\nhands\nhandle\nhandss\n'
[](#cb207-2)
[](#cb207-3)$ printf '%b' "$lines" | grep # ???
[](#cb207-4)hand
[](#cb207-5)handy
[](#cb207-6)hands
[](#cb207-7)handle
```

**14)** Input lines have three or more fields separated by a `,` delimiter. Extract second field to second last field. In other words, extract fields other than first and last.

```
[](#cb208-1)$ printf 'apple,fig,cherry\ncat,dog,bat\n' | grep # ???
[](#cb208-2)fig
[](#cb208-3)dog
[](#cb208-4)
[](#cb208-5)$ echo 'dragon,42,unicorn,3.14,shapeshifter\n' | grep # ???
[](#cb208-6)42,unicorn,3.14
```

**15)** Recursively search for files containing `ello`.

```
[](#cb209-1)# change to the 'scripts' directory and source the 'grep.sh' script
[](#cb209-2)$ source grep.sh
[](#cb209-3)
[](#cb209-4)# ???
[](#cb209-5)projects/python/hello.py
[](#cb209-6)projects/shell/hello.sh
[](#cb209-7)colors_1
[](#cb209-8)colors_2
```

**16)** Search for files containing `blue` recursively, but do not search within the `backups` directory.

```
[](#cb210-1)# change to the 'scripts' directory and source the 'grep.sh' script
[](#cb210-2)$ source grep.sh
[](#cb210-3)
[](#cb210-4)# ???
[](#cb210-5).hidden
[](#cb210-6)colors_1
[](#cb210-7)colors_2
```

**17)** Search for files containing `blue` recursively, but not if the file also contains `teal`.

```
[](#cb211-1)# change to the 'scripts' directory and source the 'grep.sh' script
[](#cb211-2)$ source grep.sh
[](#cb211-3)
[](#cb211-4)# ???
[](#cb211-5).hidden
[](#cb211-6)colors_2
[](#cb211-7)backups/color list.txt
```

**18)** Find all regular files within the `backups` directory.

```
[](#cb212-1)# change to the 'scripts' directory and source the 'find.sh' script
[](#cb212-2)$ source find.sh
[](#cb212-3)
[](#cb212-4)# ???
[](#cb212-5)backups/dot_files/.bashrc
[](#cb212-6)backups/dot_files/.inputrc
[](#cb212-7)backups/dot_files/.vimrc
[](#cb212-8)backups/aug.log
[](#cb212-9)backups/bookmarks.html
[](#cb212-10)backups/jan.log
```

**19)** Find all regular files whose extension starts with `p` or `s` or `v`.

```
[](#cb213-1)# ???
[](#cb213-2)./projects/tictactoe/game.py
[](#cb213-3)./projects/calculator/calc.sh
[](#cb213-4)./hi.sh
[](#cb213-5)./backups/dot_files/.vimrc
[](#cb213-6)./hello_world.py
```

**20)** Find all regular files whose name do *not* have the lower case alphabets `g` to `l`.

```
[](#cb214-1)# ???
[](#cb214-2)./todos/TRIP.txt
[](#cb214-3)./todos/wow.txt
```

**21)** Find all regular files whose path has at least one directory name starting with `p` or `d`.

```
[](#cb215-1)# ???
[](#cb215-2)./projects/tictactoe/game.py
[](#cb215-3)./projects/calculator/calc.sh
[](#cb215-4)./backups/dot_files/.bashrc
[](#cb215-5)./backups/dot_files/.inputrc
[](#cb215-6)./backups/dot_files/.vimrc
```

**22)** Find all directories whose name contains `b` or `d`.

```
[](#cb216-1)# ???
[](#cb216-2)./todos
[](#cb216-3)./backups
[](#cb216-4)./backups/dot_files
```

**23)** Find all hidden directories.

```
[](#cb217-1)# ???
[](#cb217-2)./projects/.venv
```

**24)** Find all regular files at exact depth of `2`.

```
[](#cb218-1)# ???
[](#cb218-2)./todos/books.txt
[](#cb218-3)./todos/TRIP.txt
[](#cb218-4)./todos/wow.txt
[](#cb218-5)./backups/aug.log
[](#cb218-6)./backups/bookmarks.html
[](#cb218-7)./backups/jan.log
```

**25)** What's the difference between `find -mtime` and `find -atime`? And, what is the time period these options work with?

**26)** Find all empty regular files.

```
[](#cb219-1)# ???
[](#cb219-2)./projects/tictactoe/game.py
[](#cb219-3)./projects/calculator/calc.sh
[](#cb219-4)./todos/books.txt
[](#cb219-5)./todos/TRIP.txt
[](#cb219-6)./todos/wow.txt
[](#cb219-7)./backups/dot_files/.bashrc
[](#cb219-8)./backups/dot_files/.inputrc
[](#cb219-9)./backups/dot_files/.vimrc
[](#cb219-10)./backups/aug.log
[](#cb219-11)./backups/bookmarks.html
[](#cb219-12)./backups/jan.log
```

**27)** Create a directory named `filtered_files`. Then, copy all regular files that are greater than `1` byte in size but whose name don't end with `.log` to this directory.

```
[](#cb220-1)# ???
[](#cb220-2)$ ls -A filtered_files
[](#cb220-3)hello_world.py  .hidden  hi.sh  ip.txt
```

**28)** Find all hidden files, but not if they are part of the `filtered_files` directory created earlier.

```
[](#cb221-1)# ???
[](#cb221-2)./.hidden
[](#cb221-3)./backups/dot_files/.bashrc
[](#cb221-4)./backups/dot_files/.inputrc
[](#cb221-5)./backups/dot_files/.vimrc
```

**29)** Delete the `filtered_files` directory created earlier. Then, go through the `find` manual and figure out how to list only executable files.

```
[](#cb222-1)# ???
[](#cb222-2)./hi.sh
[](#cb222-3)./hello_world.py
```

**30)** List at least one use case for piping the `find` output to the `xargs` command instead of using the `find -exec` option.

**31)** How does the `locate` command work faster than the equivalent `find` command?

# File Properties

In this chapter, you'll learn how to view file details like line and word counts, file and disk sizes, file types, extract parts of file path, etc. You'll also learn how to change file properties like timestamps and permissions.

> ![info](media/file0.svg) The [example_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files) directory has the scripts and sample input files used in this chapter.

## wc

The `wc` command is typically used to count the number of lines, words and characters for the given input(s). Here are some basic examples:

```
[](#cb223-1)# change to the 'example_files/text_files' directory
[](#cb223-2)$ cat greeting.txt
[](#cb223-3)Hi there
[](#cb223-4)Have a nice day
[](#cb223-5)
[](#cb223-6)# by default, gives newline/word/byte count (in that order)
[](#cb223-7)$ wc greeting.txt
[](#cb223-8) 2  6 25 greeting.txt
[](#cb223-9)
[](#cb223-10)# get only the specified counts
[](#cb223-11)$ wc -l greeting.txt
[](#cb223-12)2 greeting.txt
[](#cb223-13)$ wc -w greeting.txt
[](#cb223-14)6 greeting.txt
[](#cb223-15)$ wc -c greeting.txt
[](#cb223-16)25 greeting.txt
[](#cb223-17)$ wc -wc greeting.txt
[](#cb223-18) 6 25 greeting.txt
```

Filename won't be printed for stdin data. This is helpful to save the results in a variable for scripting purposes.

```
[](#cb224-1)$ wc -l <greeting.txt
[](#cb224-2)2
```

Word count is based on whitespace separation. You can pre-process the input to prevent certain non-whitespace characters to influence the results. `tr` can be used to remove a particular set of characters (this command will be discussed in the [Assorted Text Processing Tools](#ch013.xhtml_assorted-text-processing-tools) chapter).

```
[](#cb225-1)$ echo 'apple ; banana ; cherry' | wc -w
[](#cb225-2)5
[](#cb225-3)
[](#cb225-4)# remove characters other than alphabets and whitespace
[](#cb225-5)# -d option is for deleting, -c option complements the given set
[](#cb225-6)$ echo 'apple ; banana ; cherry' | tr -cd 'a-zA-Z[:space:]'
[](#cb225-7)apple  banana  cherry
[](#cb225-8)$ echo 'apple ; banana ; cherry' | tr -cd 'a-zA-Z[:space:]' | wc -w
[](#cb225-9)3
```

If you pass multiple files to the `wc` command, the count values will be displayed separately for each file. You'll also get a summary at the end, which sums the respective count of all the input files.

```
[](#cb226-1)$ wc greeting.txt fruits.txt sample.txt
[](#cb226-2)  2   6  25 greeting.txt
[](#cb226-3)  3   3  20 fruits.txt
[](#cb226-4) 15  38 183 sample.txt
[](#cb226-5) 20  47 228 total
```

You can use the `-L` option to report the length of the longest line in the input (excluding the newline character of a line). Note that `-L` won't count non-printable characters and tabs are converted to equivalent spaces. Multibyte characters and [grapheme clusters](https://unicode.org/reports/tr29/#Grapheme_Cluster_Boundaries) will each be counted as `1` (depending on the locale, they might become non-printable too).

```
[](#cb227-1)$ echo 'apple' | wc -L
[](#cb227-2)5
[](#cb227-3)
[](#cb227-4)$ echo 'αλεπού cag̈e' | wc -L
[](#cb227-5)11
[](#cb227-6)
[](#cb227-7)$ wc -L <greeting.txt
[](#cb227-8)15
```

Use `-m` option instead of `-c` if the input has multibyte characters.

```
[](#cb228-1)$ printf 'αλεπού' | wc -c
[](#cb228-2)12
[](#cb228-3)
[](#cb228-4)$ printf 'αλεπού' | wc -m
[](#cb228-5)6
```

## du

The `du` command helps you estimate the size of files and directories.

By default, size is given in size in terms of 1024 bytes. All directories and sub-directories are recursively reported, but files are ignored. You can use the `-a` option if files should also be reported. `du` is one of the commands that require an explicit option (`-L` in this case) if you want symbolic links to be followed.

```
[](#cb229-1)# change to the 'scripts' directory and source the 'du.sh' script
[](#cb229-2)$ source du.sh
[](#cb229-3)
[](#cb229-4)# n * 1024 bytes
[](#cb229-5)$ du
[](#cb229-6)28      ./projects/scripts
[](#cb229-7)48      ./projects
[](#cb229-8)8       ./todos
[](#cb229-9)7536    .
```

Use `-s` option to show the total directory size without descending into sub-directories. Add `-c` option to also show total size at the end.

```
[](#cb230-1)$ du -s projects report.log
[](#cb230-2)48      projects
[](#cb230-3)7476    report.log
[](#cb230-4)
[](#cb230-5)$ du -sc projects report.log
[](#cb230-6)48      projects
[](#cb230-7)7476    report.log
[](#cb230-8)7524    total
```

Here are some examples to illustrate size formatting options:

```
[](#cb231-1)# number of bytes
[](#cb231-2)$ du -b report.log
[](#cb231-3)7654321 report.log
[](#cb231-4)
[](#cb231-5)# n * 1024 bytes
[](#cb231-6)$ du -k report.log
[](#cb231-7)7476    report.log
[](#cb231-8)
[](#cb231-9)# n * 1024 * 1024 bytes
[](#cb231-10)$ du -m report.log
[](#cb231-11)8       report.log
```

The `-h` option reports size in human readable format (uses power of 1024). Use `--si` option to get results in powers of 1000 instead. If you use `du -h`, you can pipe the output to `sort -h` for sorting purposes.

```
[](#cb232-1)$ du -sh *
[](#cb232-2)48K     projects
[](#cb232-3)7.4M    report.log
[](#cb232-4)8.0K    todos
[](#cb232-5)
[](#cb232-6)$ du -sh * | sort -h
[](#cb232-7)8.0K    todos
[](#cb232-8)48K     projects
[](#cb232-9)7.4M    report.log
```

## df

The `df` command gives you the space usage of file systems. `df` without path arguments will give information about all the currently mounted file systems. You can specify `.` to get information only for the current filesystem:

```
[](#cb233-1)$ df .
[](#cb233-2)Filesystem     1K-blocks     Used Available Use% Mounted on
[](#cb233-3)/dev/sda1       98298500 58563816  34734748  63% /
```

Use `-h` option for human readable sizes. The `-B` option allows you to scale sizes by the specified amount. Use `--si` for size in powers of 1000 instead of 1024.

```
[](#cb234-1)$ df -h .
[](#cb234-2)Filesystem      Size  Used Avail Use% Mounted on
[](#cb234-3)/dev/sda1        94G   56G   34G  63% /
```

Use the `--output` option to report only specific fields of interest:

```
[](#cb235-1)$ df -h --output=size,used,file / /media/learnbyexample/projs
[](#cb235-2) Size  Used File
[](#cb235-3)  94G   56G /
[](#cb235-4)  92G   35G /media/learnbyexample/projs
[](#cb235-5)
[](#cb235-6)# 'awk' here excludes first line and matches lines with first field >= 30
[](#cb235-7)$ df -h --output=pcent,fstype,target | awk 'NR>1 && $1>=30'
[](#cb235-8) 63% ext3     /
[](#cb235-9) 38% ext4     /media/learnbyexample/projs
[](#cb235-10) 51% ext4     /media/learnbyexample/backups
```

## stat

The `stat` command is useful to get details like file type, size, inode, permissions, last accessed and modified timestamps, etc. You'll get all of these details by default. The `-c` and `--printf` options can be used to display only the required details in a particular format.

```
[](#cb236-1)# change to the 'scripts' directory and source the 'stat.sh' script
[](#cb236-2)$ source stat.sh
[](#cb236-3)
[](#cb236-4)# %x gives last accessed timestamp
[](#cb236-5)$ stat -c '%x' ip.txt
[](#cb236-6)2022-06-01 13:25:18.693823117 +0530
[](#cb236-7)
[](#cb236-8)# %y gives last modified timestamp
[](#cb236-9)$ stat -c '%y' ip.txt
[](#cb236-10)2022-05-24 14:39:41.285714934 +0530
[](#cb236-11)
[](#cb236-12)# %s gives file size in bytes
[](#cb236-13)# \n is used to get a newline
[](#cb236-14)# %i gives the inode value
[](#cb236-15)# same as: stat --printf='%s\n%i\n' ip.txt
[](#cb236-16)$ stat -c $'%s\n%i' ip.txt
[](#cb236-17)10
[](#cb236-18)787224
[](#cb236-19)
[](#cb236-20)# %N gives quoted filenames
[](#cb236-21)# if input is a link, path it points to is also displayed
[](#cb236-22)$ stat -c '%N' words.txt
[](#cb236-23)'words.txt' -> '/usr/share/dict/words'
```

You can also pass multiple file arguments:

```
[](#cb237-1)# %s gives file size in bytes
[](#cb237-2)# %n gives filenames
[](#cb237-3)$ stat -c '%s %n' ip.txt hi.sh
[](#cb237-4)10 ip.txt
[](#cb237-5)21 hi.sh
```

> ![info](media/file0.svg) ![warning](media/file1.svg) The `stat` command should be preferred instead of parsing `ls -l` output for file details. See [mywiki.wooledge: avoid parsing output of ls](https://mywiki.wooledge.org/ParsingLs) and [unix.stackexchange: why not parse ls?](https://unix.stackexchange.com/q/128985/109046) for explanation and other alternatives.

## touch

As mentioned earlier, the `touch` command helps you change the timestamps of files. You can do so based on current timestamp, passing an argument, copying the value from another file and so on.

By default, `touch` updates both access and modification timestamps to the current time. You can use `-a` to change only access timestamp and `-m` to change only modification timestamp.

```
[](#cb238-1)# change to the 'scripts' directory and source the 'touch.sh' script
[](#cb238-2)$ source touch.sh
[](#cb238-3)
[](#cb238-4)# last access and modification timestamps
[](#cb238-5)$ stat -c $'%x\n%y' fruits.txt
[](#cb238-6)2017-07-19 17:06:01.523308599 +0530
[](#cb238-7)2017-07-13 13:54:03.576055933 +0530
[](#cb238-8)
[](#cb238-9)# update access and modification values to the current time
[](#cb238-10)$ touch fruits.txt 
[](#cb238-11)$ stat -c $'%x\n%y' fruits.txt
[](#cb238-12)2022-06-14 13:01:25.921205889 +0530
[](#cb238-13)2022-06-14 13:01:25.921205889 +0530
```

You can use the `-r` option to copy timestamp information from one file to another. The `-d` and `-t` options will allow you to specify timestamps directly as part of the command.

```
[](#cb239-1)$ stat -c '%y' hi.sh
[](#cb239-2)2022-06-14 13:00:46.170416890 +0530
[](#cb239-3)
[](#cb239-4)# copy modified timestamp from 'ip.txt' to 'hi.sh'
[](#cb239-5)$ touch -m -r ip.txt hi.sh
[](#cb239-6)$ stat -c '%y' hi.sh
[](#cb239-7)2022-05-24 14:39:41.285714934 +0530
[](#cb239-8)
[](#cb239-9)# pass timestamp as an argument
[](#cb239-10)$ touch -m -d '2000-01-01 00:00:01' hi.sh
[](#cb239-11)$ stat -c '%y' hi.sh
[](#cb239-12)2000-01-01 00:00:01.000000000 +0530
```

As seen in the [Managing Files and Directories](#ch004.xhtml_managing-files-and-directories) chapter, `touch` creates a new file if the target file doesn't exist yet. You can use the `-c` option to prevent this behavior.

```
[](#cb240-1)$ ls report.txt
[](#cb240-2)ls: cannot access 'report.txt': No such file or directory
[](#cb240-3)$ touch report.txt
[](#cb240-4)$ ls report.txt
[](#cb240-5)report.txt
[](#cb240-6)
[](#cb240-7)$ touch -c xyz.txt
[](#cb240-8)$ ls xyz.txt
[](#cb240-9)ls: cannot access 'xyz.txt': No such file or directory
```

## file

The `file` command helps you identify text encoding (ASCII, UTF-8, etc), whether the file is executable and so on.

Here are some examples to show how the `file` command behaves for different types:

```
[](#cb241-1)# change to the 'scripts' directory and source the 'file.sh' script
[](#cb241-2)$ source file.sh
[](#cb241-3)$ ls -F
[](#cb241-4)hi.sh*  ip.txt  moon.png  sunrise.jpg
[](#cb241-5)
[](#cb241-6)$ file ip.txt hi.sh
[](#cb241-7)ip.txt: ASCII text
[](#cb241-8)hi.sh: Bourne-Again shell script, ASCII text executable
[](#cb241-9)
[](#cb241-10)$ printf 'αλεπού\n' | file -
[](#cb241-11)/dev/stdin: UTF-8 Unicode text
[](#cb241-12)
[](#cb241-13)$ printf 'hi\r\n' | file -
[](#cb241-14)/dev/stdin: ASCII text, with CRLF line terminators
```

Example for image files:

```
[](#cb242-1)# output of 'sunrise.jpg' wrapped for illustration purposes
[](#cb242-2)$ file sunrise.jpg moon.png
[](#cb242-3)sunrise.jpg: JPEG image data, JFIF standard 1.01, resolution (DPI), density
[](#cb242-4)    96x96, segment length 16, baseline, precision 8, 76x76, components 3
[](#cb242-5)moon.png:    PNG image data, 76 x 76, 8-bit colormap, non-interlaced
```

You can use the `-b` option to avoid filenames in the output:

```
[](#cb243-1)$ file -b ip.txt 
[](#cb243-2)ASCII text
```

Here is an example of finding particular type of files, say `image` files.

```
[](#cb244-1)# assuming filenames do not contain ':' or newline characters
[](#cb244-2)# awk here helps to print the first field of lines containing 'image data'
[](#cb244-3)$ find -type f -exec file {} + | awk -F: '/\<image data\>/{print $1}'
[](#cb244-4)./sunset.jpg
[](#cb244-5)./moon.png
```

> ![info](media/file0.svg) See also `identify` command which "describes the format and characteristics of one or more image files".

## basename

By default, the `basename` command will remove the leading directory component from the given path argument. Any trailing slashes will be removed before determining the portion to be extracted.

```
[](#cb245-1)$ basename /home/learnbyexample/example_files/scores.csv
[](#cb245-2)scores.csv
[](#cb245-3)
[](#cb245-4)# quote the arguments as needed
[](#cb245-5)$ basename 'path with spaces/report.log'
[](#cb245-6)report.log
```

You can use the `-s` option to remove a suffix from the filename. Usually used to remove the file extension.

```
[](#cb246-1)$ basename -s'.csv' /home/learnbyexample/example_files/scores.csv
[](#cb246-2)scores
[](#cb246-3)
[](#cb246-4)# suffix will be removed only once
[](#cb246-5)$ basename -s'.txt' purchases.txt.txt
[](#cb246-6)purchases.txt
```

The `basename` command requires `-a` or `-s` (which implies `-a`) to work with multiple arguments.

```
[](#cb247-1)$ basename -a /backups/jan_2021.tar.gz /home/learnbyexample/report.log
[](#cb247-2)jan_2021.tar.gz
[](#cb247-3)report.log
[](#cb247-4)
[](#cb247-5)# -a is implied when -s is used
[](#cb247-6)$ basename -s'.txt' logs/purchases.txt logs/report.txt
[](#cb247-7)purchases
[](#cb247-8)report
```

## dirname

By default, the `dirname` command removes the trailing path component (after removing any trailing slashes).

```
[](#cb248-1)$ dirname /home/learnbyexample/example_files/scores.csv
[](#cb248-2)/home/learnbyexample/example_files
[](#cb248-3)
[](#cb248-4)# one or more trailing slashes will not affect the output
[](#cb248-5)$ dirname /home/learnbyexample/example_files/
[](#cb248-6)/home/learnbyexample
[](#cb248-7)
[](#cb248-8)# unlike basename, multiple arguments are accepted by default
[](#cb248-9)$ dirname /home/learnbyexample/example_files/scores.csv ../report/backups/
[](#cb248-10)/home/learnbyexample/example_files
[](#cb248-11)../report
```

You can use shell features like command substitution to combine the effects of `basename` and `dirname` commands.

```
[](#cb249-1)# extract the second last path component
[](#cb249-2)$ basename $(dirname /home/learnbyexample/example_files/scores.csv)
[](#cb249-3)example_files
```

## chmod

You can use the `chmod` command to change file and directory permissions. Consider this example:

```
[](#cb250-1)$ mkdir practice_chmod
[](#cb250-2)$ cd practice_chmod
[](#cb250-3)$ echo 'learnbyexample' > ip.txt
[](#cb250-4)
[](#cb250-5)# this info can also be seen in the first column of 'ls -l' output
[](#cb250-6)$ stat -c '%A' ip.txt
[](#cb250-7)-rw-rw-r--
```

In the above output, the 10 characters displayed in the last line are related to file type and permissions. First character indicates the **file type**. The most common ones are shown below:

*   `-` regular file
*   `d` directory
*   `l` symbolic link

The other nine characters represent three sets of **file permissions** for *user* (`u`), *group* (`g`) and *others* (`o`), in that order.

*   *user* — file owner
*   *group* — users having file access as part of a group
*   *others* — everyone else

Only `rwx` file properties will be discussed in this section. For other types of properties, refer to the [coreutils manual: File permissions](https://www.gnu.org/software/coreutils/manual/coreutils.html#File-permissions).

**Permission reference table for files:**

| Character | Meaning | Value |
| --- | --- | --- |
| `r` | read | `4` |
| `w` | write | `2` |
| `x` | execute | `1` |
| `-` | no permission | `0` |

Here's an example showing both `rwx` and numerical representations of a file's permissions:

```
[](#cb251-1)$ stat -c '%A' ip.txt
[](#cb251-2)-rw-rw-r--
[](#cb251-3)
[](#cb251-4)# r(4) + w(2) + 0 = 6
[](#cb251-5)# r(4) + 0 + 0 = 4
[](#cb251-6)$ stat -c '%a' ip.txt
[](#cb251-7)664
```

> ![info](media/file0.svg) Note that the permissions are not straightforward to understand for directories. If a directory only has the `x` permission, you can `cd` into it but you cannot read the contents (using `ls` for example). If a directory only has the `r` permission, you cannot `cd` into it, but you'll be able to read the contents (along with "cannot access" error). For this reason, `rx` permissions are almost always enabled/disabled together. The `w` permission allows you to add or remove contents, provided `x` is active.

**Changing permissions for all three categories**

You can provide numbers for `ugo` (in that order) to change permissions. This is best understood with examples:

```
[](#cb252-1)$ printf '#!/bin/bash\n\necho hi\n' > hi.sh
[](#cb252-2)$ stat -c '%a %A' hi.sh
[](#cb252-3)664 -rw-rw-r--
[](#cb252-4)
[](#cb252-5)# r(4) + w(2) + x(1) = 7
[](#cb252-6)# r(4) + 0 + x(1) = 5
[](#cb252-7)$ chmod 755 hi.sh
[](#cb252-8)$ stat -c '%a %A' hi.sh
[](#cb252-9)755 -rwxr-xr-x
```

Here's an example for a directory:

```
[](#cb253-1)$ mkdir dot_files
[](#cb253-2)$ stat -c '%a %A' dot_files
[](#cb253-3)775 drwxrwxr-x
[](#cb253-4)
[](#cb253-5)$ chmod 700 dot_files
[](#cb253-6)$ stat -c '%a %A' dot_files
[](#cb253-7)700 drwx------
```

You can also use `mkdir -m` instead of the `mkdir+chmod` combination seen above. The argument to the `-m` option accepts the same syntax as `chmod` (including the format that'll be discussed next).

```
[](#cb254-1)$ mkdir -m 750 backups
[](#cb254-2)$ stat -c '%a %A' backups
[](#cb254-3)750 drwxr-x---
```

> ![info](media/file0.svg) You can use `chmod -R` to recursively change permissions. Use `find+exec` if you want to apply changes only for files filtered by some criteria.

**Changing permissions for specific categories**

You can assign (`=`), add (`+`) or remove (`-`) permissions by using those symbols followed by one or more `rwx` permissions. This depends on the `umask` value:

```
[](#cb255-1)$ umask
[](#cb255-2)0002
```

`umask` value of `0002` means:

*   read and execute permissions without `ugo` prefix affects all the three categories
*   write permissions without `ugo` prefix affects only `user` and `group` categories

Here are some examples without `ugo` prefixes:

```
[](#cb256-1)# remove execute permission for all three categories
[](#cb256-2)$ chmod -x hi.sh
[](#cb256-3)
[](#cb256-4)# add write permission only for 'user' and 'group'
[](#cb256-5)$ chmod +w ip.txt
[](#cb256-6)
[](#cb256-7)$ touch sample.txt
[](#cb256-8)$ chmod 702 sample.txt
[](#cb256-9)# give only read permission for all three categories
[](#cb256-10)# write/execute permissions, if any, will be removed
[](#cb256-11)$ chmod =r sample.txt
[](#cb256-12)$ stat -c '%a %A' sample.txt
[](#cb256-13)444 -r--r--r--
[](#cb256-14)
[](#cb256-15)# give read and write permissions for 'user' and 'group'
[](#cb256-16)# and read permission for 'others'
[](#cb256-17)# execute permissions, if any, will be removed
[](#cb256-18)$ chmod =rw hi.sh
```

Here are some examples with `ugo` prefixes. You can use `a` to refer to all the three categories. For example, `a+w` is same as `ugo+w`.

```
[](#cb257-1)# remove read and write permissions only for 'others'
[](#cb257-2)$ chmod o-rw sample.txt
[](#cb257-3)
[](#cb257-4)# add execute permission for 'group' and 'others'
[](#cb257-5)$ chmod go+x hi.sh
[](#cb257-6)
[](#cb257-7)# give read and write permissions for all three categories
[](#cb257-8)# execute permissions, if any, will be removed
[](#cb257-9)$ chmod a=rw hi.sh
```

You can use `,` to separate multiple permissions:

```
[](#cb258-1)# remove execute permission for 'group' and 'others'
[](#cb258-2)# remove write permission for 'others'
[](#cb258-3)$ chmod go-x,o-w hi.sh
```

**Further Reading**

*   [Linux Permissions Primer](https://danielmiessler.com/study/unixlinux_permissions/)
*   [unix.stackexchange: why chmod +w filename not giving write permission to other](https://unix.stackexchange.com/q/429421/109046)

## Exercises

> ![info](media/file0.svg) Use [example_files/text_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files/text_files) directory for input files used in the following exercises, unless otherwise specified.

> ![info](media/file0.svg) Create a temporary directory for exercises that may require you to create some files and directories. You can delete such practice directories afterwards.

**1)** Save the number of lines in the `greeting.txt` input file to the `lines` shell variable.

```
[](#cb259-1)# ???
[](#cb259-2)$ echo "$lines"
[](#cb259-3)2
```

**2)** What do you think will be the output of the following command?

```
[](#cb260-1)$ echo 'dragons:2 ; unicorns:10' | wc -w
```

**3)** Use appropriate options and arguments to get the output shown below.

```
[](#cb261-1)$ printf 'apple\nbanana\ncherry' | wc # ???
[](#cb261-2)     15     183 sample.txt
[](#cb261-3)      2      19 -
[](#cb261-4)     17     202 total
```

**4)** Go through the `wc` manual and use appropriate options and arguments to get the output shown below.

```
[](#cb262-1)$ printf 'greeting.txt\0scores.csv' | wc # ???
[](#cb262-2)2 6 25 greeting.txt
[](#cb262-3)4 4 70 scores.csv
[](#cb262-4)6 10 95 total
```

**5)** What is the difference between `wc -c` and `wc -m` options? And which option would you use to get the longest line length?

**6)** Find filenames ending with `.log` and report their sizes in human readable format. Use `find+du` combination for the first case and `ls` command (with appropriate shell features) for the second case.

```
[](#cb263-1)# change to the 'scripts' directory and source the 'du.sh' script
[](#cb263-2)$ source du.sh
[](#cb263-3)
[](#cb263-4)# ??? find+du
[](#cb263-5)16K     ./projects/errors.log
[](#cb263-6)7.4M    ./report.log
[](#cb263-7)
[](#cb263-8)# ??? ls and shell features
[](#cb263-9) 16K projects/errors.log
[](#cb263-10)7.4M report.log
```

**7)** Report sizes of files/directories in the current path in powers of `1000` without descending into sub-directories. Also, show a total at the end.

```
[](#cb264-1)# change to the 'scripts' directory and source the 'du.sh' script
[](#cb264-2)$ source du.sh
[](#cb264-3)
[](#cb264-4)# ???
[](#cb264-5)50k     projects
[](#cb264-6)7.7M    report.log
[](#cb264-7)8.2k    todos
[](#cb264-8)7.8M    total
```

**8)** What does the `du --apparent-size` option do?

**9)** When will you use the `df` command instead of `du`? Which `df` command option will help you to report only specific fields of interest?

**10)** Display the size of `scores.csv` and `timings.txt` files in the format shown below.

```
[](#cb265-1)$ stat # ???
[](#cb265-2)scores.csv: 70
[](#cb265-3)timings.txt: 49
```

**11)** Which `touch` option will help you prevent file creation if it doesn't exist yet?

**12)** Assume `new_file.txt` doesn't exist in the current working directory. What would be the output of the `stat` command shown below?

```
[](#cb266-1)$ touch -t '202010052010.05' new_file.txt
[](#cb266-2)$ stat -c '%y' new_file.txt
[](#cb266-3)# ???
```

**13)** Is the following `touch` command valid? If so, what would be the output of the `stat` command that follows?

```
[](#cb267-1)# change to the 'scripts' directory and source the 'touch.sh' script
[](#cb267-2)$ source touch.sh
[](#cb267-3)
[](#cb267-4)$ stat -c '%n: %y' fruits.txt
[](#cb267-5)fruits.txt: 2017-07-13 13:54:03.576055933 +0530
[](#cb267-6)
[](#cb267-7)$ touch -r fruits.txt f{1..3}.txt
[](#cb267-8)$ stat -c '%n: %y' f*.txt
[](#cb267-9)# ???
```

**14)** Use appropriate option(s) to get the output shown below.

```
[](#cb268-1)$ printf 'αλεπού\n' | file -
[](#cb268-2)/dev/stdin: UTF-8 Unicode text
[](#cb268-3)
[](#cb268-4)$ printf 'αλεπού\n' | file # ???
[](#cb268-5)UTF-8 Unicode text
```

**15)** Is the following command valid? If so, what would be the output?

```
[](#cb269-1)$ basename -s.txt ~///test.txt///
[](#cb269-2)# ???
```

**16)** Given the file path in the shell variable `p`, how'd you obtain the output shown below?

```
[](#cb270-1)$ p='~/projects/square_tictactoe/python/game.py'
[](#cb270-2)$ dirname # ???
[](#cb270-3)~/projects/square_tictactoe
```

**17)** Explain what each of the characters mean in the following `stat` command's output.

```
[](#cb271-1)$ stat -c '%A' ../scripts/
[](#cb271-2)drwxrwxr-x
```

**18)** What would be the output of the second `stat` command shown below?

```
[](#cb272-1)$ touch new_file.txt
[](#cb272-2)$ stat -c '%a %A' new_file.txt
[](#cb272-3)664 -rw-rw-r--
[](#cb272-4)
[](#cb272-5)$ chmod 546 new_file.txt
[](#cb272-6)$ stat -c '%a %A' new_file.txt
[](#cb272-7)# ???
```

**19)** How would you specify directory permissions using the `mkdir` command?

```
[](#cb273-1)# instead of this
[](#cb273-2)$ mkdir back_up
[](#cb273-3)$ chmod 750 back_up
[](#cb273-4)$ stat -c '%a %A' back_up
[](#cb273-5)750 drwxr-x---
[](#cb273-6)$ rm -r back_up
[](#cb273-7)
[](#cb273-8)# do this
[](#cb273-9)$ mkdir # ???
[](#cb273-10)$ stat -c '%a %A' back_up
[](#cb273-11)750 drwxr-x---
```

**20)** Change the file permission of `book_list.txt` to match the output of the second `stat` command shown below. Don't use the number `220`, specify the changes in terms of `rwx` characters.

```
[](#cb274-1)$ touch book_list.txt
[](#cb274-2)$ stat -c '%a %A' book_list.txt
[](#cb274-3)664 -rw-rw-r--
[](#cb274-4)
[](#cb274-5)# ???
[](#cb274-6)$ stat -c '%a %A' book_list.txt
[](#cb274-7)220 --w--w----
```

**21)** Change the permissions of `test_dir` to match the output of the second `stat` command shown below. Don't use the number `757`, specify the changes in terms of `rwx` characters.

```
[](#cb275-1)$ mkdir test_dir
[](#cb275-2)$ stat -c '%a %A' test_dir
[](#cb275-3)775 drwxrwxr-x
[](#cb275-4)
[](#cb275-5)# ???
[](#cb275-6)$ stat -c '%a %A' test_dir
[](#cb275-7)757 drwxr-xrwx
```

# Managing Processes

This chapter gives a basic overview of process management for interactive usage only. Handling processes for other use cases, such as system administration, requires a more robust solution (see [mywiki.wooledge: Process Management](https://mywiki.wooledge.org/ProcessManagement) to get started for such use cases).

## Definitions

Here are some definitions that will be handy to know for this chapter's contents:

*   **Program** is a set of instructions written to perform a task
*   **Process** is any running program
*   **Daemon** are background processes
*   **Job** is a process that is not a daemon
    *   i.e. jobs are interactive programs under user control

## Running jobs in background

Some commands and scripts can take more than few minutes to complete, and you might still need to continue using the shell. If you are not dependent on the current shell environment, you could just open another shell instance and continue working.

Another option is to push the job to the background, either at the time of command invocation itself or after the fact. Make sure to redirect standard output and error to avoid interfering with your continued interactive usage. Appending an `&` character to the command will execute it in the background.

```
[](#cb276-1)$ tkdiff ip.txt ip.txt.bkp &
[](#cb276-2)[1] 12726
```

In the above example, `[1]` refers to the job number and `12726` is the PID (process ID). You can use the `jobs` and `ps` commands to track active jobs:

```
[](#cb277-1)$ jobs
[](#cb277-2)[1]+  Running                 tkdiff ip.txt ip.txt.bkp &
[](#cb277-3)
[](#cb277-4)$ ps
[](#cb277-5)    PID TTY          TIME CMD
[](#cb277-6)   9657 pts/1    00:00:00 bash
[](#cb277-7)  12726 pts/1    00:00:00 wish
[](#cb277-8)  12730 pts/1    00:00:00 ps
```

But what if you forgot to append `&` to the command? You can follow these steps:

*   `Ctrl+z` — suspend the current running job
*   `bg` — push the recently suspended job to the background
*   continue using shell
*   `fg` — bring the recently pushed background job to the foreground
    *   you can use `fg %n` to bring the `n`th job number to the foreground

Here's a demo that you can try:

```
[](#cb278-1)# sleep for 30 seconds (used here for illustration purposes)
[](#cb278-2)# press Ctrl+z to suspend this job
[](#cb278-3)# you'll get the job number, status and the command in the output
[](#cb278-4)$ sleep 30
[](#cb278-5)^Z
[](#cb278-6)[1]+  Stopped                 sleep 30
[](#cb278-7)
[](#cb278-8)# bg puts the job considered as the current by the shell to the background 
[](#cb278-9)$ bg
[](#cb278-10)[1]+ sleep 30 &
[](#cb278-11)
[](#cb278-12)# use 'jobs' or 'ps' to check list of jobs
[](#cb278-13)# '+' after the job number is used to indicate the current job
[](#cb278-14)$ jobs
[](#cb278-15)[1]+  Running                 sleep 30 &
[](#cb278-16)$ ps
[](#cb278-17)    PID TTY          TIME CMD
[](#cb278-18)   2380 pts/0    00:00:00 bash
[](#cb278-19)   6160 pts/0    00:00:00 sleep
[](#cb278-20)   6162 pts/0    00:00:00 ps
[](#cb278-21)
[](#cb278-22)# fg brings the most recently pushed background job to the foreground
[](#cb278-23)$ fg
[](#cb278-24)sleep 30
[](#cb278-25)$ 
```

> ![info](media/file2.svg) `jobs`, `bg` and `fg` are shell builtins. See [bash manual: Job Control](https://www.gnu.org/software/bash/manual/bash.html#Job-Control) for more details. See also [this tutorial on job control](https://www.digitalocean.com/community/tutorials/how-to-use-bash-s-job-control-to-manage-foreground-and-background-processes).

> ![info](media/file2.svg) See also [I want to run something in the background and then log out](https://mywiki.wooledge.org/ProcessManagement#I_want_to_run_something_in_the_background_and_then_log_out.) — `screen`, `tmux`, `nohup`, `disown`, etc.

## ps

The `ps` command gives a snapshot of the current processes. A few examples were already seen earlier in this chapter. Here's an example with the `-f` option (full-format listing):

```
[](#cb279-1)$ ps -f
[](#cb279-2)UID          PID    PPID  C STIME TTY          TIME CMD
[](#cb279-3)learnby+   12299   12298  0 16:39 pts/0    00:00:00 bash
[](#cb279-4)learnby+   12311   12299  0 16:39 pts/0    00:00:00 ps -f
```

The fields in the above example are effective user ID (UID), process ID (PID), parent process ID (PPID), processor utilization (C), starting time (STIME), controlling terminal (TTY), cumulative CPU time (TIME) and command with all its arguments (CMD). You can use the `-o` option to customize the fields you want. The `--sort` option will help you to sort based on specific fields. See [ps manual: Standard Format Specifiers](https://www.mankier.com/1/ps#Standard_Format_Specifiers) for complete list of formats available.

The `-e` (or `-A`) option selects all processes. This option is typically used in combination with `grep` for filtering:

```
[](#cb280-1)$ ps -e | grep 'vim'
[](#cb280-2)   6195 ?        00:03:13 gvim
```

> ![info](media/file0.svg) See also [linuxjourney: ps tutorial](https://linuxjourney.com/lesson/monitor-processes-ps-command).

## pgrep

The `pgrep` command helps you filter processes based on their name and attributes. By default, it matches against the process name, for example:

```
[](#cb281-1)$ ps -e | grep 'vim'
[](#cb281-2)   2006 ?        00:00:27 gvim
[](#cb281-3)   3992 pts/2    00:00:00 vim
[](#cb281-4)
[](#cb281-5)$ pgrep 'vim'
[](#cb281-6)2006
[](#cb281-7)3992
```

You can use the `-l` option to display the process name as well (PID is shown by default).

```
[](#cb282-1)$ pgrep -l 'vim'
[](#cb282-2)2006 gvim
[](#cb282-3)3992 vim
```

To match the process name exactly (instead of matching anywhere), use the `-x` option.

```
[](#cb283-1)$ pgrep -x 'vim'
[](#cb283-2)3992
```

The `-a` option will list the full command line (the `-l` option seen earlier gives only the name, not the arguments).

```
[](#cb284-1)$ pgrep -a 'vim'
[](#cb284-2)2006 gvim -p notes.txt src/managing-processes.md
[](#cb284-3)3992 vim substitution.md
```

> ![info](media/file0.svg) There are several more options like filtering based on effective UID, PPID, etc. See [pgrep manual](https://www.mankier.com/1/pgrep) for more details.

## kill

Sometimes, a process might not be responding to your interaction, might be taking too long, accidentally uses too much memory, and so on. You can use the `kill` command to manage such processes.

As mentioned at the beginning of this chapter, these examples are suggested for interactive processes initiated by you (other usage, for example in scripts, will require different strategies). Be 100% sure before you attempt to send signals to manage processes.

You can pass signals by name or by their associated number. Use `kill -l` to get a full list of signals. See also [unix.stackexchange: List of Signals](https://unix.stackexchange.com/q/317492/109046) and [unix.stackexchange: What causes various signals to be sent?](https://unix.stackexchange.com/q/6332/109046)

```
[](#cb285-1)# first 20 signals (out of 64) listed below 
[](#cb285-2)$ kill -l
[](#cb285-3) 1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP
[](#cb285-4) 6) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR1
[](#cb285-5)11) SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM
[](#cb285-6)16) SIGSTKFLT   17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP
[](#cb285-7)...
```

You can use PID or job number to specify the process to which the signal has to be sent. By default, `SIGTERM` (`15`) is sent, which is a polite way to ask the program to terminate. Here's an example:

```
[](#cb286-1)# 'sleep' is used here to emulate a long running process
[](#cb286-2)# press Ctrl+z to suspend this command
[](#cb286-3)$ sleep 100
[](#cb286-4)^Z
[](#cb286-5)[1]+  Stopped                 sleep 100
[](#cb286-6)
[](#cb286-7)# terminate job number 1
[](#cb286-8)# by default, SIGTERM is sent
[](#cb286-9)$ kill %1
[](#cb286-10)# just press Enter
[](#cb286-11)$
[](#cb286-12)[1]+  Terminated              sleep 100
```

Note that in the above example, pressing `Ctrl+z` actually sends the `SIGTSTP` (`20`) signal. Programs usually handle such signals to find a safer spot to suspend. Pressing `Ctrl+c` sends the `SIGINT` (`2`) signal, usually used to abort a process (depends on how the program handles it). You can use `Ctrl+\` to send `SIGQUIT` (`3`), typically used to ask the program to quit and give a [core dump](https://en.wikipedia.org/wiki/Core_dump). See also [stackoverflow: gracefully shutdown processes](https://stackoverflow.com/q/690415/4082052).

Here's an illustration to show how to pass signals by their names and numerical values:

```
[](#cb287-1)$ sleep 100 &
[](#cb287-2)[1] 10051
[](#cb287-3)
[](#cb287-4)# suspend the above job, similar to using Ctrl+z
[](#cb287-5)# -20 refers to the signal number 20, i.e. SIGTSTP
[](#cb287-6)# 10051 is the PID
[](#cb287-7)$ kill -20 10051
[](#cb287-8)
[](#cb287-9)[1]+  Stopped                 sleep 100
[](#cb287-10)
[](#cb287-11)# resume the job in background
[](#cb287-12)$ bg
[](#cb287-13)[1]+ sleep 100 &
[](#cb287-14)
[](#cb287-15)# -s option allows you to specify signal by its name
[](#cb287-16)# '-s SIGTERM' is optional here, since that is the default
[](#cb287-17)$ kill -s SIGTERM 10051
[](#cb287-18)$ 
[](#cb287-19)[1]+  Terminated              sleep 100
```

> ![info](media/file0.svg) ![warning](media/file1.svg) If you need to terminate a process at all costs, you can use `SIGKILL` (`9`). This is a signal that cannot be blocked by programs. Use `Ctrl+z` to suspend a runaway job and then apply `kill -9` instead of trying to abort such jobs using `Ctrl+c`. See also [unix.stackexchange: why kill -9 should be avoided](https://unix.stackexchange.com/q/8916/109046).

> ![info](media/file0.svg) Note that your system will likely have several different implementations of the `kill` command. The shell builtin version was discussed in this section.

## top

The `top` command displays processes in a tabular format along with information like PID, process name, memory usage and so on. Here's a sample screenshot:

![sample screenshot for the top command](media/file9.png)

This command opens an interactive session, and automatically updates the information being displayed as well. You can press `M` (uppercase) to sort the processes by memory usage. Press `e` repeatedly to display memory sizes in terms of mega/giga/etc. Press `h` for help and press `q` to quit the session.

> ![info](media/file0.svg) Press `W` (uppercase) to write the current settings to the `toprc` configuration file and quit. The next time you use the `top` command, it will be displayed in the format that was saved.

> ![info](media/file0.svg) See also alternative implementations like [htop](https://github.com/htop-dev/htop/) and [btop](https://github.com/aristocratos/btop).

## free

The `free` command displays information about your system memory. Here's an example:

```
[](#cb288-1)# -h option shows the results in human readable format
[](#cb288-2)$ free -h
[](#cb288-3)              total        used        free      shared  buff/cache   available
[](#cb288-4)Mem:          7.6Gi       2.4Gi       2.3Gi       267Mi       2.9Gi       4.7Gi
[](#cb288-5)Swap:         3.6Gi          0B       3.6Gi
```

## Further Reading

*   [mywiki.wooledge: Process Management](https://mywiki.wooledge.org/ProcessManagement)
*   [ryanstutorials: Process Management](https://ryanstutorials.net/linuxtutorial/processes.php)
*   [digitalocean: Managing Linux Processes](https://www.digitalocean.com/community/tutorials/how-to-use-ps-kill-and-nice-to-manage-processes-in-linux)
*   [Linux ate my ram](https://www.linuxatemyram.com/) — Linux is borrowing unused memory for disk caching. This makes it look like you are low on memory, but you are not! Everything is fine!

## Exercises

**1)** How would you invoke a command to be executed in the background? And what would you do to push a job to the background after it has already been launched? What commands can you use to track active jobs?

**2)** What do `+` and `-` symbols next to job numbers indicate?

**3)** When would you use `fg %n` and `bg %n` instead of just `fg` and `bg` respectively?

**4)** Which option will help you customize the output fields needed for the `ps` command?

**5)** What's the difference between `pgrep -a` and `pgrep -l` options?

**6)** If the job number is `2`, would you use `kill %2` or `kill 2` to send `SIGTERM` to that process?

**7)** Which signal does the `Ctrl+c` shortcut send to the currently running process?

**8)** Which command helps you to continuously monitor processes, along with details like PID, memory usage, etc?

**9)** Which key will help you manipulate kill tasks from within the `top` session?

**10)** What does the `free` command do?

# Multipurpose Text Processing Tools

Many CLI text processing tools have been in existence for about half a century. And newer tools are being written to solve ever expanding text processing problems. Just knowing that a particular tool exists or searching for a tool before attempting to write your own solution can be a time saver. Also, popular tools are likely to be optimized for speed, hardened against bugs from wide usage, discussed on forums, and so on.

`grep` was already covered in the [Searching Files and Filenames](#ch007.xhtml_searching-files-and-filenames) chapter. In addition, `sed`, `awk` and `perl` are essential tools to solve a wide variety of text processing problems from the command line. In this chapter, you'll learn field processing, use regular expressions for search and replace requirements, perform operations based on multiple lines and files, etc.

> ![info](media/file0.svg) The examples presented in this chapter only cover some of the functionalities. I've written separate books to cover these tools with more detailed explanations, examples and exercises. See [https://learnbyexample.github.io/books/](https://learnbyexample.github.io/books/) for links to these books.

> ![info](media/file0.svg) The [example_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files) directory has the sample input files used in this chapter.

## sed

The command name `sed` is derived from **s**tream **ed**itor. Here, stream refers to data being passed via shell pipes. Thus, the command's primary functionality is to act as a text editor for **stdin** data with **stdout** as the output target. You can also edit file input and save the changes back to the same file if needed.

### Substitution

`sed` has various commands to manipulate text input. The **substitute** command is most commonly used, whose syntax is `s/REGEXP/REPLACEMENT/FLAGS`. Here are some basic examples:

```
[](#cb289-1)# for each input line, change only the first ',' to '-'
[](#cb289-2)$ printf '1,2,3,4\na,b,c,d\n' | sed 's/,/-/'
[](#cb289-3)1-2,3,4
[](#cb289-4)a-b,c,d
[](#cb289-5)
[](#cb289-6)# change all matches by adding the 'g' flag
[](#cb289-7)$ printf '1,2,3,4\na,b,c,d\n' | sed 's/,/-/g'
[](#cb289-8)1-2-3-4
[](#cb289-9)a-b-c-d
```

Here's an example with file input:

```
[](#cb290-1)$ cat greeting.txt
[](#cb290-2)Hi there
[](#cb290-3)Have a nice day
[](#cb290-4)
[](#cb290-5)# change 'day' to 'weekend'
[](#cb290-6)$ sed 's/day/weekend/g' greeting.txt
[](#cb290-7)Hi there
[](#cb290-8)Have a nice weekend
```

What if you want to issue multiple substitute commands (or use several other `sed` commands)? It will depend on the command being used. Here's an example where you can use the `-e` option or separate the commands with a `;` character.

```
[](#cb291-1)# change all occurrences of 'day' to 'weekend'
[](#cb291-2)# add '.' to the end of each line
[](#cb291-3)$ sed 's/day/weekend/g; s/$/./' greeting.txt
[](#cb291-4)Hi there.
[](#cb291-5)Have a nice weekend.
[](#cb291-6)
[](#cb291-7)# same thing with -e option
[](#cb291-8)$ sed -e 's/day/weekend/g' -e 's/$/./' greeting.txt
[](#cb291-9)Hi there.
[](#cb291-10)Have a nice weekend.
```

### Inplace editing

You can use the `-i` option for inplace editing. Pass an argument to this option to save the original input as a backup.

```
[](#cb292-1)$ cat ip.txt
[](#cb292-2)deep blue
[](#cb292-3)light orange
[](#cb292-4)blue delight
[](#cb292-5)
[](#cb292-6)# output from sed is written back to 'ip.txt'
[](#cb292-7)# original file is preserved in 'ip.txt.bkp'
[](#cb292-8)$ sed -i.bkp 's/blue/green/g' ip.txt
[](#cb292-9)$ cat ip.txt
[](#cb292-10)deep green
[](#cb292-11)light orange
[](#cb292-12)green delight
```

### Filtering features

`sed` also has features to filter the lines like `grep`. And you can apply other `sed` commands for these filtered lines as needed.

```
[](#cb293-1)# -n disables automatic printing
[](#cb293-2)# 'p' command prints the contents of pattern space
[](#cb293-3)# same as: grep 'at'
[](#cb293-4)$ printf 'sea\neat\ndrop\n' | sed -n '/at/p'
[](#cb293-5)eat
[](#cb293-6)
[](#cb293-7)# 'd' command deletes the matching lines
[](#cb293-8)# same as: grep -v 'at'
[](#cb293-9)$ printf 'sea\neat\ndrop\n' | sed '/at/d'
[](#cb293-10)sea
[](#cb293-11)drop
[](#cb293-12)
[](#cb293-13)# change commas to hyphens only if the input line contains '2'
[](#cb293-14)$ printf '1,2,3,4\na,b,c,d\n' | sed '/2/ s/,/-/g'
[](#cb293-15)1-2-3-4
[](#cb293-16)a,b,c,d
[](#cb293-17)
[](#cb293-18)# change commas to hyphens if the input line does NOT contain '2'
[](#cb293-19)$ printf '1,2,3,4\na,b,c,d\n' | sed '/2/! s/,/-/g'
[](#cb293-20)1,2,3,4
[](#cb293-21)a-b-c-d
```

You can use `q` and `Q` commands to quit `sed` once a matching line is found:

```
[](#cb294-1)# quit after a line containing 'st' is found
[](#cb294-2)$ printf 'apple\nsea\neast\ndust' | sed '/st/q'
[](#cb294-3)apple
[](#cb294-4)sea
[](#cb294-5)east
[](#cb294-6)
[](#cb294-7)# matching line won't be printed in this case
[](#cb294-8)$ printf 'apple\nsea\neast\ndust' | sed '/st/Q'
[](#cb294-9)apple
[](#cb294-10)sea
```

Apart from regexp, filtering can also be done based on line numbers, address ranges, etc.

```
[](#cb295-1)# perform substitution only for the second line
[](#cb295-2)# use '$' instead of a number to indicate last input line
[](#cb295-3)$ printf 'gates\nnot\nused\n' | sed '2 s/t/*/g'
[](#cb295-4)gates
[](#cb295-5)no*
[](#cb295-6)used
[](#cb295-7)
[](#cb295-8)# address range example, same as: sed -n '3,8!p'
[](#cb295-9)# you can also use regexp to construct address ranges
[](#cb295-10)$ seq 15 24 | sed '3,8d'
[](#cb295-11)15
[](#cb295-12)16
[](#cb295-13)23
[](#cb295-14)24
```

If you need to issue multiple commands for filtered lines, you can group those commands within `{}` characters. Here's an example:

```
[](#cb296-1)# for lines containing 'e', replace 's' with '*' and 't' with '='
[](#cb296-2)# note that the second line isn't changed as there's no 'e'
[](#cb296-3)$ printf 'gates\nnot\nused\n' | sed '/e/{s/s/*/g; s/t/=/g}'
[](#cb296-4)ga=e*
[](#cb296-5)not
[](#cb296-6)u*ed
```

### Regexp substitution

Here are some regexp based substitution examples. The `-E` option enables **ERE** (default is **BRE**). Most of the syntax discussed in the [Regular Expressions](#ch007.xhtml_regular-expressions) section for the `grep` command applies for `sed` as well.

```
[](#cb297-1)# replace all sequences of non-digit characters with '-'
[](#cb297-2)$ echo 'Sample123string42with777numbers' | sed -E 's/[^0-9]+/-/g'
[](#cb297-3)-123-42-777-
[](#cb297-4)
[](#cb297-5)# replace numbers >= 100 which can have optional leading zeros
[](#cb297-6)$ echo '0501 035 154 12 26 98234' | sed -E 's/\b0*[1-9][0-9]{2,}\b/X/g'
[](#cb297-7)X 035 X 12 26 X
[](#cb297-8)
[](#cb297-9)# reduce \\ to single \ and delete if it is a single \
[](#cb297-10)$ echo '\[\] and \\w and \[a-zA-Z0-9\_\]' | sed -E 's/(\\?)\\/\1/g'
[](#cb297-11)[] and \w and [a-zA-Z0-9_]
[](#cb297-12)
[](#cb297-13)# remove two or more duplicate words that are separated by a space
[](#cb297-14)# \b prevents false matches like 'the theatre', 'sand and stone' etc
[](#cb297-15)$ echo 'aa a a a 42 f_1 f_1 f_13.14' | sed -E 's/\b(\w+)( \1)+\b/\1/g'
[](#cb297-16)aa a 42 f_1 f_13.14
[](#cb297-17)
[](#cb297-18)# & backreferences the matched portion
[](#cb297-19)# \u changes the next character to uppercase
[](#cb297-20)$ echo 'hello there. how are you?' | sed 's/\b\w/\u&/g'
[](#cb297-21)Hello There. How Are You?
[](#cb297-22)
[](#cb297-23)# replace only the third matching occurrence
[](#cb297-24)$ echo 'apple:123:banana:fig' | sed 's/:/-/3'
[](#cb297-25)apple:123:banana-fig
[](#cb297-26)# change all ':' to ',' only from the second occurrence
[](#cb297-27)$ echo 'apple:123:banana:fig' | sed 's/:/,/2g'
[](#cb297-28)apple:123,banana,fig
```

The `/` character is idiomatically used as the regexp delimiter. But any character other than `\` and the newline character can be used instead. This helps to avoid or reduce the need for escaping delimiter characters.

```
[](#cb298-1)$ echo '/home/learnbyexample/reports' | sed 's#/home/learnbyexample/#~/#'
[](#cb298-2)~/reports
[](#cb298-3)
[](#cb298-4)$ echo 'home path is:' | sed 's,$, '"$HOME"','
[](#cb298-5)home path is: /home/learnbyexample
```

### Further Reading

*   My ebook [GNU SED](https://github.com/learnbyexample/learn_gnused)
    *   See also my blog post [GNU BRE/ERE cheatsheet](https://learnbyexample.github.io/gnu-bre-ere-cheatsheet/)
*   [unix.stackexchange: common search and replace examples with sed and other tools](https://unix.stackexchange.com/q/112023/109046)

## awk

`awk` is a programming language and primarily used for field based processing. `awk` also provides filtering capabilities like those supported by `grep` and `sed` along with some more nifty features. And similar to many command line utilities, `awk` can accept input from both `stdin` and files.

### Regexp filtering

To make it easier to use programming features from the command line, there are several shortcuts, for example:

*   `awk '/regexp/'` is a shortcut for `awk '$0 ~ /regexp/{print $0}'`
*   `awk '!/regexp/'` is a shortcut for `awk '$0 !~ /regexp/{print $0}'`

```
[](#cb299-1)# same as: grep 'at' and sed -n '/at/p'
[](#cb299-2)$ printf 'gate\napple\nwhat\nkite\n' | awk '/at/'
[](#cb299-3)gate
[](#cb299-4)what
[](#cb299-5)
[](#cb299-6)# same as: grep -v 'e' and sed -n '/e/!p'
[](#cb299-7)$ printf 'gate\napple\nwhat\nkite\n' | awk '!/e/'
[](#cb299-8)what
```

### Awk special variables

Brief description for some of the special variables are given below:

*   `$0` contains input record content
*   `$1` first field
*   `$2` second field and so on
*   `FS` input field separator
*   `OFS` output field separator
*   `NF` number of fields
*   `RS` input record separator
*   `ORS` output record separator
*   `NR` number of records (i.e. line number)

### Default field processing

`awk` automatically splits input into fields based on one or more sequence of **space** or **tab** or **newline** characters. In addition, any of these three characters at the start or end of input gets trimmed and won't be part of field contents. The fields are accessible using `$N` where `N` is the field number you need. You can also pass an expression instead of numeric literal to specify the field required.

Here are some examples:

```
[](#cb300-1)$ cat table.txt
[](#cb300-2)brown bread mat hair 42
[](#cb300-3)blue cake mug shirt -7
[](#cb300-4)yellow banana window shoes 3.14
[](#cb300-5)
[](#cb300-6)# print the second field of each input line
[](#cb300-7)$ awk '{print $2}' table.txt
[](#cb300-8)bread
[](#cb300-9)cake
[](#cb300-10)banana
[](#cb300-11)
[](#cb300-12)# print lines only if the last field is a negative number
[](#cb300-13)$ awk '$NF<0' table.txt
[](#cb300-14)blue cake mug shirt -7
[](#cb300-15)
[](#cb300-16)# change 'b' to 'B' only for the first field
[](#cb300-17)# gsub() is like the sed substitution command with 'g' flag
[](#cb300-18)# use sub() when 'g' flag is not needed
[](#cb300-19)$ awk '{gsub(/b/, "B", $1)} 1' table.txt
[](#cb300-20)Brown bread mat hair 42
[](#cb300-21)Blue cake mug shirt -7
[](#cb300-22)yellow banana window shoes 3.14
```

### Condition and Action

The examples so far have used a few different ways to construct a typical `awk` one-liner. If you haven't yet grasped the syntax, this generic structure might help:

```
[](#cb301-1)awk 'cond1{action1} cond2{action2} ... condN{actionN}'
```

If a condition isn't provided, the action is always executed. Within a block, you can provide multiple statements separated by a semicolon character. If action isn't provided, then by default, contents of `$0` variable is printed if the condition evaluates to *true*. When action isn't present, you can use semicolon to terminate the condition and start another `condX{actionX}` snippet.

You can use a `BEGIN{}` block when you need to execute something before the input is read and an `END{}` block to execute something after all of the input has been processed.

```
[](#cb302-1)$ seq 2 | awk 'BEGIN{print "---"} 1; END{print "%%%"}'
[](#cb302-2)---
[](#cb302-3)1
[](#cb302-4)2
[](#cb302-5)%%%
```

### Regexp field processing

As seen earlier, `awk` automatically splits input into fields (based on space/tab/newline characters) which are accessible using `$N` where `N` is the field number you need. You can use the `-F` option or `FS` variable to set a regexp based field separator. Use `OFS` variable to set the output field separator.

```
[](#cb303-1)$ echo 'goal:amazing:whistle:kwality' | awk -F: '{print $1}'
[](#cb303-2)goal
[](#cb303-3)$ echo 'Sample123string42with777numbers' | awk -F'[a-zA-Z]+' '{print $2}'
[](#cb303-4)123
[](#cb303-5)
[](#cb303-6)$ s='Sample123string42with777numbers'
[](#cb303-7)# -v option helps you set a value for the given variable
[](#cb303-8)$ echo "$s" | awk -F'[0-9]+' -v OFS=, '{print $1, $(NF-1)}'
[](#cb303-9)Sample,with
```

You can use `FPAT` to define what characters should make up the fields. `FS` splits the input record whereas `FPAT` matches the fields. The below example finds fields that are enclosed within double quotes or made up of non-comma characters.

```
[](#cb304-1)$ s='eagle,"fox,42",bee,frog'
[](#cb304-2)$ echo "$s" | awk -v FPAT='"[^"]*"|[^,]*' '{print $2}'
[](#cb304-3)"fox,42"
```

### Record separators

By default, newline is used as input and output record separators. You can change them using the `RS` and `ORS` variables.

```
[](#cb305-1)# print records containing 'i' as well as 't'
[](#cb305-2)$ printf 'Sample123string42with777numbers' | awk -v RS='[0-9]+' '/i/ && /t/'
[](#cb305-3)string
[](#cb305-4)with
[](#cb305-5)
[](#cb305-6)# empty RS is paragraph mode, uses two or more newlines as separator
[](#cb305-7)$ printf 'apple\nbanana\nfig\n\n\n123\n456' | awk -v RS= 'NR==1'
[](#cb305-8)apple
[](#cb305-9)banana
[](#cb305-10)fig
[](#cb305-11)
[](#cb305-12)# change ORS depending on some condition
[](#cb305-13)$ seq 9 | awk '{ORS = NR%3 ? "-" : "\n"} 1'
[](#cb305-14)1-2-3
[](#cb305-15)4-5-6
[](#cb305-16)7-8-9
```

### State machines

The `condX{actionX}` shortcut makes it easy to code state machines concisely, which is useful to solve problems that depend on contents of multiple records.

Here's an example of printing the matching line as well as `c` number of lines that follow:

```
[](#cb306-1)# same as: grep --no-group-separator -A1 'blue'
[](#cb306-2)# print matching line as well as the one that follows it
[](#cb306-3)$ printf 'red\nblue\ngreen\nteal\n' | awk -v c=1 '/blue/{n=c+1} n && n--'
[](#cb306-4)blue
[](#cb306-5)green
[](#cb306-6)
[](#cb306-7)# print matching line as well as two lines that follow
[](#cb306-8)$ printf 'red\nblue\ngreen\nteal\n' | awk -v c=2 '/blue/{n=c+1} n && n--'
[](#cb306-9)blue
[](#cb306-10)green
[](#cb306-11)teal
```

Consider the following input file that has records bounded by distinct markers (lines containing `start` and `end`):

```
[](#cb307-1)$ cat uniform.txt
[](#cb307-2)mango
[](#cb307-3)icecream
[](#cb307-4)--start 1--
[](#cb307-5)1234
[](#cb307-6)6789
[](#cb307-7)**end 1**
[](#cb307-8)how are you
[](#cb307-9)have a nice day
[](#cb307-10)--start 2--
[](#cb307-11)a
[](#cb307-12)b
[](#cb307-13)c
[](#cb307-14)**end 2**
[](#cb307-15)par,far,mar,tar
```

Here are some examples of processing such bounded records:

```
[](#cb308-1)# same as: sed -n '/start/,/end/p' uniform.txt
[](#cb308-2)$ awk '/start/{f=1} f; /end/{f=0}' uniform.txt
[](#cb308-3)--start 1--
[](#cb308-4)1234
[](#cb308-5)6789
[](#cb308-6)**end 1**
[](#cb308-7)--start 2--
[](#cb308-8)a
[](#cb308-9)b
[](#cb308-10)c
[](#cb308-11)**end 2**
[](#cb308-12)
[](#cb308-13)# you can re-arrange and invert the conditions to create other combinations
[](#cb308-14)# for example, exclude ending match
[](#cb308-15)$ awk '/start/{f=1} /end/{f=0} f' uniform.txt
[](#cb308-16)--start 1--
[](#cb308-17)1234
[](#cb308-18)6789
[](#cb308-19)--start 2--
[](#cb308-20)a
[](#cb308-21)b
[](#cb308-22)c
```

Here's an example of printing two consecutive records only if the first record contains `ar` and the second one contains `nice`:

```
[](#cb309-1)$ awk 'p ~ /ar/ && /nice/{print p ORS $0} {p=$0}' uniform.txt
[](#cb309-2)how are you
[](#cb309-3)have a nice day
```

### Two files processing

The *key* features used in the solution below:

*   For two files as input, `NR==FNR` will be *true* only when the first file is being processed
    *   `FNR` is record number like `NR` but resets for each input file
*   `next` will skip the rest of the code and fetch the next record
*   `a[$0]` by itself is a valid statement. It will create an uninitialized element in array `a` with `$0` as the key (if the key doesn't exist yet)
*   `$0 in a` checks if the given string (`$0` here) exists as a key in the array `a`

```
[](#cb310-1)# common lines, same as: grep -Fxf c1.txt c2.txt
[](#cb310-2)$ awk 'NR==FNR{a[$0]; next} $0 in a' c1.txt c2.txt
[](#cb310-3)Blue
[](#cb310-4)Orange
[](#cb310-5)Red
[](#cb310-6)White
[](#cb310-7)
[](#cb310-8)# lines present in c2.txt but not in c1.txt
[](#cb310-9)$ awk 'NR==FNR{a[$0]; next} !($0 in a)' c1.txt c2.txt
[](#cb310-10)Black
[](#cb310-11)Green
[](#cb310-12)Pink
```

> ![warning](media/file7.svg) Note that the `NR==FNR` logic will fail if the first file is empty. See [this unix.stackexchange thread](https://unix.stackexchange.com/a/237110/109046) for workarounds.

### Removing duplicates

`awk '!a[$0]++'` is one of the most famous `awk` one-liners. It eliminates line based duplicates while retaining input order. The following example shows this feature in action along with an illustration of how the logic works.

```
[](#cb311-1)$ cat purchases.txt
[](#cb311-2)coffee
[](#cb311-3)tea
[](#cb311-4)washing powder
[](#cb311-5)coffee
[](#cb311-6)toothpaste
[](#cb311-7)tea
[](#cb311-8)soap
[](#cb311-9)tea
[](#cb311-10)
[](#cb311-11)$ awk '{print +a[$0] "\t" $0; a[$0]++}' purchases.txt
[](#cb311-12)0       coffee
[](#cb311-13)0       tea
[](#cb311-14)0       washing powder
[](#cb311-15)1       coffee
[](#cb311-16)0       toothpaste
[](#cb311-17)1       tea
[](#cb311-18)0       soap
[](#cb311-19)2       tea
[](#cb311-20)
[](#cb311-21)# only those entries with zero in first column will be retained
[](#cb311-22)$ awk '!a[$0]++' purchases.txt
[](#cb311-23)coffee
[](#cb311-24)tea
[](#cb311-25)washing powder
[](#cb311-26)toothpaste
[](#cb311-27)soap
```

### Further Reading

*   My ebook [GNU AWK](https://github.com/learnbyexample/learn_gnuawk)
    *   See also my blog post [GNU BRE/ERE cheatsheet](https://learnbyexample.github.io/gnu-bre-ere-cheatsheet/)
*   [Online gawk manual](https://www.gnu.org/software/gawk/manual/)

## perl

Perl is a scripting language with plenty of builtin features and a strong ecosystem. Perl one-liners can be used for text processing, similar to `grep`, `sed`, `awk` and more. And similar to many command line utilities, `perl` can accept input from both `stdin` and file arguments.

### Basic one-liners

```
[](#cb312-1)# print all lines containing 'at'
[](#cb312-2)# same as: grep 'at' and sed -n '/at/p' and awk '/at/'
[](#cb312-3)$ printf 'gate\napple\nwhat\nkite\n' | perl -ne 'print if /at/'
[](#cb312-4)gate
[](#cb312-5)what
[](#cb312-6)
[](#cb312-7)# print all lines NOT containing 'e'
[](#cb312-8)# same as: grep -v 'e' and sed -n '/e/!p' and awk '!/e/'
[](#cb312-9)$ printf 'gate\napple\nwhat\nkite\n' | perl -ne 'print if !/e/'
[](#cb312-10)what
```

The `-e` option accepts code as a command line argument. Many shortcuts are available to reduce the amount of typing needed. In the above examples, a regular expression has been used to filter the input. When the input string isn't specified, the test is performed against special variable `$_`, which has the contents of the current input line. `$_` is also the default argument for many functions like `print` and `length`. To summarize:

*   `/REGEXP/FLAGS` is a shortcut for `$_ =~ m/REGEXP/FLAGS`
*   `!/REGEXP/FLAGS` is a shortcut for `$_ !~ m/REGEXP/FLAGS`

In the examples below, `-p` option is used instead of `-n` option. This helps to automatically print the value of `$_` after processing each input line.

```
[](#cb313-1)# same as: sed 's/:/-/' and awk '{sub(/:/, "-")} 1'
[](#cb313-2)$ printf '1:2:3:4\na:b:c:d\n' | perl -pe 's/:/-/'
[](#cb313-3)1-2:3:4
[](#cb313-4)a-b:c:d
[](#cb313-5)
[](#cb313-6)# same as: sed 's/:/-/g' and awk '{gsub(/:/, "-")} 1'
[](#cb313-7)$ printf '1:2:3:4\na:b:c:d\n' | perl -pe 's/:/-/g'
[](#cb313-8)1-2-3-4
[](#cb313-9)a-b-c-d
```

> ![info](media/file0.svg) Similar to `sed`, you can use the `-i` option for inplace editing.

### Perl special variables

Brief description for some of the special variables are given below:

*   `$_` contains input record content
*   `@F` array containing fields (with `-a` and `-F` options)
    *   `$F[0]` first field
    *   `$F[1]` second field and so on
    *   `$F[-1]` last field
    *   `$F[-2]` second last field and so on
    *   `$#F` index of the last field
*   `$.` number of records (i.e. line number)
*   `$1` backreference to the first capture group
*   `$2` backreference to the second capture group and so on
*   `$&` backreference to the entire matched portion

You'll see examples using such variables in the sections to follow.

### Auto split

Here are some examples based on specific fields rather than the entire line. The `-a` option will cause the input line to be split based on whitespaces and the field contents can be accessed using the `@F` special array variable. Leading and trailing whitespaces will be suppressed, so there's no possibility of empty fields.

```
[](#cb314-1)$ cat table.txt
[](#cb314-2)brown bread mat hair 42
[](#cb314-3)blue cake mug shirt -7
[](#cb314-4)yellow banana window shoes 3.14
[](#cb314-5)
[](#cb314-6)# same as: awk '{print $2}' table.txt
[](#cb314-7)$ perl -lane 'print $F[1]' table.txt
[](#cb314-8)bread
[](#cb314-9)cake
[](#cb314-10)banana
[](#cb314-11)
[](#cb314-12)# same as: awk '$NF<0' table.txt
[](#cb314-13)$ perl -lane 'print if $F[-1] < 0' table.txt
[](#cb314-14)blue cake mug shirt -7
[](#cb314-15)
[](#cb314-16)# same as: awk '{gsub(/b/, "B", $1)} 1' table.txt
[](#cb314-17)$ perl -lane '$F[0] =~ s/b/B/g; print "@F"' table.txt
[](#cb314-18)Brown bread mat hair 42
[](#cb314-19)Blue cake mug shirt -7
[](#cb314-20)yellow banana window shoes 3.14
```

When you use an array within double quotes (like `"@F"` in the example above), the fields will be printed with a space character in between. The `join` function is one of the ways to print the contents of an array with a custom field separator. Here's an example:

```
[](#cb315-1)# print contents of @F array with colon as the separator
[](#cb315-2)$ perl -lane 'print join ":", @F' table.txt
[](#cb315-3)brown:bread:mat:hair:42
[](#cb315-4)blue:cake:mug:shirt:-7
[](#cb315-5)yellow:banana:window:shoes:3.14
```

> ![info](media/file0.svg) In the above examples, the `-l` option has been used to remove the record separator (which is newline by default) from the input line. The record separator thus removed is added back when the `print` function is used.

### Regexp field separator

You can use the `-F` option to specify a regexp pattern for input field separation.

```
[](#cb316-1)$ echo 'apple,banana,cherry' | perl -F, -lane 'print $F[1]'
[](#cb316-2)banana
[](#cb316-3)
[](#cb316-4)$ s='Sample123string42with777numbers'
[](#cb316-5)$ echo "$s" | perl -F'\d+' -lane 'print join ",", @F'
[](#cb316-6)Sample,string,with,numbers
```

### Powerful features

I reach for Perl over `grep`, `sed` and `awk` when I need powerful regexp features and make use of the vast builtin functions and libraries.

Here are some examples showing regexp features not present in BRE/ERE:

```
[](#cb317-1)# reverse lowercase alphabets at the end of input lines
[](#cb317-2)# 'e' flag allows you to use Perl code in the replacement section
[](#cb317-3)$ echo 'fig 42apples' | perl -pe 's/[a-z]+$/reverse $&/e'
[](#cb317-4)fig 42selppa
[](#cb317-5)
[](#cb317-6)# replace arithmetic expressions with their results
[](#cb317-7)$ echo '42*10 200+100 22/7' | perl -pe 's|\d+[+/*-]\d+|$&|gee'
[](#cb317-8)420 300 3.14285714285714
[](#cb317-9)
[](#cb317-10)# exclude terms in the search pattern
[](#cb317-11)$ s='orange apple appleseed'
[](#cb317-12)$ echo "$s" | perl -pe 's#\bapple\b(*SKIP)(*F)|\w+#($&)#g'
[](#cb317-13)(orange) apple (appleseed)
```

And here are some examples showing off builtin features:

```
[](#cb318-1)# filter fields containing 'in' or 'it' or 'is'
[](#cb318-2)$ s='goal:amazing:42:whistle:kwality:3.14'
[](#cb318-3)$ echo "$s" | perl -F: -lane 'print join ":", grep {/i[nts]/} @F'
[](#cb318-4)amazing:whistle:kwality
[](#cb318-5)
[](#cb318-6)# sort numbers in ascending order
[](#cb318-7)# use {$b <=> $a} for descending order
[](#cb318-8)$ echo '23 756 -983 5' | perl -lane 'print join " ", sort {$a <=> $b} @F'
[](#cb318-9)-983 5 23 756
[](#cb318-10)
[](#cb318-11)# sort strings in ascending order
[](#cb318-12)$ s='floor bat to dubious four'
[](#cb318-13)$ echo "$s" | perl -lane 'print join ":", sort @F'
[](#cb318-14)bat:dubious:floor:four:to
[](#cb318-15)
[](#cb318-16)# unique fields, maintains input order of elements
[](#cb318-17)# -M option helps you load modules
[](#cb318-18)$ s='3,b,a,3,c,d,1,d,c,2,2,2,3,1,b'
[](#cb318-19)$ echo "$s" | perl -MList::Util=uniq -F, -lane 'print join ",", uniq @F'
[](#cb318-20)3,b,a,c,d,1,2
```

### Further Reading

*   [perldoc: Perl introduction](https://perldoc.perl.org/perlintro)
*   [perldoc: Regexp tutorial](https://perldoc.perl.org/perlretut)
*   My ebook [Perl one-liners](https://github.com/learnbyexample/learn_perl_oneliners)

## Exercises

> ![info](media/file0.svg) Use [example_files/text_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files/text_files) directory for input files used in the following exercises.

**1)** Replace all occurrences of `0xA0` with `0x50` and `0xFF` with `0x7F` for the given input.

```
[](#cb319-1)$ printf 'a1:0xA0, a2:0xA0A1\nb1:0xFF, b2:0xBE\n'
[](#cb319-2)a1:0xA0, a2:0xA0A1
[](#cb319-3)b1:0xFF, b2:0xBE
[](#cb319-4)
[](#cb319-5)$ printf 'a1:0xA0, a2:0xA0A1\nb1:0xFF, b2:0xBE\n' | sed # ???
[](#cb319-6)a1:0x50, a2:0x50A1
[](#cb319-7)b1:0x7F, b2:0xBE
```

**2)** Remove only the third line from the given input.

```
[](#cb320-1)$ seq 34 37 | # ???
[](#cb320-2)34
[](#cb320-3)35
[](#cb320-4)37
```

**3)** For the input file `sample.txt`, display all lines that contain `it` but not `do`.

```
[](#cb321-1)# ???
[](#cb321-2) 7) Believe it
```

**4)** For the input file `purchases.txt`, delete all lines containing `tea`. Also, replace all occurrences of `coffee` with `milk`. Write back the changes to the input file itself. The original contents should get saved to `purchases.txt.orig`. Afterwards, restore the contents from this backup file.

```
[](#cb322-1)# make the changes
[](#cb322-2)# ???
[](#cb322-3)$ ls purchases*
[](#cb322-4)purchases.txt  purchases.txt.orig
[](#cb322-5)$ cat purchases.txt
[](#cb322-6)milk
[](#cb322-7)washing powder
[](#cb322-8)milk
[](#cb322-9)toothpaste
[](#cb322-10)soap
[](#cb322-11)
[](#cb322-12)# restore the contents
[](#cb322-13)# ???
[](#cb322-14)$ ls purchases*
[](#cb322-15)purchases.txt
[](#cb322-16)$ cat purchases.txt
[](#cb322-17)coffee
[](#cb322-18)tea
[](#cb322-19)washing powder
[](#cb322-20)coffee
[](#cb322-21)toothpaste
[](#cb322-22)tea
[](#cb322-23)soap
[](#cb322-24)tea
```

**5)** For the input file `sample.txt`, display all lines from the start of the file till the first occurrence of `are`.

```
[](#cb323-1)# ???
[](#cb323-2) 1) Hello World
[](#cb323-3) 2) 
[](#cb323-4) 3) Hi there
[](#cb323-5) 4) How are you
```

**6)** Delete all groups of lines from a line containing `start` to a line containing `end` for the `uniform.txt` input file.

```
[](#cb324-1)# ???
[](#cb324-2)mango
[](#cb324-3)icecream
[](#cb324-4)how are you
[](#cb324-5)have a nice day
[](#cb324-6)par,far,mar,tar
```

**7)** Replace all occurrences of `42` with `[42]` unless it is at the edge of a word.

```
[](#cb325-1)$ echo 'hi42bye nice421423 bad42 cool_4242a 42c' | sed # ???
[](#cb325-2)hi[42]bye nice[42]1[42]3 bad42 cool_[42][42]a 42c
```

**8)** Replace all whole words with `X` that start and end with the same word character.

```
[](#cb326-1)$ echo 'oreo not a _a2_ roar took 22' | sed # ???
[](#cb326-2)X not X X X took X
```

**9)** For the input file `anchors.txt`, convert markdown anchors to hyperlinks as shown below.

```
[](#cb327-1)$ cat anchors.txt
[](#cb327-2)# <a name="regular-expressions"></a>Regular Expressions
[](#cb327-3)## <a name="subexpression-calls"></a>Subexpression calls
[](#cb327-4)## <a name="the-dot-meta-character"></a>The dot meta character
[](#cb327-5)
[](#cb327-6)$ sed # ???
[](#cb327-7)[Regular Expressions](#regular-expressions)
[](#cb327-8)[Subexpression calls](#subexpression-calls)
[](#cb327-9)[The dot meta character](#the-dot-meta-character)
```

**10)** Replace all occurrences of `e` with `3` except the first two matches.

```
[](#cb328-1)$ echo 'asset sets tests site' | sed # ???
[](#cb328-2)asset sets t3sts sit3
[](#cb328-3)
[](#cb328-4)$ echo 'sample item teem eel' | sed # ???
[](#cb328-5)sample item t33m 33l
```

**11)** The below sample strings use `,` as the delimiter and the field values can be empty as well. Use `sed` to replace only the third field with `42`.

```
[](#cb329-1)$ echo 'lion,,ant,road,neon' | sed # ???
[](#cb329-2)lion,,42,road,neon
[](#cb329-3)$ echo ',,,' | sed # ???
[](#cb329-4),,42,
```

**12)** For the input file `table.txt`, calculate and display the product of numbers in the last field of each line. Consider space as the field separator for this file.

```
[](#cb330-1)$ cat table.txt
[](#cb330-2)brown bread mat hair 42
[](#cb330-3)blue cake mug shirt -7
[](#cb330-4)yellow banana window shoes 3.14
[](#cb330-5)
[](#cb330-6)# ???
[](#cb330-7)-923.16
```

**13)** Extract the contents between `()` or `)(` from each of the input lines. Assume that the `()` characters will be present only once every line.

```
[](#cb331-1)$ printf 'apple(ice)pie\n(almond)pista\nyo)yoyo(yo\n'
[](#cb331-2)apple(ice)pie
[](#cb331-3)(almond)pista
[](#cb331-4)yo)yoyo(yo
[](#cb331-5)
[](#cb331-6)$ printf 'apple(ice)pie\n(almond)pista\nyo)yoyo(yo\n' | awk # ???
[](#cb331-7)ice
[](#cb331-8)almond
[](#cb331-9)yoyo
```

**14)** For the input file `scores.csv`, display the `Name` and `Physics` fields in the format shown below.

```
[](#cb332-1)$ cat scores.csv
[](#cb332-2)Name,Maths,Physics,Chemistry
[](#cb332-3)Ith,100,100,100
[](#cb332-4)Cy,97,98,95
[](#cb332-5)Lin,78,83,80
[](#cb332-6)
[](#cb332-7)# ???
[](#cb332-8)Name:Physics
[](#cb332-9)Ith:100
[](#cb332-10)Cy:98
[](#cb332-11)Lin:83
```

**15)** Extract and display third and first words in the format shown below.

```
[](#cb333-1)$ echo '%whole(Hello)--{doubt}==ado==' | # ???
[](#cb333-2)doubt:whole
[](#cb333-3)
[](#cb333-4)$ echo 'just,\joint*,concession_42<=nice' | # ???
[](#cb333-5)concession_42:just
```

**16)** For the input file `scores.csv`, add another column named `GP` which is calculated out of `100` by giving `50%` weightage to `Maths` and `25%` each for `Physics` and `Chemistry`.

```
[](#cb334-1)$ awk # ???
[](#cb334-2)Name,Maths,Physics,Chemistry,GP
[](#cb334-3)Ith,100,100,100,100
[](#cb334-4)Cy,97,98,95,96.75
[](#cb334-5)Lin,78,83,80,79.75
```

**17)** From the `para.txt` input file, display all paragraphs containing any digit character.

```
[](#cb335-1)$ cat para.txt
[](#cb335-2)hi there
[](#cb335-3)how are you
[](#cb335-4)
[](#cb335-5)2 apples
[](#cb335-6)12 bananas
[](#cb335-7)
[](#cb335-8)
[](#cb335-9)blue sky
[](#cb335-10)yellow sun
[](#cb335-11)brown earth
[](#cb335-12)
[](#cb335-13)$ awk # ???
[](#cb335-14)2 apples
[](#cb335-15)12 bananas
```

**18)** Input has the ASCII NUL character as the record separator. Change it to dot and newline characters as shown below.

```
[](#cb336-1)$ printf 'apple\npie\0banana\ncherry\0' | awk # ???
[](#cb336-2)apple
[](#cb336-3)pie.
[](#cb336-4)banana
[](#cb336-5)cherry.
```

**19)** For the input file `sample.txt`, print a matching line containing `do` only if `you` is found two lines before. For example, if `do` is found on line number 10 and 8th line contains `you`, then 10th line should be printed.

```
[](#cb337-1)# ???
[](#cb337-2) 6) Just do-it
```

**20)** For the input file `blocks.txt`, extract contents from a line containing exactly `%=%=` until but not including the next such line. The block to be extracted is indicated by variable `n` passed via the `-v` option.

```
[](#cb338-1)$ cat blocks.txt
[](#cb338-2)%=%=
[](#cb338-3)apple
[](#cb338-4)banana
[](#cb338-5)%=%=
[](#cb338-6)brown
[](#cb338-7)green
[](#cb338-8)
[](#cb338-9)$ awk -v n=1 # ???
[](#cb338-10)%=%=
[](#cb338-11)apple
[](#cb338-12)banana
[](#cb338-13)$ awk -v n=2 # ???
[](#cb338-14)%=%=
[](#cb338-15)brown
[](#cb338-16)green
```

**21)** Display lines present in `c1.txt` but not in `c2.txt` using the `awk` command.

```
[](#cb339-1)$ awk # ???
[](#cb339-2)Brown
[](#cb339-3)Purple
[](#cb339-4)Teal
```

**22)** Display lines from `scores.csv` by matching the first field based on a list of names from the `names.txt` file.

```
[](#cb340-1)$ printf 'Ith\nLin\n' > names.txt
[](#cb340-2)
[](#cb340-3)$ awk # ???
[](#cb340-4)Ith,100,100,100
[](#cb340-5)Lin,78,83,80
[](#cb340-6)
[](#cb340-7)$ rm names.txt
```

**23)** Retain only the first copy of duplicate lines from the `duplicates.txt` input file. Use only the contents of the last field for determining duplicates.

```
[](#cb341-1)$ cat duplicates.txt
[](#cb341-2)brown,toy,bread,42
[](#cb341-3)dark red,ruby,rose,111
[](#cb341-4)blue,ruby,water,333
[](#cb341-5)dark red,sky,rose,555
[](#cb341-6)yellow,toy,flower,333
[](#cb341-7)white,sky,bread,111
[](#cb341-8)light red,purse,rose,333
[](#cb341-9)
[](#cb341-10)# ???
[](#cb341-11)brown,toy,bread,42
[](#cb341-12)dark red,ruby,rose,111
[](#cb341-13)blue,ruby,water,333
[](#cb341-14)dark red,sky,rose,555
```

**24)** For the input file `table.txt`, print input lines if the second field starts with `b`. Construct solutions using `awk` and `perl`.

```
[](#cb342-1)$ awk # ???
[](#cb342-2)brown bread mat hair 42
[](#cb342-3)yellow banana window shoes 3.14
[](#cb342-4)
[](#cb342-5)$ perl # ???
[](#cb342-6)brown bread mat hair 42
[](#cb342-7)yellow banana window shoes 3.14
```

**25)** For the input file `table.txt`, retain only the second last field. Write back the changes to the input file itself. The original contents should get saved to `table.txt.bkp`. Afterwards, restore the contents from this backup file.

```
[](#cb343-1)# make the changes
[](#cb343-2)$ perl # ???
[](#cb343-3)$ ls table*
[](#cb343-4)table.txt  table.txt.bkp
[](#cb343-5)$ cat table.txt
[](#cb343-6)hair
[](#cb343-7)shirt
[](#cb343-8)shoes
[](#cb343-9)
[](#cb343-10)# restore the contents
[](#cb343-11)# ???
[](#cb343-12)$ ls table*
[](#cb343-13)table.txt
[](#cb343-14)$ cat table.txt
[](#cb343-15)brown bread mat hair 42
[](#cb343-16)blue cake mug shirt -7
[](#cb343-17)yellow banana window shoes 3.14
```

**26)** Reverse the first field contents of `table.txt` input file.

```
[](#cb344-1)# ???
[](#cb344-2)nworb bread mat hair 42
[](#cb344-3)eulb cake mug shirt -7
[](#cb344-4)wolley banana window shoes 3.14
```

**27)** Sort the given comma separated input lexicographically. Change the output field separator to a `:` character.

```
[](#cb345-1)$ ip='floor,bat,to,dubious,four'
[](#cb345-2)$ echo "$ip" | perl # ???
[](#cb345-3)bat:dubious:floor:four:to
```

**28)** Filter fields containing digit characters.

```
[](#cb346-1)$ ip='5pearl 42 east 1337 raku_6 lion 3.14'
[](#cb346-2)$ echo "$ip" | perl # ???
[](#cb346-3)5pearl 42 1337 raku_6 3.14
```

**29)** The input shown below has several words ending with digit characters. Change the words containing `test` to match the output shown below. That is, renumber the matching portions to `1`, `2`, etc. Words not containing `test` should not be changed.

```
[](#cb347-1)$ ip='test_12:test123\nanother_test_4,no_42\n'
[](#cb347-2)$ printf '%b' "$ip"
[](#cb347-3)test_12:test123
[](#cb347-4)another_test_4,no_42
[](#cb347-5)
[](#cb347-6)$ printf '%b' "$ip" | perl # ???
[](#cb347-7)test_1:test2
[](#cb347-8)another_test_3,no_42
```

**30)** For the input file `table.txt`, change contents of the third field to all uppercase. Construct solutions using `sed`, `awk` and `perl`.

```
[](#cb348-1)$ sed # ???
[](#cb348-2)brown bread MAT hair 42
[](#cb348-3)blue cake MUG shirt -7
[](#cb348-4)yellow banana WINDOW shoes 3.14
[](#cb348-5)
[](#cb348-6)$ awk # ???
[](#cb348-7)brown bread MAT hair 42
[](#cb348-8)blue cake MUG shirt -7
[](#cb348-9)yellow banana WINDOW shoes 3.14
[](#cb348-10)
[](#cb348-11)$ perl # ???
[](#cb348-12)brown bread MAT hair 42
[](#cb348-13)blue cake MUG shirt -7
[](#cb348-14)yellow banana WINDOW shoes 3.14
```

# Sorting Stuff

In this chapter, you'll learn how to sort input based on various criteria. And then, you'll learn about tools that typically require sorted input for performing operations like finding unique entries, comparing two files line wise and so on.

> ![info](media/file0.svg) The [example_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files) directory has the sample input files used in this chapter.

## sort

As the name implies, this command is used to sort the contents of input files. Alphabetic sort and numeric sort? Possible. How about sorting a particular column? Possible. Prioritized multiple sorting order? Possible. Randomize? Unique? Lots of features supported by this powerful command.

### Common options

Commonly used options are shown below. Examples will be discussed in later sections.

*   `-n` sort numerically
*   `-g` general numeric sort
*   `-V` version sort (aware of numbers within text)
*   `-h` sort human readable numbers (ex: 4K, 3M, 12G, etc)
*   `-k` sort via key (column sorting)
*   `-t` single byte character as field separator (default is non-blank to blank transition)
*   `-u` sort uniquely
*   `-R` random sort
*   `-r` reverse the sort output
*   `-o` redirect sorted result to specified filename (ex: for inplace sorting)

### Default sort

By default, `sort` orders the input [lexicographically](https://en.wikipedia.org/wiki/Lexicographic_order) in ascending order. You can use the `-r` option to reverse the results.

```
[](#cb349-1)# default sort 
[](#cb349-2)$ printf 'banana\ncherry\napple' | sort
[](#cb349-3)apple
[](#cb349-4)banana
[](#cb349-5)cherry
[](#cb349-6)
[](#cb349-7)# sort and then display the results in reversed order
[](#cb349-8)$ printf 'peace\nrest\nquiet' | sort -r
[](#cb349-9)rest
[](#cb349-10)quiet
[](#cb349-11)peace
```

> ![info](media/file0.svg) Use `-f` option if you want to ignore case. See also [coreutils FAQ: Sort does not sort in normal order!](https://www.gnu.org/software/coreutils/faq/#Sort-does-not-sort-in-normal-order_0021).

### Numerical sort

There are several ways to deal with input containing numbers:

```
[](#cb350-1)$ printf '20\n2\n3' | sort -n
[](#cb350-2)2
[](#cb350-3)3
[](#cb350-4)20
[](#cb350-5)
[](#cb350-6)# sorting human readable numbers
[](#cb350-7)$ sort -hr file_size.txt
[](#cb350-8)1.4G    games
[](#cb350-9)316M    projects
[](#cb350-10)746K    report.log
[](#cb350-11)104K    power.log
[](#cb350-12)20K     sample.txt
[](#cb350-13)
[](#cb350-14)# version sort
[](#cb350-15)$ sort -V timings.txt
[](#cb350-16)3m20.058s
[](#cb350-17)3m42.833s
[](#cb350-18)4m3.083s
[](#cb350-19)4m11.130s
[](#cb350-20)5m35.363s
```

### Unique sort

The `-u` option will keep only the first copy of lines that are deemed to be equal.

```
[](#cb351-1)# -f option ignores case differences
[](#cb351-2)$ printf 'CAT\nbat\ncat\ncar\nbat\n' | sort -fu
[](#cb351-3)bat
[](#cb351-4)car
[](#cb351-5)CAT
```

### Column sort

The `-k` option allows you to sort based on specific column(s) instead of the entire input line. By default, the empty string between non-blank and blank characters is considered as the separator. This option accepts arguments in various ways. You can specify starting and ending column numbers separated by a comma. If you specify only the starting column, the last column will be used as the ending column. Usually you just want to sort by a single column, in which case the same number is specified as both the starting and ending columns. Here's an example:

```
[](#cb352-1)$ cat shopping.txt
[](#cb352-2)apple   50
[](#cb352-3)toys    5
[](#cb352-4)Pizza   2
[](#cb352-5)mango   25
[](#cb352-6)Banana  10
[](#cb352-7)
[](#cb352-8)# sort based on 2nd column numbers
[](#cb352-9)$ sort -k2,2n shopping.txt
[](#cb352-10)Pizza   2
[](#cb352-11)toys    5
[](#cb352-12)Banana  10
[](#cb352-13)mango   25
[](#cb352-14)apple   50
```

> ![info](media/file0.svg) You can use the `-t` option to specify a single byte character as the field separator. Use `\0` to specify ASCII NUL as the separator.

> ![info](media/file0.svg) Use the `-s` option to retain the original order of input lines when two or more lines are deemed equal. You can still use multiple keys to specify your own tie breakers, `-s` only prevents the last resort comparison.

## uniq

This command helps you to identify and remove duplicates. Usually used with sorted inputs as the comparison is made between adjacent lines only.

### Common options

Commonly used options are shown below. Examples will be discussed in later sections.

*   `-u` display only the unique entries
*   `-d` display only the duplicate entries
*   `-D` display all the copies of duplicates
*   `-c` prefix count
*   `-i` ignore case while determining duplicates
*   `-f` skip first `N` fields
    *   field separation is based on one or more space/tab characters only
*   `-s` skip first `N` characters
*   `-w` restricts the comparison to the first `N` characters

### Default uniq

By default, `uniq` retains only one copy of duplicate lines:

```
[](#cb353-1)# same as sort -u for this case
[](#cb353-2)$ printf 'brown\nbrown\nbrown\ngreen\nbrown\nblue\nblue' | sort | uniq
[](#cb353-3)blue
[](#cb353-4)brown
[](#cb353-5)green
[](#cb353-6)
[](#cb353-7)# can't use sort -n -u here
[](#cb353-8)$ printf '2 balls\n13 pens\n2 pins\n13 pens\n' | sort -n | uniq
[](#cb353-9)2 balls
[](#cb353-10)2 pins
[](#cb353-11)13 pens
```

### Unique and duplicate entries

The `-u` option will display only the unique entries. That is, only if a line doesn't occur more than once.

```
[](#cb354-1)$ cat purchases.txt
[](#cb354-2)coffee
[](#cb354-3)tea
[](#cb354-4)washing powder
[](#cb354-5)coffee
[](#cb354-6)toothpaste
[](#cb354-7)tea
[](#cb354-8)soap
[](#cb354-9)tea
[](#cb354-10)
[](#cb354-11)$ sort purchases.txt | uniq -u
[](#cb354-12)soap
[](#cb354-13)toothpaste
[](#cb354-14)washing powder
```

The `-d` option will display only the duplicate entries. That is, only if a line is seen more than once. To display all the copies of duplicates, use the `-D` option.

```
[](#cb355-1)$ sort purchases.txt | uniq -d
[](#cb355-2)coffee
[](#cb355-3)tea
[](#cb355-4)
[](#cb355-5)$ sort purchases.txt | uniq -D
[](#cb355-6)coffee
[](#cb355-7)coffee
[](#cb355-8)tea
[](#cb355-9)tea
[](#cb355-10)tea
```

### Prefix count

If you want to know how many times a line has been repeated, use the `-c` option. This will be added as a prefix.

```
[](#cb356-1)$ sort purchases.txt | uniq -c
[](#cb356-2)      2 coffee
[](#cb356-3)      1 soap
[](#cb356-4)      3 tea
[](#cb356-5)      1 toothpaste
[](#cb356-6)      1 washing powder
[](#cb356-7)
[](#cb356-8)$ sort purchases.txt | uniq -dc
[](#cb356-9)      2 coffee
[](#cb356-10)      3 tea
[](#cb356-11)
[](#cb356-12)# sorting by number of occurrences
[](#cb356-13)$ sort purchases.txt | uniq -c | sort -nr
[](#cb356-14)      3 tea
[](#cb356-15)      2 coffee
[](#cb356-16)      1 washing powder
[](#cb356-17)      1 toothpaste
[](#cb356-18)      1 soap
```

### Partial match

`uniq` has three options to change the matching criteria to partial parts of the input line. These aren't as powerful as the `sort -k` option, but they do come in handy for some use cases.

```
[](#cb357-1)# compare only first 2 characters
[](#cb357-2)$ printf '1) apple\n1) almond\n2) banana\n3) cherry\n3) cup' | uniq -w2
[](#cb357-3)1) apple
[](#cb357-4)2) banana
[](#cb357-5)3) cherry
[](#cb357-6)
[](#cb357-7)# -f1 skips first field
[](#cb357-8)# -s2 then skips two characters (including the blank character)
[](#cb357-9)# -w2 uses next two characters for comparison ('bl' and 'ch' in this example)
[](#cb357-10)$ printf '2 @blue\n10 :black\n5 :cherry\n3 @chalk' | uniq -f1 -s2 -w2
[](#cb357-11)2 @blue
[](#cb357-12)5 :cherry
```

## comm

The `comm` command finds common and unique lines between two sorted files. By default, you'll get a tabular output with three columns:

*   first column has lines unique to the first file
*   second column has lines unique to the second file
*   third column has lines common to both the files

```
[](#cb358-1)# side by side view of already sorted sample files
[](#cb358-2)$ paste c1.txt c2.txt
[](#cb358-3)Blue    Black
[](#cb358-4)Brown   Blue
[](#cb358-5)Orange  Green
[](#cb358-6)Purple  Orange
[](#cb358-7)Red     Pink
[](#cb358-8)Teal    Red
[](#cb358-9)White   White
[](#cb358-10)
[](#cb358-11)# default three column output
[](#cb358-12)$ comm c1.txt c2.txt
[](#cb358-13)        Black
[](#cb358-14)                Blue
[](#cb358-15)Brown
[](#cb358-16)        Green
[](#cb358-17)                Orange
[](#cb358-18)        Pink
[](#cb358-19)Purple
[](#cb358-20)                Red
[](#cb358-21)Teal
[](#cb358-22)                White
```

You can use one or more of the following options to suppress columns:

*   `-1` to suppress lines unique to the first file
*   `-2` to suppress lines unique to the second file
*   `-3` to suppress lines common to both the files

```
[](#cb359-1)# only the common lines
[](#cb359-2)$ comm -12 c1.txt c2.txt
[](#cb359-3)Blue
[](#cb359-4)Orange
[](#cb359-5)Red
[](#cb359-6)White
[](#cb359-7)
[](#cb359-8)# lines unique to the second file
[](#cb359-9)$ comm -13 c1.txt c2.txt
[](#cb359-10)Black
[](#cb359-11)Green
[](#cb359-12)Pink
```

## join

By default, `join` combines two files based on the first field content (also referred as **key**). Only the lines with common keys will be part of the output.

The key field will be displayed first in the output (this distinction will come into play if the first field isn't the key). Rest of the line will have the remaining fields from the first and second files, in that order. One or more blanks (space or tab) will be considered as the input field separator and a single space will be used as the output field separator. If present, blank characters at the start of the input lines will be ignored.

```
[](#cb360-1)# sample sorted input files
[](#cb360-2)$ cat shopping_jan.txt
[](#cb360-3)apple   10
[](#cb360-4)banana  20
[](#cb360-5)soap    3
[](#cb360-6)tshirt  3
[](#cb360-7)$ cat shopping_feb.txt
[](#cb360-8)banana  15
[](#cb360-9)fig     100
[](#cb360-10)pen     2
[](#cb360-11)soap    1
[](#cb360-12)
[](#cb360-13)# combine common lines based on the first field
[](#cb360-14)$ join shopping_jan.txt shopping_feb.txt
[](#cb360-15)banana 20 15
[](#cb360-16)soap 3 1
```

> ![info](media/file0.svg) Note that the collating order used for `join` should be same as the one used to `sort` the input files. Use `join -i` to ignore case, similar to `sort -f` usage.

If a field value is present multiple times in the same input file, all possible combinations will be present in the output. As shown below, `join` will also ensure to add a final newline character even if not present in the input.

```
[](#cb361-1)$ join <(printf 'a f1_x\na f1_y') <(printf 'a f2_x\na f2_y')
[](#cb361-2)a f1_x f2_x
[](#cb361-3)a f1_x f2_y
[](#cb361-4)a f1_y f2_x
[](#cb361-5)a f1_y f2_y
```

> ![info](media/file0.svg) There are many more features such as specifying field delimiter, selecting specific fields from each input file in a particular order, filling fields for non-matching lines and so on. See [join chapter](https://learnbyexample.github.io/cli_text_processing_coreutils/join.html) from my [Command line text processing with GNU Coreutils](https://github.com/learnbyexample/cli_text_processing_coreutils) ebook for explanations and examples.

## Exercises

> ![info](media/file0.svg) Use [example_files/text_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files/text_files) directory for input files used in the following exercises.

**1)** Default `sort` doesn't work for numbers. Correct the command used below:

```
[](#cb362-1)# wrong output
[](#cb362-2)$ printf '100\n10\n20\n3000\n2.45\n' | sort
[](#cb362-3)10
[](#cb362-4)100
[](#cb362-5)20
[](#cb362-6)2.45
[](#cb362-7)3000
[](#cb362-8)
[](#cb362-9)# expected output
[](#cb362-10)$ printf '100\n10\n20\n3000\n2.45\n' | sort # ???
[](#cb362-11)2.45
[](#cb362-12)10
[](#cb362-13)20
[](#cb362-14)100
[](#cb362-15)3000
```

**2)** Which `sort` option will help you ignore case?

```
[](#cb363-1)$ printf 'Super\nover\nRUNE\ntea\n' | LC_ALL=C sort # ???
[](#cb363-2)over
[](#cb363-3)RUNE
[](#cb363-4)Super
[](#cb363-5)tea
```

**3)** Go through the `sort` manual and use appropriate options to get the output shown below.

```
[](#cb364-1)# wrong output
[](#cb364-2)$ printf '+120\n-1.53\n3.14e+4\n42.1e-2' | sort -n
[](#cb364-3)-1.53
[](#cb364-4)+120
[](#cb364-5)3.14e+4
[](#cb364-6)42.1e-2
[](#cb364-7)
[](#cb364-8)# expected output
[](#cb364-9)$ printf '+120\n-1.53\n3.14e+4\n42.1e-2' | sort # ???
[](#cb364-10)-1.53
[](#cb364-11)42.1e-2
[](#cb364-12)+120
[](#cb364-13)3.14e+4
```

**4)** Sort the `scores.csv` file numerically in ascending order using the contents of the second field. Header line should be preserved as the first line as shown below. *Hint*: see [Shell Features](#ch005.xhtml_shell-features) chapter.

```
[](#cb365-1)# ???
[](#cb365-2)Name,Maths,Physics,Chemistry
[](#cb365-3)Lin,78,83,80
[](#cb365-4)Cy,97,98,95
[](#cb365-5)Ith,100,100,100
```

**5)** Sort the contents of `duplicates.txt` by the fourth column numbers in descending order. Retain only the first copy of lines with the same number.

```
[](#cb366-1)# ???
[](#cb366-2)dark red,sky,rose,555
[](#cb366-3)blue,ruby,water,333
[](#cb366-4)dark red,ruby,rose,111
[](#cb366-5)brown,toy,bread,42
```

**6)** Will `uniq` throw an error if the input is not sorted? What do you think will be the output for the following input?

```
[](#cb367-1)$ printf 'red\nred\nred\ngreen\nred\nblue\nblue' | uniq
[](#cb367-2)# ???
```

**7)** Retain only unique entries based on the first two characters of the input lines. Sort the input if necessary.

```
[](#cb368-1)$ printf '3) cherry\n1) apple\n2) banana\n1) almond\n'
[](#cb368-2)3) cherry
[](#cb368-3)1) apple
[](#cb368-4)2) banana
[](#cb368-5)1) almond
[](#cb368-6)
[](#cb368-7)$ printf '3) cherry\n1) apple\n2) banana\n1) almond\n' | # ???
[](#cb368-8)2) banana
[](#cb368-9)3) cherry
```

**8)** Count the number of times input lines are repeated and display the results in the format shown below.

```
[](#cb369-1)$ printf 'brown\nbrown\nbrown\ngreen\nbrown\nblue\nblue' | # ???
[](#cb369-2)      1 green
[](#cb369-3)      2 blue
[](#cb369-4)      4 brown
```

**9)** Display lines present in `c1.txt` but not in `c2.txt` using the `comm` command. Assume that the input files are already sorted.

```
[](#cb370-1)# ???
[](#cb370-2)Brown
[](#cb370-3)Purple
[](#cb370-4)Teal
```

**10)** Use appropriate options to get the expected output shown below.

```
[](#cb371-1)# wrong usage, no output
[](#cb371-2)$ join <(printf 'apple 2\nfig 5') <(printf 'Fig 10\nmango 4')
[](#cb371-3)
[](#cb371-4)# expected output
[](#cb371-5)# ???
[](#cb371-6)fig 5 10
```

**11)** What are the differences between `sort -u` and `uniq -u` options, if any?

# Comparing Files

In this chapter, you'll learn how to find and report differences between the contents of two files.

> ![info](media/file0.svg) The [example_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files) directory has the sample input files used in this chapter.

## cmp

The `cmp` command is useful to compare text and binary files. If the two files are same, no output is displayed and exit status is `0`. If there is a difference, it prints the first difference with details like line number and byte location and the exit status will be `1`.

```
[](#cb372-1)$ mkdir practice_cmp
[](#cb372-2)$ cd practice_cmp
[](#cb372-3)$ echo 'hello' > x1.txt
[](#cb372-4)$ cp x{1,2}.txt
[](#cb372-5)$ echo 'hello.' > x3.txt
[](#cb372-6)
[](#cb372-7)# files with same content
[](#cb372-8)$ cmp x1.txt x2.txt
[](#cb372-9)$ echo $?
[](#cb372-10)0
[](#cb372-11)
[](#cb372-12)# files with differences
[](#cb372-13)$ cmp x1.txt x3.txt
[](#cb372-14)x1.txt x3.txt differ: byte 6, line 1
[](#cb372-15)$ echo $?
[](#cb372-16)1
```

> ![info](media/file0.svg) Use the `-s` option to suppress the output when you just need the exit status. The `-i` option will allow you to skip initial bytes from the input.

## diff

Useful to find differences between text files. All the differences are printed, which might not be desirable for long files.

### Common options

Commonly used options are shown below. Examples will be discussed in later sections.

*   `-i` ignore case while comparing
*   `-w` ignore whitespaces
*   `-b` ignore changes in the amount of whitespace
*   `-B` ignore only blank lines
*   `-E` ignore changes due to tab expansion
*   `-z` ignore trailing whitespaces at the end of line
*   `-y` two column output
*   `-r` recursively compare files between the two directories specified
*   `-s` convey message when two files are same
*   `-q` report if files differ, not the details of differences

### Default diff

By default, the `diff` output shows lines from the first file input prefixed with `<` and lines from the second file input prefixed with `>`. A line containing `---` is used as the group separator. Each difference is prefixed by a command that indicates the differences (these commands are understood by tools like `patch`).

```
[](#cb373-1)# change to the 'example_files/text_files' directory
[](#cb373-2)# side-by-side view of sample input files
[](#cb373-3)$ paste f1.txt f2.txt
[](#cb373-4)1       1
[](#cb373-5)2       hello
[](#cb373-6)3       3
[](#cb373-7)world   4
[](#cb373-8)
[](#cb373-9)$ diff f1.txt f2.txt
[](#cb373-10)2c2
[](#cb373-11)< 2
[](#cb373-12)---
[](#cb373-13)> hello
[](#cb373-14)4c4
[](#cb373-15)< world
[](#cb373-16)---
[](#cb373-17)> 4
[](#cb373-18)
[](#cb373-19)$ diff <(seq 4) <(seq 5)
[](#cb373-20)4a5
[](#cb373-21)> 5
```

### Ignoring whitespaces

There are several options to ignore specific whitespace characters during comparison. Here are some examples:

```
[](#cb374-1)# ignore changes in the amount of whitespace
[](#cb374-2)$ diff -b <(echo 'good day') <(echo 'good    day')
[](#cb374-3)$ echo $?
[](#cb374-4)0
[](#cb374-5)
[](#cb374-6)# ignore all whitespaces
[](#cb374-7)$ diff -w <(echo 'hi    there ') <(echo ' hi there')
[](#cb374-8)$ echo $?
[](#cb374-9)0
[](#cb374-10)$ diff -w <(echo 'hi    there ') <(echo 'hithere')
[](#cb374-11)$ echo $?
[](#cb374-12)0
```

### Side-by-side output

The `-y` option is handy to view the differences side-by-side. By default, all the input lines will be present in the output and the line width is 130 print columns. You can use the `-W` option to change the width when dealing with short input lines. The `--suppress-common-lines` helps to focus only on the differences.

```
[](#cb375-1)$ diff -y f1.txt f2.txt
[](#cb375-2)1                                                               1
[](#cb375-3)2                                                             | hello
[](#cb375-4)3                                                               3
[](#cb375-5)world                                                         | 4
[](#cb375-6)
[](#cb375-7)$ diff -W 60 --suppress-common-lines -y f1.txt f2.txt
[](#cb375-8)2                            |  hello
[](#cb375-9)world                        |  4
```

### Further Reading

*   `gvimdiff` edit two, three or four versions of a file with GVim and show differences
*   [GUI diff and merge tools](http://askubuntu.com/questions/2946/what-are-some-good-gui-diff-and-merge-applications-available-for-ubuntu)

## Exercises

> ![info](media/file0.svg) Use [example_files/text_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files/text_files) directory for input files used in the following exercises.

**1)** Which `cmp` option would you use if you just need the exit status reflecting whether the given inputs are same or not?

**2)** Which `cmp` option would you use to skip initial bytes for comparison purposes? The below example requires you to skip the first two bytes.

```
[](#cb376-1)$ echo '1) apple' > x1.txt
[](#cb376-2)$ echo '2\. apple' > x2.txt
[](#cb376-3)$ cmp x1.txt x2.txt
[](#cb376-4)x1.txt x2.txt differ: byte 1, line 1
[](#cb376-5)
[](#cb376-6)$ cmp # ???
[](#cb376-7)$ echo $?
[](#cb376-8)0
[](#cb376-9)
[](#cb376-10)$ rm x[12].txt
```

**3)** What does the `diff -d` option do?

**4)** Which option will help you get colored output with `diff`?

**5)** Use appropriate options to get the desired output shown below.

```
[](#cb377-1)# instead of this output
[](#cb377-2)$ diff -W 40 --suppress-common-lines -y f1.txt f2.txt
[](#cb377-3)2                  |    hello
[](#cb377-4)world              |    4
[](#cb377-5)
[](#cb377-6)# get this output
[](#cb377-7)$ diff # ???
[](#cb377-8)1                  (
[](#cb377-9)2                  |    hello
[](#cb377-10)3                  (
[](#cb377-11)world              |    4
```

**6)** Use appropriate options to get the desired output shown below.

```
[](#cb378-1)$ echo 'hello' > d1.txt
[](#cb378-2)$ echo 'Hello' > d2.txt
[](#cb378-3)
[](#cb378-4)# instead of this output
[](#cb378-5)$ diff d1.txt d2.txt
[](#cb378-6)1c1
[](#cb378-7)< hello
[](#cb378-8)---
[](#cb378-9)> Hello
[](#cb378-10)
[](#cb378-11)# get this output
[](#cb378-12)$ diff # ???
[](#cb378-13)Files d1.txt and d2.txt are identical
[](#cb378-14)
[](#cb378-15)$ rm d[12].txt
```

# Assorted Text Processing Tools

There are way too many specialized text processing tools. This chapter will discuss some of the commands that haven't been covered in the previous chapters.

> ![info](media/file0.svg) The [example_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files) directory has the sample input files used in this chapter.

## seq

The `seq` command is a handy tool to generate a sequence of numbers in ascending or descending order. Both integer and floating-point numbers are supported. You can also customize the formatting for numbers and the separator between them.

You need three numbers to generate an arithmetic progression — **start**, **step** and **stop**. When you pass only a single number as the stop value, the default start and step values are assumed to be `1`. Passing two numbers are considered as start and stop values (in that order).

```
[](#cb379-1)# start=1, step=1 and stop=3
[](#cb379-2)$ seq 3
[](#cb379-3)1
[](#cb379-4)2
[](#cb379-5)3
[](#cb379-6)
[](#cb379-7)# start=25434, step=1 and stop=25437
[](#cb379-8)$ seq 25434 25437
[](#cb379-9)25434
[](#cb379-10)25435
[](#cb379-11)25436
[](#cb379-12)25437
[](#cb379-13)
[](#cb379-14)# start=-5, step=1 and stop=-3
[](#cb379-15)$ seq -5 -3
[](#cb379-16)-5
[](#cb379-17)-4
[](#cb379-18)-3
[](#cb379-19)
[](#cb379-20)# start=0.25, step=0.33 and stop=1.12
[](#cb379-21)$ seq 0.25 0.33 1.12
[](#cb379-22)0.25
[](#cb379-23)0.58
[](#cb379-24)0.91
```

By using a negative step value, you can generate sequences in descending order.

```
[](#cb380-1)$ seq 3 -1 1
[](#cb380-2)3
[](#cb380-3)2
[](#cb380-4)1
```

You can use the `-s` option to change the separator *between* the numbers of a sequence. A single newline character is always the character added after the final number.

```
[](#cb381-1)$ seq -s' - ' 4
[](#cb381-2)1 - 2 - 3 - 4
[](#cb381-3)
[](#cb381-4)$ seq -s: 1.2e2 0.752 1.22e2
[](#cb381-5)120.000:120.752:121.504
```

The `-w` option will equalize the width of the output numbers using leading zeros. The largest width between the start and stop values will be used.

```
[](#cb382-1)$ seq -w 8 10
[](#cb382-2)08
[](#cb382-3)09
[](#cb382-4)10
[](#cb382-5)
[](#cb382-6)$ seq -w 0003
[](#cb382-7)0001
[](#cb382-8)0002
[](#cb382-9)0003
```

You can use the `-f` option for `printf` style floating-point number formatting.

```
[](#cb383-1)$ seq -f'%g' -s: 1 0.75 3
[](#cb383-2)1:1.75:2.5
[](#cb383-3)
[](#cb383-4)$ seq -f'%.4f' -s: 1 0.75 3
[](#cb383-5)1.0000:1.7500:2.5000
[](#cb383-6)
[](#cb383-7)$ seq -f'%.3e' 1.2e2 0.752 1.22e2
[](#cb383-8)1.200e+02
[](#cb383-9)1.208e+02
[](#cb383-10)1.215e+02
```

## shuf

By default, `shuf` will randomize the order of input lines. You can use the `-n` option to limit the number of output lines.

```
[](#cb384-1)$ printf 'apple\nbanana\ncherry\nfig\nmango' | shuf
[](#cb384-2)banana
[](#cb384-3)cherry
[](#cb384-4)mango
[](#cb384-5)apple
[](#cb384-6)fig
[](#cb384-7)
[](#cb384-8)$ printf 'apple\nbanana\ncherry\nfig\nmango' | shuf -n2
[](#cb384-9)mango
[](#cb384-10)cherry
```

You can use the `-e` option to specify multiple input lines as arguments to the command. The `-r` option helps if you want to allow input lines to be repeated. This option is usually paired with `-n` to limit the number of lines in the output.

```
[](#cb385-1)$ shuf -n4 -r -e brown green blue
[](#cb385-2)green
[](#cb385-3)brown
[](#cb385-4)blue
[](#cb385-5)green
```

The `-i` option will help you generate random positive integers.

```
[](#cb386-1)$ shuf -n3 -i 100-200
[](#cb386-2)170
[](#cb386-3)112
[](#cb386-4)148
```

## cut

`cut` is a handy tool for many field processing use cases. The features are limited compared to `awk` and `perl` commands, but the reduced scope also leads to faster processing.

By default, `cut` splits the input content into fields based on the tab character, which you can change using the `-d` option. The `-f` option allows you to select a desired field from each input line. To extract multiple fields, specify the selections separated by the comma character. By default, lines not containing the input delimiter will still be part of the output. You can use the `-s` option to suppress such lines.

```
[](#cb387-1)# second field
[](#cb387-2)$ printf 'apple\tbanana\tcherry\n' | cut -f2
[](#cb387-3)banana
[](#cb387-4)
[](#cb387-5)# first and third field
[](#cb387-6)$ printf 'apple\tbanana\tcherry\n' | cut -f1,3
[](#cb387-7)apple   cherry
[](#cb387-8)
[](#cb387-9)# setting -d automatically changes output delimiter as well
[](#cb387-10)$ echo 'one;two;three;four;five' | cut -d';' -f2,5
[](#cb387-11)two;five
```

You can use the `-` character to specify field ranges. The starting or ending field number can be skipped, but not both.

```
[](#cb388-1)# 2nd, 3rd and 4th fields
[](#cb388-2)$ printf 'apple\tbanana\tcherry\tdates\n' | cut -f2-4
[](#cb388-3)banana  cherry  dates
[](#cb388-4)
[](#cb388-5)# all fields from the start till the 3rd field
[](#cb388-6)$ printf 'apple\tbanana\tcherry\tdates\n' | cut -f-3
[](#cb388-7)apple   banana  cherry
[](#cb388-8)
[](#cb388-9)# 1st field and all fields from the 3rd field till the end
[](#cb388-10)$ printf 'apple\tbanana\tcherry\tdates\n' | cut -f1,3-
[](#cb388-11)apple   cherry  dates
```

Use the `--output-delimiter` option to customize the output separator to any string of your choice.

```
[](#cb389-1)# same as: tr '\t' ','
[](#cb389-2)$ printf 'apple\tbanana\tcherry\n' | cut --output-delimiter=, -f1-
[](#cb389-3)apple,banana,cherry
[](#cb389-4)
[](#cb389-5)# multicharacter example
[](#cb389-6)$ echo 'one;two;three;four' | cut -d';' --output-delimiter=' : ' -f1,3-
[](#cb389-7)one : three : four
```

The `--complement` option allows you to invert the field selections.

```
[](#cb390-1)# except second field
[](#cb390-2)$ printf 'apple ball cat\n1 2 3 4 5' | cut --complement -d' ' -f2
[](#cb390-3)apple cat
[](#cb390-4)1 3 4 5
[](#cb390-5)
[](#cb390-6)# except first and third fields
[](#cb390-7)$ printf 'apple ball cat\n1 2 3 4 5' | cut --complement -d' ' -f1,3
[](#cb390-8)ball
[](#cb390-9)2 4 5
```

You can use the `-b` or `-c` options to select specified bytes from each input line. The syntax is same as the `-f` option. The `-c` option is intended for multibyte character selection, but for now it works exactly as the `-b` option.

```
[](#cb391-1)$ printf 'apple\tbanana\tcherry\n' | cut -c2,8,11
[](#cb391-2)pan
[](#cb391-3)
[](#cb391-4)$ printf 'apple\tbanana\tcherry\n' | cut -c2,8,11 --output-delimiter=-
[](#cb391-5)p-a-n
[](#cb391-6)
[](#cb391-7)$ printf 'apple\tbanana\tcherry\n' | cut --complement -c13-
[](#cb391-8)apple   banana
[](#cb391-9)
[](#cb391-10)$ printf 'cat-bat\ndog:fog' | cut -c5-
[](#cb391-11)bat
[](#cb391-12)fog
```

## column

The `column` command is a nifty tool to align input data column wise. By default, whitespace is used as the input delimiter. Space character is used to align the output columns, so whitespace characters like tab will get converted to spaces.

```
[](#cb392-1)$ printf 'one two three\nfour five six\nseven eight nine\n'
[](#cb392-2)one two three
[](#cb392-3)four five six
[](#cb392-4)seven eight nine
[](#cb392-5)
[](#cb392-6)$ printf 'one two three\nfour five six\nseven eight nine\n' | column -t
[](#cb392-7)one    two    three
[](#cb392-8)four   five   six
[](#cb392-9)seven  eight  nine
```

You can use the `-s` option to customize the input delimiter. Note that the output delimiter will still be made up of spaces only.

```
[](#cb393-1)$ cat scores.csv
[](#cb393-2)Name,Maths,Physics,Chemistry
[](#cb393-3)Ith,100,100,100
[](#cb393-4)Cy,97,98,95
[](#cb393-5)Lin,78,83,80
[](#cb393-6)
[](#cb393-7)$ column -s, -t scores.csv
[](#cb393-8)Name  Maths  Physics  Chemistry
[](#cb393-9)Ith   100    100      100
[](#cb393-10)Cy    97     98       95
[](#cb393-11)Lin   78     83       80
[](#cb393-12)
[](#cb393-13)$ printf '1:-:2:-:3\napple:-:banana:-:cherry\n' | column -s:-: -t
[](#cb393-14)1      2       3
[](#cb393-15)apple  banana  cherry
```

> ![warning](media/file7.svg) Input should have a newline at the end, otherwise you'll get an error:
> 
> ```
> [](#cb394-1)$ printf '1 2 3\na   b   c' | column -t
> [](#cb394-2)column: line too long
> [](#cb394-3)1  2  3
> ```

## tr

`tr` helps you to map one set of characters to another set of characters. Features like range, repeats, character sets, squeeze, complement, etc makes it a must know text processing tool.

`tr` works only on `stdin` data, so you'll need to use shell input redirection for file input. Here are some basic examples:

```
[](#cb395-1)# 'l' maps to '1', 'e' to '3', 't' to '7' and 's' to '5'
[](#cb395-2)$ echo 'leet speak' | tr 'lets' '1375'
[](#cb395-3)1337 5p3ak
[](#cb395-4)
[](#cb395-5)# example with shell metacharacters
[](#cb395-6)$ echo 'apple;banana;cherry' | tr ';' ':'
[](#cb395-7)apple:banana:cherry
[](#cb395-8)
[](#cb395-9)# swap case
[](#cb395-10)$ echo 'Hello World' | tr 'a-zA-Z' 'A-Za-z'
[](#cb395-11)hELLO wORLD
[](#cb395-12)
[](#cb395-13)$ tr 'a-z' 'A-Z' <greeting.txt
[](#cb395-14)HI THERE
[](#cb395-15)HAVE A NICE DAY
```

You can use the `-d` option to specify a set of characters to be deleted. The `-c` option will invert the first set of characters. Here are some examples:

```
[](#cb396-1)$ echo '2021-08-12' | tr -d '-'
[](#cb396-2)20210812
[](#cb396-3)
[](#cb396-4)$ s='"Hi", there! How *are* you? All fine here.'
[](#cb396-5)$ echo "$s" | tr -d '[:punct:]'
[](#cb396-6)Hi there How are you All fine here
[](#cb396-7)
[](#cb396-8)# retain alphabets, whitespaces, period, exclamation and question mark
[](#cb396-9)$ echo "$s" | tr -cd 'a-zA-Z.!?[:space:]'
[](#cb396-10)Hi there! How are you? All fine here.
```

The `-s` option will squeeze consecutive repeated characters to a single copy of that character.

```
[](#cb397-1)# squeeze lowercase alphabets
[](#cb397-2)$ echo 'hhoowwww aaaaaareeeeee yyouuuu!!' | tr -s 'a-z'
[](#cb397-3)how are you!!
[](#cb397-4)
[](#cb397-5)# translate and squeeze
[](#cb397-6)$ echo 'hhoowwww aaaaaareeeeee yyouuuu!!' | tr -s 'a-z' 'A-Z'
[](#cb397-7)HOW ARE YOU!!
[](#cb397-8)
[](#cb397-9)# delete and squeeze
[](#cb397-10)$ echo 'hhoowwww aaaaaareeeeee yyouuuu!!' | tr -sd '!' 'a-z'
[](#cb397-11)how are you
[](#cb397-12)
[](#cb397-13)# squeeze other than lowercase alphabets
[](#cb397-14)$ echo 'apple    noon     banana!!!!!' | tr -cs 'a-z'
[](#cb397-15)apple noon banana!
```

## paste

`paste` is typically used to merge two or more files column wise. It also has a handy feature for serializing data. By default, `paste` adds a tab character between the corresponding lines of input files.

```
[](#cb398-1)$ cat colors_1.txt
[](#cb398-2)Blue
[](#cb398-3)Brown
[](#cb398-4)Orange
[](#cb398-5)Purple
[](#cb398-6)$ cat colors_2.txt
[](#cb398-7)Black
[](#cb398-8)Blue
[](#cb398-9)Green
[](#cb398-10)Orange
[](#cb398-11)
[](#cb398-12)$ paste colors_1.txt colors_2.txt
[](#cb398-13)Blue    Black
[](#cb398-14)Brown   Blue
[](#cb398-15)Orange  Green
[](#cb398-16)Purple  Orange
```

You can use the `-d` option to change the delimiter between the columns. The separator is added even if the data has been exhausted for some of the input files.

```
[](#cb399-1)$ paste -d'|' <(seq 3) <(seq 4 5) <(seq 6 8)
[](#cb399-2)1|4|6
[](#cb399-3)2|5|7
[](#cb399-4)3||8
[](#cb399-5)
[](#cb399-6)# note that the space between -d and empty string is necessary here
[](#cb399-7)$ paste -d '' <(seq 3) <(seq 6 8)
[](#cb399-8)16
[](#cb399-9)27
[](#cb399-10)38
[](#cb399-11)
[](#cb399-12)$ paste -d'\n' <(seq 11 12) <(seq 101 102)
[](#cb399-13)11
[](#cb399-14)101
[](#cb399-15)12
[](#cb399-16)102
```

You can use empty files to get multicharacter separation between the columns.

```
[](#cb400-1)$ paste -d' : ' <(seq 3) /dev/null /dev/null <(seq 4 6)
[](#cb400-2)1 : 4
[](#cb400-3)2 : 5
[](#cb400-4)3 : 6
```

If you use `-` multiple times, `paste` will consume a line from `stdin` data every time `-` is encountered. This is different from using the same filename multiple times, in which case they are treated as separate inputs.

```
[](#cb401-1)# five columns
[](#cb401-2)$ seq 10 | paste -d: - - - - -
[](#cb401-3)1:2:3:4:5
[](#cb401-4)6:7:8:9:10
[](#cb401-5)
[](#cb401-6)# use redirection for file input
[](#cb401-7)$ <colors_1.txt paste -d: - - -
[](#cb401-8)Blue:Brown:Orange
[](#cb401-9)Purple::
```

The `-s` option allows you to combine all the input lines from a file into a single line using the given delimiter. Multiple input files are treated separately. `paste` will ensure to add a final newline character even if it isn't present in the input.

```
[](#cb402-1)# <colors_1.txt tr '\n' ',' will give you a trailing comma
[](#cb402-2)$ paste -sd, colors_1.txt
[](#cb402-3)Blue,Brown,Orange,Purple
[](#cb402-4)
[](#cb402-5)# multiple file example
[](#cb402-6)$ paste -sd: colors_1.txt colors_2.txt
[](#cb402-7)Blue:Brown:Orange:Purple
[](#cb402-8)Black:Blue:Green:Orange
```

## pr

> Paginate or columnate FILE(s) for printing.

As stated in the above quote from the manual, the `pr` command is mainly used for those two tasks. This section will discuss only the columnate features and some miscellaneous tasks. Here's a pagination example if you are interested in exploring further. The `pr` command will add blank lines, a header and so on to make it suitable for printing.

```
[](#cb403-1)$ pr greeting.txt | head -n8
[](#cb403-2)
[](#cb403-3)
[](#cb403-4)2022-06-11 10:48                   greeting.txt                   Page 1
[](#cb403-5)
[](#cb403-6)
[](#cb403-7)Hi there
[](#cb403-8)Have a nice day
```

The `--columns` and `-a` options can be used to merge the input lines in two different ways:

*   split the input file and then merge them as columns
*   merge consecutive lines, similar to the `paste` command

Here's an example to get started. Note that `-N` is same as using `--columns=N` where `N` is the number of columns you want in the output. The default page width is `72`, which means each column can only have a maximum of `72/N` characters (including the separator). Tab and space characters will be used to fill the columns as needed. You can use the `-J` option to prevent `pr` from truncating longer columns. The `-t` option is used here to turn off the pagination features.

```
[](#cb404-1)# split input into three parts
[](#cb404-2)# each column width is 72/3 = 24 characters max
[](#cb404-3)$ seq 9 | pr -3t
[](#cb404-4)1                       4                       7
[](#cb404-5)2                       5                       8
[](#cb404-6)3                       6                       9
```

You can customize the separator using the `-s` option. The default is a tab character which you can change to any other string value. The `-s` option also turns off line truncation, so `-J` option isn't needed.

```
[](#cb405-1)# tab separator
[](#cb405-2)$ seq 9 | pr -3ts
[](#cb405-3)1       4       7
[](#cb405-4)2       5       8
[](#cb405-5)3       6       9
[](#cb405-6)
[](#cb405-7)# custom separator
[](#cb405-8)$ seq 9 | pr -3ts' : '
[](#cb405-9)1 : 4 : 7
[](#cb405-10)2 : 5 : 8
[](#cb405-11)3 : 6 : 9
```

However, the default page width of `72` can still cause issues, which you can prevent by using the `-w` option. The `-w` option overrides the effect of `-s` option on line truncation, so use `-J` option as well unless you really need truncation.

```
[](#cb406-1)$ seq 6 | pr -J -w10 -3ats'::::'
[](#cb406-2)pr: page width too narrow
[](#cb406-3)
[](#cb406-4)$ seq 6 | pr -J -w11 -3ats'::::'
[](#cb406-5)1::::2::::3
[](#cb406-6)4::::5::::6
```

Use the `-a` option to merge consecutive lines, similar to the `paste` command. One advantage is that the `-s` option supports a string value, whereas with `paste` you'd need to use workarounds to get multicharacter separation.

```
[](#cb407-1)# same as: paste -d: - - - -
[](#cb407-2)$ seq 8 | pr -4ats:
[](#cb407-3)1:2:3:4
[](#cb407-4)5:6:7:8
[](#cb407-5)
[](#cb407-6)# unlike paste, pr doesn't add separators if the last row has less columns to fill
[](#cb407-7)$ seq 10 | pr -4ats,
[](#cb407-8)1,2,3,4
[](#cb407-9)5,6,7,8
[](#cb407-10)9,10
```

Two or more input files can be merged column wise using the `-m` option. As seen before, `-t` is needed to ignore pagination features and `-s` can be used to customize the separator.

```
[](#cb408-1)# same as: paste -d' : ' <(seq 3) /dev/null /dev/null <(seq 4 6)
[](#cb408-2)$ pr -mts' : ' <(seq 3) <(seq 4 6)
[](#cb408-3)1 : 4
[](#cb408-4)2 : 5
[](#cb408-5)3 : 6
```

## rev

The `rev` command reverses each input line character wise. Newline character *won't* be added to the end if it wasn't present in the input. Here are some examples:

```
[](#cb409-1)$ echo 'This is a sample text' | rev
[](#cb409-2)txet elpmas a si sihT
[](#cb409-3)
[](#cb409-4)$ printf 'apple\nbanana\ncherry\n' | rev
[](#cb409-5)elppa
[](#cb409-6)ananab
[](#cb409-7)yrrehc
[](#cb409-8)
[](#cb409-9)$ printf 'malayalam\nnoon\n' | rev
[](#cb409-10)malayalam
[](#cb409-11)noon
```

## split

The `split` command is useful to divide the input into smaller parts based on number of lines, bytes, file size, etc. You can also execute another command on the divided parts before saving the results. An example use case is sending a large file as multiple parts as a workaround for online transfer size limits.

By default, the `split` command divides the input `1000` lines at a time. Newline character is the default line separator. You can pass a single file or `stdin` data as the input. Use `cat` if you need to concatenate multiple input sources. By default, the output files will be named `xaa`, `xab`, `xac` and so on (where `x` is the prefix). If the filenames are exhausted, two more letters will be appended and the pattern will continue as needed. If the number of input lines is not evenly divisible, the last file will contain less than `1000` lines.

```
[](#cb410-1)# divide input 1000 lines at a time
[](#cb410-2)$ seq 10000 | split
[](#cb410-3)
[](#cb410-4)# output filenames
[](#cb410-5)$ ls x*
[](#cb410-6)xaa  xab  xac  xad  xae  xaf  xag  xah  xai  xaj
[](#cb410-7)
[](#cb410-8)# preview of some of the output files
[](#cb410-9)$ head -n1 xaa xab xae xaj
[](#cb410-10)==> xaa <==
[](#cb410-11)1
[](#cb410-12)
[](#cb410-13)==> xab <==
[](#cb410-14)1001
[](#cb410-15)
[](#cb410-16)==> xae <==
[](#cb410-17)4001
[](#cb410-18)
[](#cb410-19)==> xaj <==
[](#cb410-20)9001
```

> ![info](media/file0.svg) For more examples, customization options and other details, see [split chapter](https://learnbyexample.github.io/cli_text_processing_coreutils/split.html) from my [Command line text processing with GNU Coreutils](https://github.com/learnbyexample/cli_text_processing_coreutils) ebook.

## csplit

The `csplit` command is useful to divide the input into smaller parts based on line numbers and regular expression patterns.

You can split the input into two based on a particular line number. To do so, specify the line number after the input source (filename or `stdin` data). The first output file will have the input lines *before* the given line number and the second output file will have the rest of the contents. By default, the output files will be named `xx00`, `xx01`, `xx02` and so on (where `xx` is the prefix). The numerical suffix will automatically use more digits if needed.

```
[](#cb411-1)# split input into two based on line number 2
[](#cb411-2)# -q option suppresses output showing number of bytes written for each file
[](#cb411-3)$ seq 4 | csplit -q - 2
[](#cb411-4)
[](#cb411-5)# first output file will have the first line
[](#cb411-6)# second output file will have the rest
[](#cb411-7)$ head xx*
[](#cb411-8)==> xx00 <==
[](#cb411-9)1
[](#cb411-10)
[](#cb411-11)==> xx01 <==
[](#cb411-12)2
[](#cb411-13)3
[](#cb411-14)4
```

You can also split the input based on a line matching the given regular expression. The output produced will vary based on `//` or `%%` delimiters being used to surround the regexp. When `/regexp/` is used, output is similar to the line number based splitting. The first output file will have the input lines *before* the first occurrence of a line matching the given regexp and the second output file will have the rest of the contents.

Consider this sample input file:

```
[](#cb412-1)$ cat purchases.txt
[](#cb412-2)coffee
[](#cb412-3)tea
[](#cb412-4)washing powder
[](#cb412-5)coffee
[](#cb412-6)toothpaste
[](#cb412-7)tea
[](#cb412-8)soap
[](#cb412-9)tea
```

Here's an example of splitting the input file using the `/regexp/` syntax:

```
[](#cb413-1)# match a line containing 't' followed by zero or more characters and then 'p'
[](#cb413-2)# 'toothpaste' is the only match for this input file
[](#cb413-3)$ csplit -q purchases.txt '/t.*p/'
[](#cb413-4)
[](#cb413-5)$ head xx*
[](#cb413-6)==> xx00 <==
[](#cb413-7)coffee
[](#cb413-8)tea
[](#cb413-9)washing powder
[](#cb413-10)coffee
[](#cb413-11)
[](#cb413-12)==> xx01 <==
[](#cb413-13)toothpaste
[](#cb413-14)tea
[](#cb413-15)soap
[](#cb413-16)tea
```

When `%regexp%` is used, the lines occurring before the matching line won't be part of the output. Only the line matching the given regexp and the rest of the contents will be part of the single output file.

```
[](#cb414-1)$ csplit -q purchases.txt '%t.*p%'
[](#cb414-2)
[](#cb414-3)$ cat xx00
[](#cb414-4)toothpaste
[](#cb414-5)tea
[](#cb414-6)soap
[](#cb414-7)tea
```

> ![info](media/file0.svg) For more examples, customization options and other details, see [csplit chapter](https://learnbyexample.github.io/cli_text_processing_coreutils/csplit.html) from my [Command line text processing with GNU Coreutils](https://github.com/learnbyexample/cli_text_processing_coreutils) ebook.

## xargs

By default, `xargs` executes the `echo` command for the arguments extracted from `stdin` data (or file input via the `-a` option). The `-n` option helps to customize how many arguments should be passed at a time. Together, these features can be used to reshape whitespace separated data as shown in the examples below:

```
[](#cb415-1)$ printf '  apple   banana cherry\n\t\tdragon unicorn   \n'
[](#cb415-2)  apple   banana cherry
[](#cb415-3)                dragon unicorn 
[](#cb415-4)$ printf '  apple   banana cherry\n\t\tdragon unicorn   \n' | xargs -n2
[](#cb415-5)apple banana
[](#cb415-6)cherry dragon
[](#cb415-7)unicorn
[](#cb415-8)
[](#cb415-9)$ cat ip.txt
[](#cb415-10)deep blue
[](#cb415-11)light orange
[](#cb415-12)blue delight
[](#cb415-13)$ xargs -a ip.txt -n3
[](#cb415-14)deep blue light
[](#cb415-15)orange blue delight
```

You can use the `-L` option to specify how many input lines should be combined at a time:

```
[](#cb416-1)# same as: pr -3ats' ' or paste -d' ' - - -
[](#cb416-2)$ seq 9 | xargs -L3
[](#cb416-3)1 2 3
[](#cb416-4)4 5 6
[](#cb416-5)7 8 9
[](#cb416-6)
[](#cb416-7)$ xargs -a ip.txt -L2
[](#cb416-8)deep blue light orange
[](#cb416-9)blue delight
[](#cb416-10)
[](#cb416-11)# you can also use -l instead of -L1
[](#cb416-12)$ printf '  apple   banana cherry\n\t\tdragon unicorn   \n' | xargs -L1
[](#cb416-13)apple banana cherry
[](#cb416-14)dragon unicorn
```

> ![info](media/file0.svg) Note that `xargs -L1` is not the same as `awk '{$1=$1} 1'` since `xargs` will discard blank lines. Also, trailing blank characters will cause the next line to be considered as part of the current line. For example:
> 
> ```
> [](#cb417-1)# no trailing blanks
> [](#cb417-2)$ printf 'xerox apple\nregex   go  sea\n' | xargs -L1
> [](#cb417-3)xerox apple
> [](#cb417-4)regex go sea
> [](#cb417-5)
> [](#cb417-6)# with trailing blanks
> [](#cb417-7)$ printf 'xerox apple  \nregex   go  sea\n' | xargs -L1
> [](#cb417-8)xerox apple regex go sea
> ```

Use `-d` option to change the input delimiter from whitespace to some other single character. For example:

```
[](#cb418-1)$ printf '1,2,3,4,5,6' | xargs -d, -n3
[](#cb418-2)1 2 3
[](#cb418-3)4 5 6
```

## Exercises

> ![info](media/file0.svg) Use [example_files/text_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files/text_files) directory for input files used in the following exercises.

**1)** Generate the following sequence.

```
[](#cb419-1)# ???
[](#cb419-2)100
[](#cb419-3)95
[](#cb419-4)90
[](#cb419-5)85
[](#cb419-6)80
```

**2)** Is the sequence shown below possible to generate with `seq`? If so, how?

```
[](#cb420-1)# ???
[](#cb420-2)01.5,02.5,03.5,04.5,05.5
```

**3)** Display three random words from `/usr/share/dict/words` (or equivalent dictionary word file) containing `s` and `e` and `t` in any order. The output shown below is just an example.

```
[](#cb421-1)# ???
[](#cb421-2)supplemental
[](#cb421-3)foresight
[](#cb421-4)underestimates
```

**4)** Briefly describe the purpose of the `shuf` command options `-i`, `-e` and `-r`.

**5)** Why does the below command not work as expected? What other tools can you use in such cases?

```
[](#cb422-1)# not working as expected
[](#cb422-2)$ echo 'apple,banana,cherry,dates' | cut -d, -f3,1,3
[](#cb422-3)apple,cherry
[](#cb422-4)
[](#cb422-5)# expected output
[](#cb422-6)# ???
[](#cb422-7)cherry,apple,cherry
```

**6)** Display except the second field in the format shown below. Can you construct two different solutions?

```
[](#cb423-1)$ echo 'apple,banana,cherry,dates' | cut # ???
[](#cb423-2)apple cherry dates
[](#cb423-3)
[](#cb423-4)$ echo '2,3,4,5,6,7,8' | cut # ???
[](#cb423-5)2 4 5 6 7 8
```

**7)** Extract first three characters from the input lines as shown below. Can you also use the `head` command for this purpose? If not, why not?

```
[](#cb424-1)$ printf 'apple\nbanana\ncherry\ndates\n' | cut # ???
[](#cb424-2)app
[](#cb424-3)ban
[](#cb424-4)che
[](#cb424-5)dat
```

**8)** Display only the first and third columns of the `scores.csv` input file in the format as shown below. Note that only space characters are present between the two columns, not tab.

```
[](#cb425-1)$ cat scores.csv
[](#cb425-2)Name,Maths,Physics,Chemistry
[](#cb425-3)Ith,100,100,100
[](#cb425-4)Cy,97,98,95
[](#cb425-5)Lin,78,83,80
[](#cb425-6)
[](#cb425-7)# ???
[](#cb425-8)Name  Physics
[](#cb425-9)Ith   100
[](#cb425-10)Cy    98
[](#cb425-11)Lin   83
```

**9)** Display the contents of `table.txt` in the format shown below.

```
[](#cb426-1)# ???
[](#cb426-2)brown   bread   mat     hair   42
[](#cb426-3)blue    cake    mug     shirt  -7
[](#cb426-4)yellow  banana  window  shoes  3.14
```

**10)** Implement [ROT13](https://en.wikipedia.org/wiki/ROT13) cipher using the `tr` command.

```
[](#cb427-1)$ echo 'Hello World' | tr # ???
[](#cb427-2)Uryyb Jbeyq
[](#cb427-3)$ echo 'Uryyb Jbeyq' | tr # ???
[](#cb427-4)Hello World
```

**11)** Retain only alphabets, digits and whitespace characters.

```
[](#cb428-1)$ echo 'Apple_42 cool,blue Dragon:army' | # ???
[](#cb428-2)Apple42 coolblue Dragonarmy
```

**12)** Use `tr` to get the output shown below.

```
[](#cb429-1)$ echo '!!hhoowwww !!aaaaaareeeeee!! yyouuuu!!' | tr # ???
[](#cb429-2)how are you
```

**13)** `paste -s` works separately for multiple input files. How would you workaround this if you needed to treat input as a single source?

```
[](#cb430-1)# this works individually for each input file
[](#cb430-2)$ paste -sd, fruits.txt ip.txt
[](#cb430-3)banana,papaya,mango
[](#cb430-4)deep blue,light orange,blue delight
[](#cb430-5)
[](#cb430-6)# expected output
[](#cb430-7)# ???
[](#cb430-8)banana,papaya,mango,deep blue,light orange,blue delight
```

**14)** Use appropriate options to get the expected output shown below.

```
[](#cb431-1)# default output
[](#cb431-2)$ paste fruits.txt ip.txt
[](#cb431-3)banana  deep blue
[](#cb431-4)papaya  light orange
[](#cb431-5)mango   blue delight
[](#cb431-6)
[](#cb431-7)# expected output
[](#cb431-8)$ paste # ???
[](#cb431-9)banana
[](#cb431-10)deep blue
[](#cb431-11)papaya
[](#cb431-12)light orange
[](#cb431-13)mango
[](#cb431-14)blue delight
```

**15)** Use the `pr` command to get the expected output shown below.

```
[](#cb432-1)$ seq -w 16 | pr # ???
[](#cb432-2)01,02,03,04
[](#cb432-3)05,06,07,08
[](#cb432-4)09,10,11,12
[](#cb432-5)13,14,15,16
[](#cb432-6)
[](#cb432-7)$ seq -w 16 | pr # ???
[](#cb432-8)01,05,09,13
[](#cb432-9)02,06,10,14
[](#cb432-10)03,07,11,15
[](#cb432-11)04,08,12,16
```

**16)** Use the `pr` command to join the input files `fruits.txt` and `ip.txt` as shown below.

```
[](#cb433-1)# ???
[](#cb433-2)banana : deep blue
[](#cb433-3)papaya : light orange
[](#cb433-4)mango : blue delight
```

**17)** The `cut` command doesn't support a way to choose the last `N` fields. Which tool presented in this chapter can be combined to work with `cut` to get the output shown below?

```
[](#cb434-1)# last two characters from each line
[](#cb434-2)$ printf 'apple\nbanana\ncherry\ndates\n' | # ???
[](#cb434-3)le
[](#cb434-4)na
[](#cb434-5)ry
[](#cb434-6)es
```

**18)** Go through `split` documentation and use appropriate options to get the output shown below for the input file `purchases.txt`.

```
[](#cb435-1)# split input by 3 lines (max) at a time
[](#cb435-2)# ???
[](#cb435-3)
[](#cb435-4)$ head xa?
[](#cb435-5)==> xaa <==
[](#cb435-6)coffee
[](#cb435-7)tea
[](#cb435-8)washing powder
[](#cb435-9)
[](#cb435-10)==> xab <==
[](#cb435-11)coffee
[](#cb435-12)toothpaste
[](#cb435-13)tea
[](#cb435-14)
[](#cb435-15)==> xac <==
[](#cb435-16)soap
[](#cb435-17)tea
[](#cb435-18)
[](#cb435-19)$ rm xa?
```

**19)** Go through `split` documentation and use appropriate options to get the output shown below.

```
[](#cb436-1)$ echo 'apple,banana,cherry,dates' | split # ???
[](#cb436-2)
[](#cb436-3)$ head xa?
[](#cb436-4)==> xaa <==
[](#cb436-5)apple,
[](#cb436-6)==> xab <==
[](#cb436-7)banana,
[](#cb436-8)==> xac <==
[](#cb436-9)cherry,
[](#cb436-10)==> xad <==
[](#cb436-11)dates
[](#cb436-12)
[](#cb436-13)$ rm xa?
```

**20)** Split the input file `purchases.txt` such that the text before a line containing `powder` is part of the first file and the rest are part of the second file as shown below.

```
[](#cb437-1)# ???
[](#cb437-2)
[](#cb437-3)$ head xx0?
[](#cb437-4)==> xx00 <==
[](#cb437-5)coffee
[](#cb437-6)tea
[](#cb437-7)
[](#cb437-8)==> xx01 <==
[](#cb437-9)washing powder
[](#cb437-10)coffee
[](#cb437-11)toothpaste
[](#cb437-12)tea
[](#cb437-13)soap
[](#cb437-14)tea
[](#cb437-15)
[](#cb437-16)$ rm xx0?
```

**21)** Write a generic solution that transposes comma delimited data. Example input/output is shown below. You can use any tool(s) presented in this book.

```
[](#cb438-1)$ cat scores.csv 
[](#cb438-2)Name,Maths,Physics,Chemistry
[](#cb438-3)Ith,100,100,100
[](#cb438-4)Cy,97,98,95
[](#cb438-5)Lin,78,83,80
[](#cb438-6)
[](#cb438-7)# ???
[](#cb438-8)Name,Ith,Cy,Lin
[](#cb438-9)Maths,100,97,78
[](#cb438-10)Physics,100,98,83
[](#cb438-11)Chemistry,100,95,80
```

**22)** Reshape the contents of `table.txt` to the expected output shown below.

```
[](#cb439-1)$ cat table.txt
[](#cb439-2)brown bread mat hair 42
[](#cb439-3)blue cake mug shirt -7
[](#cb439-4)yellow banana window shoes 3.14
[](#cb439-5)
[](#cb439-6)# ???
[](#cb439-7)brown   bread  mat     hair
[](#cb439-8)42      blue   cake    mug
[](#cb439-9)shirt   -7     yellow  banana
[](#cb439-10)window  shoes  3.14
```

# Shell Scripting

This chapter will cover basics of shell scripting with `bash`. You'll learn about declaring variables, control structures, working with arguments passed to a script, getting user input and so on.

> ![info](media/file0.svg) The [example_files](https://github.com/learnbyexample/cli-computing/tree/master/example_files) directory has all the shell scripts discussed in this chapter. However, it is recommended that you type the scripts manually using your favorite text editor and refer to the `example_files/shell_scripting` directory only if necessary.

## Need for scripting

From [wikipedia: Scripting language](https://en.wikipedia.org/wiki/Scripting_language):

> A scripting language or script language is a programming language for a runtime system that automates the execution of tasks that would otherwise be performed individually by a human operator. Scripting languages are usually interpreted at runtime rather than compiled.

> Typical scripting languages are intended to be very fast to learn and write in, either as short source code files or interactively in a read–eval–print loop (REPL, language shell). This generally implies relatively simple syntax and semantics; typically a "script" (code written in the scripting language) is executed from start to finish, as a "script", with no explicit entry point.

From [wikipedia: Shell script](https://en.wikipedia.org/wiki/Shell_script):

> A shell script is a computer program designed to be run by the Unix shell, a command-line interpreter. The various dialects of shell scripts are considered to be scripting languages. Typical operations performed by shell scripts include file manipulation, program execution, and printing text. A script which sets up the environment, runs the program, and does any necessary cleanup or logging, is called a wrapper.

See also [Difference between scripting and programming languages](https://stackoverflow.com/q/17253545/4082052).

## Executable script

There are several ways you can execute commands from a file. This section shows an example of creating an executable script. Consider this sample script saved in a file named `hello.sh`:

```
[](#cb440-1)#!/bin/bash
[](#cb440-2)
[](#cb440-3)echo "Hello $USER"
[](#cb440-4)echo "Today is $(date -u +%A)"
[](#cb440-5)echo 'Have a nice day'
```

The first line in the above script has two parts:

*   `/bin/bash` is the path of `bash` interpreter
    *   you can use `type bash` to get the path on your system
*   `#!` is known as [shebang or hashbang](https://en.wikipedia.org/wiki/Shebang_(Unix)) which directs the program loader to use the interpreter path provided
    *   see also [stackoverflow: comparison between #!/usr/bin/env and #!/bin/bash?](https://stackoverflow.com/q/21612980/4082052)
    *   the `#` character starts a comment, `#!` is only special at the start of the script

Use `chmod` to add executable permission to the file and then run the script:

```
[](#cb441-1)$ chmod +x hello.sh
[](#cb441-2)
[](#cb441-3)$ ./hello.sh 
[](#cb441-4)Hello learnbyexample
[](#cb441-5)Today is Wednesday
[](#cb441-6)Have a nice day
```

If you want to use just the script name to execute it, the file has to be located in one of the `PATH` folders. Otherwise, you'll have to provide the script's path (absolute or relative) in order to execute it (as shown in the above illustration).

> ![info](media/file2.svg) `.sh` is typically used as the file extension for shell scripts. It is also common to *not* have an extension at all, especially for executable scripts.

## Passing file argument to bash

You can also just pass a regular file as an argument to the `bash` command. In this case, the shebang isn't needed (though it wouldn't cause any issues either, since it will be treated as a comment).

```
[](#cb442-1)$ cat greeting.sh
[](#cb442-2)echo 'hello'
[](#cb442-3)echo 'have a nice day'
[](#cb442-4)
[](#cb442-5)$ bash greeting.sh
[](#cb442-6)hello
[](#cb442-7)have a nice day
```

## Sourcing script

Yet another way to execute a script is to *source* it using the `source` (or `.`) builtin command. A major difference from the previous methods is that the script is executed in the current shell environment context instead of a sub-shell. A common use case is sourcing `~/.bashrc` and alias/functions (if they are saved in a separate file).

Here's an example:

```
[](#cb443-1)$ cat prev_cmd.sh
[](#cb443-2)prev=$(fc -ln -2 | sed 's/^\s*//; q')
[](#cb443-3)echo "$prev"
[](#cb443-4)
[](#cb443-5)# 'echo' here is just a sample command for illustration purposes
[](#cb443-6)$ echo 'hello'
[](#cb443-7)hello
[](#cb443-8)# sourcing the script correctly gives the previous command
[](#cb443-9)$ source prev_cmd.sh
[](#cb443-10)echo 'hello'
[](#cb443-11)
[](#cb443-12)$ echo 'hello'
[](#cb443-13)hello
[](#cb443-14)# no output when the script is executed in a sub-shell
[](#cb443-15)$ bash prev_cmd.sh
```

> ![info](media/file0.svg) `fc` is a builtin command to manipulate the history of commands you've used from the terminal. See [bash manual: History Builtins](https://www.gnu.org/software/bash/manual/bash.html#Bash-History-Builtins) for more details.

## Comments

Single line comments can be inserted after the `#` character, either at the start of a line or after an instruction.

```
[](#cb444-1)$ cat comments.sh
[](#cb444-2)# this is a comment on its own line
[](#cb444-3)echo 'hello' # and this is a comment after a command
[](#cb444-4)
[](#cb444-5)$ bash comments.sh
[](#cb444-6)hello
```

> ![info](media/file2.svg) See this [unix.stackexchange thread](https://unix.stackexchange.com/q/37411/109046) for emulating multiline comments.

## Variables

Here's a basic example of assigning a variable and accessing its value:

```
[](#cb445-1)$ name='learnbyexample'
[](#cb445-2)
[](#cb445-3)$ echo "$name"
[](#cb445-4)learnbyexample
```

As seen above, you need to use the `$` prefix while accessing the value stored in a variable. You can use `${variable}` syntax to distinguish between the variable and other parts of the string. Using appropriate quotes is recommended, unless otherwise necessary.

You can append to a variable by using the `+=` operator. Here's an example:

```
[](#cb446-1)$ colors='blue'
[](#cb446-2)$ echo "$colors"
[](#cb446-3)blue
[](#cb446-4)
[](#cb446-5)$ colors+=' green'
[](#cb446-6)$ echo "$colors"
[](#cb446-7)blue green
```

You can use the `declare` builtin to add attributes to variables. For example, the `-i` option for treating the variable as an integer, `-r` option for readonly, etc. These attributes can change the behavior of operators like `=` and `+=` for those variables. See [bash manual: Shell-Parameters](https://www.gnu.org/software/bash/manual/bash.html#Shell-Parameters) and [bash manual: declare](https://www.gnu.org/software/bash/manual/bash.html#index-declare) for more details.

```
[](#cb447-1)$ declare -i num=5
[](#cb447-2)$ echo "$num"
[](#cb447-3)5
[](#cb447-4)$ num+=42
[](#cb447-5)$ echo "$num"
[](#cb447-6)47
[](#cb447-7)
[](#cb447-8)$ declare -r color='brown'
[](#cb447-9)$ echo "$color"
[](#cb447-10)brown
[](#cb447-11)$ color+=' green'
[](#cb447-12)bash: color: readonly variable
```

> ![info](media/file0.svg) ![warning](media/file1.svg) Assigning variables is one of the most common source for errors. Unlike most programming languages, spaces are *not* allowed around the `=` sign. That is because space is a shell metacharacter. Another common issue is using quotes (or not) around the value. Here are some examples:
> 
> ```
> [](#cb448-1)$ num = 42
> [](#cb448-2)num: command not found
> [](#cb448-3)
> [](#cb448-4)$ greeting=hello world
> [](#cb448-5)world: command not found
> [](#cb448-6)$ greeting='hello world'
> [](#cb448-7)$ echo "$greeting"
> [](#cb448-8)hello world
> [](#cb448-9)
> [](#cb448-10)# using quotes is NOT desirable here
> [](#cb448-11)$ dir_path=~/reports
> [](#cb448-12)$ echo "$dir_path"
> [](#cb448-13)/home/learnbyexample/reports
> [](#cb448-14)$ dir_path='~/reports'
> [](#cb448-15)$ echo "$dir_path"
> [](#cb448-16)~/reports
> ```

## Arrays

From [bash manual: Arrays](https://www.gnu.org/software/bash/manual/bash.html#Arrays):

> Bash provides one-dimensional indexed and associative array variables. Any variable may be used as an indexed array; the `declare` builtin will explicitly declare an array. There is no maximum limit on the size of an array, nor any requirement that members be indexed or assigned contiguously. Indexed arrays are referenced using integers and are zero-based; associative arrays use arbitrary strings.

Here's an example of assigning an indexed array and various ways of accessing the elements:

```
[](#cb449-1)$ fruits=('apple' 'fig' 'mango')
[](#cb449-2)
[](#cb449-3)# first element
[](#cb449-4)$ echo "${fruits[0]}"
[](#cb449-5)apple
[](#cb449-6)
[](#cb449-7)# last element
[](#cb449-8)$ echo "${fruits[-1]}"
[](#cb449-9)mango
[](#cb449-10)
[](#cb449-11)# all elements (example with for loop will be discussed later on)
[](#cb449-12)$ echo "${fruits[@]}"
[](#cb449-13)apple fig mango
[](#cb449-14)$ printf '%s\n' "${fruits[@]}"
[](#cb449-15)apple
[](#cb449-16)fig
[](#cb449-17)mango
```

## Parameter Expansion

Bash provides several useful ways to extract and modify contents of parameters and variables (including arrays). Some of these features will be discussed in this section.

*1)* Substring extraction using `${parameter:offset}` syntax to get all characters from the given index:

```
[](#cb450-1)$ city='Lucknow'
[](#cb450-2)
[](#cb450-3)# all characters from index 4 onwards
[](#cb450-4)# indexing starts from 0
[](#cb450-5)$ echo "${city:4}"
[](#cb450-6)now
[](#cb450-7)
[](#cb450-8)# last two characters
[](#cb450-9)# space before the negative sign is compulsory here,
[](#cb450-10)# since ${parameter:-word} is a different feature
[](#cb450-11)$ echo "${city: -2}"
[](#cb450-12)ow
```

When applied to arrays, substring extraction will give you those elements:

```
[](#cb451-1)$ fruits=('apple' 'fig' 'mango')
[](#cb451-2)
[](#cb451-3)# all elements from index 1
[](#cb451-4)$ echo "${fruits[@]:1}"
[](#cb451-5)fig mango
```

*2)* Substring extraction using `${parameter:offset:length}` syntax to get specific number of characters from the given index:

```
[](#cb452-1)$ city='Lucknow'
[](#cb452-2)
[](#cb452-3)# 4 characters starting from index 0
[](#cb452-4)# can also use: echo "${city::4}"
[](#cb452-5)$ echo "${city:0:4}"
[](#cb452-6)Luck
[](#cb452-7)
[](#cb452-8)# 2 characters starting from index -4 (4th character from the end)
[](#cb452-9)$ echo "${city: -4:2}"
[](#cb452-10)kn
[](#cb452-11)
[](#cb452-12)# except last 2 characters
[](#cb452-13)$ echo "${city::-2}"
[](#cb452-14)Luckn
```

*3)* `${#parameter}` will give you the length of the string and `${#array[@]}` will give you the number of elements in the array:

```
[](#cb453-1)$ city='Lucknow'
[](#cb453-2)$ echo "${#city}"
[](#cb453-3)7
[](#cb453-4)
[](#cb453-5)$ fruits=('apple' 'fig' 'mango')
[](#cb453-6)$ echo "${#fruits[@]}"
[](#cb453-7)3
```

*4)* `${parameter#glob}` will remove the shortest match from the start of the string. You can also use extended globs if enabled via `shopt` builtin. `${parameter##glob}` will remove the longest match from the start of the string. Here are some examples:

```
[](#cb454-1)$ s='this is his life history'
[](#cb454-2)
[](#cb454-3)# shortest match is deleted
[](#cb454-4)$ echo "${s#*is}"
[](#cb454-5) is his life history
[](#cb454-6)# longest match is deleted
[](#cb454-7)$ echo "${s##*is}"
[](#cb454-8)tory
[](#cb454-9)
[](#cb454-10)# assuming extglob is enabled
[](#cb454-11)$ echo "${s#+([^ ])}"
[](#cb454-12)his is his life history
[](#cb454-13)$ echo "${s##+([^ ])}"
[](#cb454-14) is his life history
[](#cb454-15)
[](#cb454-16)# for arrays, the processing is applied to each element
[](#cb454-17)$ fruits=('apple' 'fig' 'mango')
[](#cb454-18)$ echo "${fruits[@]#*[aeiou]}"
[](#cb454-19)pple g ngo
```

*5)* You can use `${parameter%glob}` to remove the shortest match from the end of the string. `${parameter%%glob}` will remove the longest match from the end of the string. Here are some examples:

```
[](#cb455-1)$ s='this is his life history'
[](#cb455-2)
[](#cb455-3)$ echo "${s%is*}"
[](#cb455-4)this is his life h
[](#cb455-5)$ echo "${s%%is*}"
[](#cb455-6)th
[](#cb455-7)
[](#cb455-8)$ fruits=('apple' 'fig' 'mango')
[](#cb455-9)$ echo "${fruits[@]%[aeiou]*}"
[](#cb455-10)appl f mang
```

*6)* `${parameter/glob/string}` replaces the first matching occurrence with the given replacement string and `${parameter//glob/string}` will replace all the matching occurrences. You can leave out the `/string` portion when you want to delete the matching occurrences. The `glob` will match the longest portion, similar to greedy behavior in regular expressions. Here are some examples:

```
[](#cb456-1)$ ip='this is a sample string'
[](#cb456-2)
[](#cb456-3)# first occurrence of 'is' is replaced with '123'
[](#cb456-4)$ echo "${ip/is/123}"
[](#cb456-5)th123 is a sample string
[](#cb456-6)# all occurrences of 'is' are replaced with '123'
[](#cb456-7)$ echo "${ip//is/123}"
[](#cb456-8)th123 123 a sample string
[](#cb456-9)
[](#cb456-10)# replace all occurrences of 'am' or 'in' with '-'
[](#cb456-11)$ echo "${ip//@(am|in)/-}"
[](#cb456-12)this is a s-ple str-g
[](#cb456-13)
[](#cb456-14)# matches from the first 'is' to the last 's' in the input
[](#cb456-15)$ echo "${ip/is*s/ X }"
[](#cb456-16)th X tring
[](#cb456-17)
[](#cb456-18)# deletes first occurrence of 's'
[](#cb456-19)$ echo "${ip/s}"
[](#cb456-20)thi is a sample string
[](#cb456-21)# deletes all occurrences of 's'
[](#cb456-22)$ echo "${ip//s}"
[](#cb456-23)thi i a ample tring
```

*7)* You can use `${parameter/#glob/string}` to match only at the start of the string and `${parameter/%glob/string}` to match only at the end of the string.

```
[](#cb457-1)$ ip='spare'
[](#cb457-2)
[](#cb457-3)# remove only from the start of the string
[](#cb457-4)$ echo "${ip/#sp}"
[](#cb457-5)are
[](#cb457-6)$ echo "${ip/#par}"
[](#cb457-7)spare
[](#cb457-8)# example with replacement string
[](#cb457-9)$ echo "${ip/#sp/fl}"
[](#cb457-10)flare
[](#cb457-11)
[](#cb457-12)# remove only from the end of the string
[](#cb457-13)$ echo "${ip/%re}"
[](#cb457-14)spa
[](#cb457-15)$ echo "${ip/%par}"
[](#cb457-16)spare
```

*8)* `${parameter^glob}` can change only the first character to uppercase if matched by the glob. `${parameter^^glob}` changes all the matching characters to uppercase (anywhere in the input string). You should provide a glob that only matches one character in length. If the glob is omitted, entire parameter will be matched. These rules also apply to the lowercase and swap case versions discussed later.

```
[](#cb458-1)$ fruit='apple'
[](#cb458-2)
[](#cb458-3)# uppercase the first character
[](#cb458-4)$ echo "${fruit^}"
[](#cb458-5)Apple
[](#cb458-6)# uppercase the entire parameter
[](#cb458-7)$ echo "${fruit^^}"
[](#cb458-8)APPLE
[](#cb458-9)
[](#cb458-10)# first character doesn't match the 'g-z' range, so no change
[](#cb458-11)$ echo "${fruit^[g-z]}"
[](#cb458-12)apple
[](#cb458-13)# uppercase all letters in the 'g-z' range
[](#cb458-14)$ echo "${fruit^^[g-z]}"
[](#cb458-15)aPPLe
[](#cb458-16)# uppercase all letters in the 'a-e' or 'j-m' ranges
[](#cb458-17)$ echo "${fruit^^[a-ej-m]}"
[](#cb458-18)AppLE
[](#cb458-19)
[](#cb458-20)# this won't work since 'sky-' is not a single character
[](#cb458-21)$ color='sky-rose'
[](#cb458-22)$ echo "${color^^*-}"
[](#cb458-23)sky-rose
```

*9)* To change the characters to lowercase, use `,` and `,,` as shown below:

```
[](#cb459-1)$ fruit='APPLE'
[](#cb459-2)
[](#cb459-3)$ echo "${fruit,}"
[](#cb459-4)aPPLE
[](#cb459-5)$ echo "${fruit,,}"
[](#cb459-6)apple
[](#cb459-7)
[](#cb459-8)$ echo "${fruit,,[G-Z]}"
[](#cb459-9)ApplE
```

*10)* To swap case, use `~` and `~~` as shown below. Note that this seems to be deprecated, since it is no longer mentioned in the `bash` manual.

```
[](#cb460-1)$ fruit='aPPle'
[](#cb460-2)
[](#cb460-3)# swap case only for the first character
[](#cb460-4)$ echo "${fruit~}"
[](#cb460-5)APPle
[](#cb460-6)# swap case for all the characters
[](#cb460-7)$ echo "${fruit~~}"
[](#cb460-8)AppLE
[](#cb460-9)
[](#cb460-10)# swap case for characters matching the given character set
[](#cb460-11)$ echo "${fruit~~[g-zG-Z]}"
[](#cb460-12)appLe
```

> ![info](media/file2.svg) See [bash manual: Shell Parameter Expansion](https://www.gnu.org/software/bash/manual/bash.html#Shell-Parameter-Expansion) for more details and other types of expansions.

## Command Line Arguments

Command line arguments passed to a script (or a function) are saved in positional parameters starting with `1`, `2`, `3` etc. `0` contains the name of the shell or shell script. `@` contains all the positional parameters starting from `1`. Use `#` to get the number of positional parameters. Similar to variables, you need to use a `$` prefix to get the value stored in these parameters. If the parameter number requires more than a single digit, you have to necessarily enclose them in `{}` (for example, `${12}` to get the value of the twelfth parameter).

Here's an example script that accepts two arguments:

```
[](#cb461-1)$ cat command_line_arguments.sh
[](#cb461-2)echo "No. of lines in '$1' is $(wc -l < "$1")"
[](#cb461-3)echo "No. of lines in '$2' is $(wc -l < "$2")"
[](#cb461-4)
[](#cb461-5)$ seq 12 > 'test file.txt'
[](#cb461-6)
[](#cb461-7)$ bash command_line_arguments.sh hello.sh test\ file.txt 
[](#cb461-8)No. of lines in 'hello.sh' is 5
[](#cb461-9)No. of lines in 'test file.txt' is 12
```

**Further Reading**

*   [unix.stackexchange: shell script choking on whitespace or other special characters](https://unix.stackexchange.com/q/131766/109046)
*   [bash manual: Special Parameters](https://www.gnu.org/software/bash/manual/bash.html#Special-Parameters)

## Conditional Expressions

You can test a condition within `[[` and `]]` to get a success (`0`) or failure (`1` or higher) exit status and take action accordingly. Bash provides several options and operators that you can use. Space is required after `[[` and before `]]` for this compound command to function.

> ![info](media/file0.svg) Operators `;`, `&&` and `||` will be used in this section to keep the examples terser. `if-else` and other control structures will be discussed later.

### Options

The `-e` option checks if the given path argument exists or not. Add a `!` prefix to negate the condition.

```
[](#cb462-1)# change to the 'example_files/shell_scripting' directory for this section
[](#cb462-2)
[](#cb462-3)$ [[ -e hello.sh ]] && echo 'found' || echo 'not found'
[](#cb462-4)found
[](#cb462-5)
[](#cb462-6)$ [[ -e xyz.txt ]] && echo 'found' || echo 'not found'
[](#cb462-7)not found
[](#cb462-8)
[](#cb462-9)# exit status
[](#cb462-10)$ [[ -e hello.sh ]] ; echo $?
[](#cb462-11)0
[](#cb462-12)$ [[ -e xyz.txt ]] ; echo $?
[](#cb462-13)1
[](#cb462-14)$ [[ ! -e xyz.txt ]] ; echo $?
[](#cb462-15)0
```

You can use `-d` and `-f` to check if the path is a valid directory and file respectively. The `-s` option checks if the file exists and its size is greater than zero. The `-x` option checks if the file exists and is executable. See `help test` and [bash manual: Conditional Expressions](https://www.gnu.org/software/bash/manual/bash.html#Bash-Conditional-Expressions) for a complete list of such options.

### String comparisons

*   `s1 = s2` or `s1 == s2` checks if two strings are equal
    *   unquoted portions of `s2` will be treated as a wildcard while testing against `s1`
    *   `extglob` would be considered as enabled for such comparisons
*   `s1 != s2` checks if strings are *not* equal
    *   unquoted portions of `s2` will be treated as a wildcard while testing against `s1`
    *   `extglob` would be considered as enabled for such comparisons
*   `s1 < s2` checks if `s1` sorts before `s2` lexicographically
*   `s1 > s2` checks if `s1` sorts after `s2` lexicographically
*   `s1 =~ s2` checks if `s1` matches the POSIX extended regular expression provided by `s2`
    *   exit status will be `2` if `s2` is not a valid regexp

Here are some examples for equal and not-equal comparisons:

```
[](#cb463-1)$ fruit='apple'
[](#cb463-2)$ [[ $fruit == 'apple' ]] && echo 'true' || echo 'false'
[](#cb463-3)true
[](#cb463-4)$ [[ $fruit == 'banana' ]] && echo 'true' || echo 'false'
[](#cb463-5)false
[](#cb463-6)
[](#cb463-7)# glob should be constructed to match the entire string
[](#cb463-8)$ [[ hello == h* ]] && echo 'true' || echo 'false'
[](#cb463-9)true
[](#cb463-10)# don't quote the glob!
[](#cb463-11)$ [[ hello == 'h*' ]] && echo 'true' || echo 'false'
[](#cb463-12)false
[](#cb463-13)
[](#cb463-14)# another example to emphasize that the glob should match the entire string
[](#cb463-15)$ [[ hello == e*o ]] && echo 'true' || echo 'false'
[](#cb463-16)false
[](#cb463-17)$ [[ hello == *e*o ]] && echo 'true' || echo 'false'
[](#cb463-18)true
[](#cb463-19)
[](#cb463-20)$ [[ hello != *a* ]] && echo 'true' || echo 'false'
[](#cb463-21)true
[](#cb463-22)$ [[ hello != *e* ]] && echo 'true' || echo 'false'
[](#cb463-23)false
```

Here are some examples for greater-than and less-than comparisons:

```
[](#cb464-1)$ [[ apple < banana ]] && echo 'true' || echo 'false'
[](#cb464-2)true
[](#cb464-3)$ [[ par < part ]] && echo 'true' || echo 'false'
[](#cb464-4)true
[](#cb464-5)
[](#cb464-6)$ [[ mango > banana ]] && echo 'true' || echo 'false'
[](#cb464-7)true
[](#cb464-8)$ [[ sun > moon && fig < papaya ]] && echo 'true' || echo 'false'
[](#cb464-9)true
[](#cb464-10)
[](#cb464-11)# don't use this to compare numbers!
[](#cb464-12)$ [[ 20 > 3 ]] && echo 'true' || echo 'false'
[](#cb464-13)false
[](#cb464-14)# -gt and other such operators will be discussed later
[](#cb464-15)$ [[ 20 -gt 3 ]] && echo 'true' || echo 'false'
[](#cb464-16)true
```

Here are some examples for regexp comparison. You can use the special array `BASH_REMATCH` to retrieve specific portions of the string that was matched. Index `0` gives entire matched portion, `1` gives the portion matched by the first capture group and so on.

```
[](#cb465-1)$ fruit='apple'
[](#cb465-2)$ [[ $fruit =~ ^a ]] && echo 'true' || echo 'false'
[](#cb465-3)true
[](#cb465-4)$ [[ $fruit =~ ^b ]] && echo 'true' || echo 'false'
[](#cb465-5)false
[](#cb465-6)
[](#cb465-7)# entire matched portion
[](#cb465-8)$ [[ $fruit =~ a.. ]] && echo "${BASH_REMATCH[0]}"
[](#cb465-9)app
[](#cb465-10)# portion matched by the first capture group
[](#cb465-11)$ [[ $fruit =~ a(..) ]] && echo "${BASH_REMATCH[1]}"
[](#cb465-12)pp
```

### Numeric comparisons

*   `n1 -eq n2` checks if two numbers are equal
*   `n1 -ne n2` checks if two numbers are *not* equal
*   `n1 -gt n2` checks if `n1` is greater than `n2`
*   `n1 -ge n2` checks if `n1` is greater than or equal to `n2`
*   `n1 -lt n2` checks if `n1` is less than `n2`
*   `n1 -le n2` checks if `n1` is less than or equal to `n2`

These operators support only integer comparisons.

```
[](#cb466-1)$ [[ 20 -gt 3 ]] && echo 'true' || echo 'false'
[](#cb466-2)true
[](#cb466-3)
[](#cb466-4)$ n1='42'
[](#cb466-5)$ n2='25'
[](#cb466-6)$ [[ $n1 -gt 30 && $n2 -lt 12 ]] && echo 'true' || echo 'false'
[](#cb466-7)false
```

Numeric arithmetic operations and comparisons can also be performed within the `((` and `))` compound command. Here are some sample comparisons:

```
[](#cb467-1)$ (( 20 > 3 )) && echo 'true' || echo 'false'
[](#cb467-2)
[](#cb467-3)$ n1='42'
[](#cb467-4)$ n2='25'
[](#cb467-5)$ (( n1 > 30 && n2 < 12 )) && echo 'true' || echo 'false'
[](#cb467-6)false
```

> ![info](media/file2.svg) Note that the `$` prefix was *not* used for variables in the above example. See [bash manual: Shell Arithmetic](https://www.gnu.org/software/bash/manual/bash.html#Shell-Arithmetic) for more details.

## Accepting user input interactively

You can use the `read` builtin command to accept input from the user interactively. If multiple variables are given as arguments to the `read` command, values will be assigned based on whitespace separation by default. Any pending values will be assigned to the last variable. Here are some examples:

```
[](#cb468-1)# press 'Enter' after the 'read' command
[](#cb468-2)# and also after you've finished entering the input
[](#cb468-3)$ read color
[](#cb468-4)light green
[](#cb468-5)$ echo "$color"
[](#cb468-6)light green
[](#cb468-7)
[](#cb468-8)# example with multiple variables
[](#cb468-9)$ read fruit qty
[](#cb468-10)apple 10
[](#cb468-11)$ echo "${fruit}: ${qty}"
[](#cb468-12)apple: 10
```

The `-p` option helps you to add a user prompt. Here is an example of getting two arguments from the user:

```
[](#cb469-1)$ cat user_input.sh
[](#cb469-2)read -p 'Enter two integers separated by spaces: ' num1 num2
[](#cb469-3)sum=$(( num1 + num2 ))
[](#cb469-4)echo "$num1 + $num2 = $sum"
[](#cb469-5)
[](#cb469-6)$ bash user_input.sh
[](#cb469-7)Enter two integers separated by spaces: -2 42
[](#cb469-8)-2 + 42 = 40
```

> ![info](media/file2.svg) You can use the `-a` option to assign an array, the `-d` option to specify a custom delimiter instead of newline for terminating user input and so on. See `help read` and [bash manual: Builtins](https://www.gnu.org/software/bash/manual/bash.html#Bash-Builtins) for more details.

## if then else

The keywords needed to construct an `if` control structure are `if`, `then`, `fi` and optionally `else` and `elif`. You can use compound commands like `[[` and `((` to provide the test condition. You can also directly use a command's exit status. Here's an example script:

```
[](#cb470-1)$ cat if_then_else.sh
[](#cb470-2)if (( $# != 1 )) ; then
[](#cb470-3)    echo 'Error! One file argument expected.' 1>&2
[](#cb470-4)    exit 1
[](#cb470-5)else
[](#cb470-6)    if [[ ! -f $1 ]] ; then
[](#cb470-7)        printf 'Error! %q is not a valid file\n' "$1" 1>&2
[](#cb470-8)        exit 1
[](#cb470-9)    else
[](#cb470-10)        echo "No. of lines in '$1' is $(wc -l < "$1")"
[](#cb470-11)    fi
[](#cb470-12)fi
```

`1>&2` is used in the above script to redirect error messages to the `stderr` stream. Sample script invocations are shown below:

```
[](#cb471-1)$ bash if_then_else.sh
[](#cb471-2)Error! One file argument expected.
[](#cb471-3)$ echo $?
[](#cb471-4)1
[](#cb471-5)
[](#cb471-6)$ bash if_then_else.sh xyz.txt
[](#cb471-7)Error! xyz.txt is not a valid file
[](#cb471-8)$ echo $?
[](#cb471-9)1
[](#cb471-10)
[](#cb471-11)$ bash if_then_else.sh hello.sh
[](#cb471-12)No. of lines in 'hello.sh' is 5
[](#cb471-13)$ echo $?
[](#cb471-14)0
```

Sometimes you just need to know if the intended command operation was successful or not and then take an action depending on the outcome. In such cases, you can provide the command directly after the `if` keyword. Note that `stdout` and `stderr` of the command will still be active unless redirected or suppressed using appropriate options.

For example, the `grep` command supports `-q` option to suppress `stdout`. Here's a script using that feature:

```
[](#cb472-1)$ cat search.sh 
[](#cb472-2)read -p 'Enter a search pattern: ' search
[](#cb472-3)
[](#cb472-4)if grep -q "$search" hello.sh ; then
[](#cb472-5)    echo "match found"
[](#cb472-6)else
[](#cb472-7)    echo "match not found"
[](#cb472-8)fi
```

Sample invocations for the above script:

```
[](#cb473-1)$ bash search.sh
[](#cb473-2)Enter a search pattern: echo
[](#cb473-3)match found
[](#cb473-4)
[](#cb473-5)$ bash search.sh
[](#cb473-6)Enter a search pattern: xyz
[](#cb473-7)match not found
```

## for loop

To construct a `for` loop, you'll need the `for`, `do` and `done` keywords. Here are some examples:

```
[](#cb474-1)# iterate over numbers generated using brace expansion
[](#cb474-2)$ for num in {2..4}; do echo "$num"; done
[](#cb474-3)2
[](#cb474-4)3
[](#cb474-5)4
[](#cb474-6)
[](#cb474-7)# iterate over files matched using wildcards
[](#cb474-8)# echo is used here for dry run testing
[](#cb474-9)$ for file in [gh]*.sh; do echo mv "$file" "$file.bkp"; done
[](#cb474-10)mv greeting.sh greeting.sh.bkp
[](#cb474-11)mv hello.sh hello.sh.bkp
```

As seen in the above examples, the space separated arguments provided after the `in` keyword are automatically assigned to the variable provided after the `for` keyword during each iteration.

Here's a modified example of the last example that accepts user provided command line arguments:

```
[](#cb475-1)$ cat for_loop.sh
[](#cb475-2)for file in "$@"; do 
[](#cb475-3)    echo mv "$file" "$file.bkp"
[](#cb475-4)done
[](#cb475-5)
[](#cb475-6)$ bash for_loop.sh [gh]*.sh
[](#cb475-7)mv greeting.sh greeting.sh.bkp
[](#cb475-8)mv hello.sh hello.sh.bkp
[](#cb475-9)
[](#cb475-10)$ bash for_loop.sh report.log ip.txt fruits.txt
[](#cb475-11)mv report.log report.log.bkp
[](#cb475-12)mv ip.txt ip.txt.bkp
[](#cb475-13)mv fruits.txt fruits.txt.bkp
```

Here's an example of iterating over an array:

```
[](#cb476-1)$ files=('report.log' 'pass_list.txt')
[](#cb476-2)$ for f in "${files[@]}"; do echo "$f"; done
[](#cb476-3)report.log
[](#cb476-4)pass_list.txt
```

> ![info](media/file2.svg) You can use `continue` and `break` to alter the loop flow depending on specific conditions. See [bash manual: Bourne Shell Builtins](https://www.gnu.org/software/bash/manual/bash.html#Bourne-Shell-Builtins) for more details.

> ![info](media/file0.svg) `for file;` is same as `for file in "$@";` since `in "$@"` is the default. I'd recommend using the explicit version.

## while loop

Here's a simple `while` loop construct. You'll see a more practical example later in this chapter.

```
[](#cb477-1)$ cat while_loop.sh
[](#cb477-2)i="$1"
[](#cb477-3)while (( i > 0 )) ; do
[](#cb477-4)    echo "$i"
[](#cb477-5)    (( i-- ))
[](#cb477-6)done
[](#cb477-7)
[](#cb477-8)$ bash while_loop.sh 3
[](#cb477-9)3
[](#cb477-10)2
[](#cb477-11)1
```

## Reading a file

The `while` loop combined with the `read` builtin helps you to process the content of a file. Here's an example of reading input contents line by line:

```
[](#cb478-1)$ cat read_file_lines.sh
[](#cb478-2)while IFS= read -r line; do
[](#cb478-3)    # do something with each line
[](#cb478-4)    wc -l "$line"
[](#cb478-5)done < "$1"
[](#cb478-6)
[](#cb478-7)$ printf 'hello.sh\ngreeting.sh\n' > files.txt
[](#cb478-8)$ bash read_file_lines.sh files.txt
[](#cb478-9)5 hello.sh
[](#cb478-10)2 greeting.sh
```

The intention in the above script is to treat each input line literally. So, the `IFS` (input field separator) special variable is set to empty string to prevent stripping of leading and trailing whitespaces. The `-r` option to the `read` builtin allows `\` in input to be treated literally. Note that the input filename is accepted as the first command line argument and redirected as `stdin` to the `while` loop. You also need to make sure that the last line of input ends with a newline character, otherwise the last line won't be processed.

You can change `IFS` to split the input line into different fields and specify appropriate number of variables to the `read` builtin. Here's an example:

```
[](#cb479-1)$ cat read_file_fields.sh
[](#cb479-2)while IFS=' : ' read -r field1 field2; do
[](#cb479-3)    echo "$field2,$field1"
[](#cb479-4)done < "$1"
[](#cb479-5)
[](#cb479-6)$ bash read_file_fields.sh <(printf 'apple : 3\nfig : 100\n')
[](#cb479-7)3,apple
[](#cb479-8)100,fig
```

You can pass a number to the `-n` option for the `read` builtin to process the input that many characters at a time. Here's an example:

```
[](#cb480-1)$ while read -r -n2 ip; do echo "$ip"; done <<< '\word'
[](#cb480-2)\w
[](#cb480-3)or
[](#cb480-4)d
```

> ![info](media/file0.svg) The `xargs` command can also be used for some of the cases discussed above. See [unix.stackexchange: parse each line of a text file as a command argument](https://unix.stackexchange.com/q/149726/109046) for examples.

## Functions

From [bash manual: Shell Functions](https://www.gnu.org/software/bash/manual/bash.html#Shell-Functions):

> Shell functions are a way to group commands for later execution using a single name for the group. They are executed just like a "regular" command. When the name of a shell function is used as a simple command name, the list of commands associated with that function name is executed. Shell functions are executed in the current shell context; no new process is created to interpret them.

You can use either of the syntax shown below to declare functions:

```
[](#cb481-1)fname () compound-command [ redirections ]
[](#cb481-2)
[](#cb481-3)function fname [()] compound-command [ redirections ]
```

Arguments to functions are passed in the same manner as those discussed earlier for shell scripts. Here's an example:

```
[](#cb482-1)$ cat functions.sh
[](#cb482-2)add_border ()
[](#cb482-3){
[](#cb482-4)    size='10'
[](#cb482-5)    color='grey'
[](#cb482-6)    if (( $# == 1 )) ; then
[](#cb482-7)        ip="$1"
[](#cb482-8)    elif (( $# == 2 )) ; then
[](#cb482-9)        if [[ $1 =~ ^[0-9]+$ ]] ; then
[](#cb482-10)            size="$1"
[](#cb482-11)        else
[](#cb482-12)            color="$1"
[](#cb482-13)        fi
[](#cb482-14)        ip="$2"
[](#cb482-15)    else
[](#cb482-16)        size="$1"
[](#cb482-17)        color="$2"
[](#cb482-18)        ip="$3"
[](#cb482-19)    fi
[](#cb482-20)
[](#cb482-21)    op="${ip%.*}_border.${ip##*.}"
[](#cb482-22)    echo convert -border "$size" -bordercolor "$color" "$ip" "$op"
[](#cb482-23)}
[](#cb482-24)
[](#cb482-25)add_border flower.png
[](#cb482-26)add_border 5 insect.png
[](#cb482-27)add_border red lake.png
[](#cb482-28)add_border 20 blue sky.png
```

In the above example, `echo` is used to display the command that will be executed. Remove `echo` if you want this script to actually create new images with the given parameters. The function accepts one to three arguments and uses default values when some of the arguments are not passed. Here's the output:

```
[](#cb483-1)$ bash functions.sh
[](#cb483-2)convert -border 10 -bordercolor grey flower.png flower_border.png
[](#cb483-3)convert -border 5 -bordercolor grey insect.png insect_border.png
[](#cb483-4)convert -border 10 -bordercolor red lake.png lake_border.png
[](#cb483-5)convert -border 20 -bordercolor blue sky.png sky_border.png
```

> ![info](media/file2.svg) Use `mogrify` instead of `convert` if you want to modify the input image inplace instead of creating a new image. These image manipulation commands are part of the [ImageMagick](https://imagemagick.org/) suite. As an exercise, modify the above function to generate error if the arguments passed do not match the expected usage. You can also accept output image name (or perhaps a different suffix) as an additional argument.

The shell script and user defined functions (which in turn might call itself or another function) can both have positional arguments. In such cases, the shell takes cares of restoring positional arguments to the earlier state once a function completes its tasks.

Functions have exit status as well, which is based on the last executed command by default. You can use the `return` builtin to provide your own custom exit status.

## Debugging

You can use the following `bash` options for debugging purposes:

*   `-x` print commands and their arguments as they are executed
*   `-v` verbose option, print shell input lines as they are read

Here's an example with `bash -x` option:

```
[](#cb484-1)$ bash -x search.sh
[](#cb484-2)+ read -p 'Enter a search pattern: ' search
[](#cb484-3)Enter a search pattern: xyz
[](#cb484-4)+ grep -q xyz hello.sh
[](#cb484-5)+ echo 'match not found'
[](#cb484-6)match not found
```

The lines starting with `+` show the command being executed with expanded values if applicable (the `search` variable to `grep -q` for example). Multiple `+` will be used if there are multiple expansions. Here's how `bash -xv` would behave for the same script:

```
[](#cb485-1)$ bash -xv search.sh
[](#cb485-2)read -p 'Enter a search pattern: ' search
[](#cb485-3)+ read -p 'Enter a search pattern: ' search
[](#cb485-4)Enter a search pattern: xyz
[](#cb485-5)
[](#cb485-6)if grep -q "$search" hello.sh ; then
[](#cb485-7)    echo "match found"
[](#cb485-8)else
[](#cb485-9)    echo "match not found"
[](#cb485-10)fi
[](#cb485-11)+ grep -q xyz hello.sh
[](#cb485-12)+ echo 'match not found'
[](#cb485-13)match not found
```

> ![info](media/file2.svg) You can also use `set -x` or `set -v` or `set -xv` from within the script to debug from a particular point onwards. You can turn off such debugging by using `+` instead of `-` as the option prefix (for example, `set +x`).

## shellcheck

[shellcheck](https://www.shellcheck.net/) is a static analysis tool that gives warnings and suggestions for scripts. You can use it online or install the tool for offline use. Given the various `bash` gotchas, this tool is highly recommended for both beginners and advanced users.

Consider this script:

```
[](#cb486-1)$ cat bad_script.sh
[](#cb486-2)#!/bin/bash
[](#cb486-3)
[](#cb486-4)greeting = 'hello world'
[](#cb486-5)echo "$greeting"
```

Here's how `shellcheck` reports the issue:

```
[](#cb487-1)$ shellcheck bad_script.sh
[](#cb487-2)
[](#cb487-3)In bad_script.sh line 3:
[](#cb487-4)greeting = 'hello world'
[](#cb487-5)         ^-- SC1068: Don't put spaces around the = in assignments
[](#cb487-6)                     (or quote to make it literal).
[](#cb487-7)
[](#cb487-8)For more information:
[](#cb487-9)  https://www.shellcheck.net/wiki/SC1068 -- Don't put spaces around the = in ...
```

> ![info](media/file2.svg) If the script doesn't have a shebang, you can use the `-s` option (`shellcheck -s bash` for example) to specify the shell application.

> ![info](media/file2.svg) ![warning](media/file1.svg) Note that `shellcheck` will not catch all types of issues. And suggestions should not be blindly accepted without understanding if that makes sense in the given context.

## Resource lists

Here are some more learning resources:

**Shell Scripting**

*   [Bash Guide](https://mywiki.wooledge.org/BashGuide) — aspires to teach good practice techniques for using Bash, and writing simple scripts
*   [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/) — solid foundation in how to write Bash scripts, to get the computer to do complex, repetitive tasks for you
*   [bash-handbook](https://github.com/denysdovhan/bash-handbook) — for those who want to learn Bash without diving in too deeply
*   [Serious Shell Programming](https://freebsdfrau.gitbook.io/serious-shell-programming/) — focuses on POSIX-compliant Bourne Shell for portability

**Handy tools, tips and reference**

*   [shellcheck](https://www.shellcheck.net/) — linting tool to avoid common mistakes and improve your script
*   [Bash reference cheatsheet](https://devmanual.gentoo.org/tools-reference/bash/index.html) — nicely formatted and explained well
*   [Bash scripting cheatsheet](https://devhints.io/bash) — quick reference to getting started with Bash scripting
*   Comprehensive lists on `mywiki.wooledge.org` website:
    *   [Bash FAQ](https://mywiki.wooledge.org/BashFAQ)
    *   [Bash Practices](https://mywiki.wooledge.org/BashGuide/Practices)
    *   [Bash Pitfalls](https://mywiki.wooledge.org/BashPitfalls)
*   [Google shell style guide](https://google.github.io/styleguide/shellguide.html)
*   Reliability and robustness
    *   [safe ways to do things in bash](https://github.com/anordal/shellharden/blob/master/how_to_do_things_safely_in_bash.md)
    *   [better scripting](https://robertmuth.blogspot.in/2012/08/better-bash-scripting-in-15-minutes.html)
    *   [robust scripting](https://www.davidpashley.com/articles/writing-robust-shell-scripts/)

**Specific topics**

*   Reading file(s)
    *   [Reading file](https://mywiki.wooledge.org/BashFAQ/001)
    *   [Loop through the lines of two files in parallel](https://unix.stackexchange.com/q/82541/109046)
*   [arrays](https://mywiki.wooledge.org/BashGuide/Arrays)
*   [nameref](https://unix.stackexchange.com/q/288886/109046)
    *   also see this [FAQ](https://mywiki.wooledge.org/BashFAQ/006)
*   getopts
    *   [getopts tutorial](https://wiki.bash-hackers.org/howto/getopts_tutorial)
    *   [handling command-line arguments](https://mywiki.wooledge.org/BashFAQ/035)
    *   [stackoverflow: getopts example](https://stackoverflow.com/q/16483119/4082052)
*   [Sending and Trapping Signals](https://mywiki.wooledge.org/SignalTrap)

## Exercises

> ![info](media/file0.svg) Use a temporary working directory before attempting the exercises. You can delete such practice directories afterwards.

**1)** What's wrong with the script shown below? Also, will the error go away if you use `bash try.sh` instead?

```
[](#cb488-1)$ printf '    \n!#/bin/bash\n\necho hello\n' > try.sh
[](#cb488-2)$ chmod +x try.sh
[](#cb488-3)$ ./try.sh
[](#cb488-4)./try.sh: line 2: !#/bin/bash: No such file or directory
[](#cb488-5)hello
[](#cb488-6)
[](#cb488-7)# expected output
[](#cb488-8)$ ./try.sh
[](#cb488-9)hello
```

**2)** Will the command shown below work? If so, what would be the output?

```
[](#cb489-1)$ echo echo hello | bash
```

**3)** When would you `source` a script instead of using `bash` or creating an executable using shebang?

**4)** How would you display the contents of a variable with `shake` appended?

```
[](#cb490-1)$ fruit='banana'
[](#cb490-2)
[](#cb490-3)$ echo # ???
[](#cb490-4)bananashake
```

**5)** What changes would you make to the code shown below to get the expected output?

```
[](#cb491-1)# default behavior
[](#cb491-2)$ n=100
[](#cb491-3)$ n+=100
[](#cb491-4)$ echo "$n"
[](#cb491-5)100100
[](#cb491-6)
[](#cb491-7)# expected output
[](#cb491-8)$ echo "$n"
[](#cb491-9)200
```

**6)** Is the following code valid? If so, what would be the output of the `echo` command?

```
[](#cb492-1)$ declare -a colors
[](#cb492-2)$ colors[3]='green'
[](#cb492-3)$ colors[1]='blue'
[](#cb492-4)
[](#cb492-5)$ echo "${colors[@]}"
[](#cb492-6)# ???
```

**7)** How would you get the last three characters of a variable's contents?

```
[](#cb493-1)$ fruit='banana'
[](#cb493-2)
[](#cb493-3)# ???
[](#cb493-4)ana
```

**8)** Will the second `echo` command give an error? If not, what will be the output?

```
[](#cb494-1)$ fruits=('apple' 'fig' 'mango')
[](#cb494-2)$ echo "${#fruits[@]}"
[](#cb494-3)3
[](#cb494-4)
[](#cb494-5)$ echo "${#fruits}"
[](#cb494-6)# ???
```

**9)** For the given array, use parameter expansion to remove characters until first/last space.

```
[](#cb495-1)$ colors=('green' 'dark brown' 'deep sky blue white')
[](#cb495-2)
[](#cb495-3)# remove till first space
[](#cb495-4)$ printf '%s\n' # ???
[](#cb495-5)green
[](#cb495-6)brown
[](#cb495-7)sky blue white
[](#cb495-8)
[](#cb495-9)# remove till last space
[](#cb495-10)$ printf '%s\n' # ???
[](#cb495-11)green
[](#cb495-12)brown
[](#cb495-13)white
```

**10)** Use parameter expansion to get the expected outputs shown below.

```
[](#cb496-1)$ ip='apple:banana:cherry:dragon'
[](#cb496-2)
[](#cb496-3)$ echo # ???
[](#cb496-4)apple:banana:cherry
[](#cb496-5)
[](#cb496-6)$ echo # ???
[](#cb496-7)apple
```

**11)** Is it possible to achieve the expected outputs shown below using parameter expansion? If so, how?

```
[](#cb497-1)$ ip='apple:banana:cherry:dragon'
[](#cb497-2)
[](#cb497-3)$ echo # ???
[](#cb497-4)apple 42 dragon
[](#cb497-5)
[](#cb497-6)$ echo # ???
[](#cb497-7)fig:banana:cherry:dragon
[](#cb497-8)
[](#cb497-9)$ echo # ???
[](#cb497-10)apple:banana:cherry:end
```

**12)** For the given input, change case as per the expected outputs shown below.

```
[](#cb498-1)$ ip='This is a Sample STRING'
[](#cb498-2)
[](#cb498-3)$ echo # ???
[](#cb498-4)THIS IS A SAMPLE STRING
[](#cb498-5)
[](#cb498-6)$ echo # ???
[](#cb498-7)this is a sample string
[](#cb498-8)
[](#cb498-9)$ echo # ???
[](#cb498-10)tHIS IS A sAMPLE string
```

**13)** Why does the conditional expression shown below fail?

```
[](#cb499-1)$ touch ip.txt
[](#cb499-2)$ [[-f ip.txt]] && echo 'file exists'
[](#cb499-3)[[-f: command not found
```

**14)** What is the difference between `==` and `=~` string comparison operators?

**15)** Why does the conditional expression used below show `failed` both times? Modify the expressions such that the first one correctly says `matched` instead of `failed`.

```
[](#cb500-1)$ f1='1234.txt'
[](#cb500-2)$ f2='report_2.txt'
[](#cb500-3)
[](#cb500-4)$ [[ $f1 == '+([0-9]).txt' ]] && echo 'matched' || echo 'failed'
[](#cb500-5)failed
[](#cb500-6)$ [[ $f2 == '+([0-9]).txt' ]] && echo 'matched' || echo 'failed'
[](#cb500-7)failed
```

**16)** Extract the digits that follow a `:` character for the given variable contents.

```
[](#cb501-1)$ item='chocolate:50'
[](#cb501-2)# ???
[](#cb501-3)50
[](#cb501-4)
[](#cb501-5)$ item='50 apples, fig:100, books-12'
[](#cb501-6)# ???
[](#cb501-7)100
```

**17)** Modify the expression shown below to correctly report `true` instead of `false`.

```
[](#cb502-1)$ num=12345
[](#cb502-2)$ [[ $num > 3 ]] && echo 'true' || echo 'false'
[](#cb502-3)false
```

**18)** Write a shell script named `array.sh` that accepts array input from the user followed by another input as index. Display the corresponding value at that index. Couple of examples are shown below.

```
[](#cb503-1)$ bash array.sh
[](#cb503-2)enter array elements: apple banana cherry
[](#cb503-3)enter array index: 1
[](#cb503-4)element at index '1' is: banana
[](#cb503-5)
[](#cb503-6)$ bash array.sh
[](#cb503-7)enter array elements: dragon unicorn centaur
[](#cb503-8)enter array index: -1
[](#cb503-9)element at index '-1' is: centaur
```

**19)** Write a shell script named `case.sh` that accepts exactly two command line arguments. The first argument can be `lower`, `upper` or `swap` and this should be used to transform the contents of the second argument. Examples script invocations are shown below, including what should happen if the command line arguments do not meet the script expectations.

```
[](#cb504-1)$ ./case.sh upper 'how are you?'
[](#cb504-2)HOW ARE YOU?
[](#cb504-3)
[](#cb504-4)$ ./case.sh lower PineAPPLE
[](#cb504-5)pineapple
[](#cb504-6)
[](#cb504-7)$ ./case.sh swap 'HeLlo WoRlD'
[](#cb504-8)hElLO wOrLd
[](#cb504-9)
[](#cb504-10)$ ./case.sh lower
[](#cb504-11)Error! Two arguments expected.
[](#cb504-12)$ echo $?
[](#cb504-13)1
[](#cb504-14)
[](#cb504-15)$ ./case.sh upper apple fig
[](#cb504-16)Error! Two arguments expected.
[](#cb504-17)
[](#cb504-18)$ ./case.sh lowercase DRAGON
[](#cb504-19)Error! 'lowercase' command not recognized.
[](#cb504-20)$ echo $?
[](#cb504-21)1
[](#cb504-22)
[](#cb504-23)$ ./case.sh apple lower 2> /dev/null
[](#cb504-24)$ echo $?
[](#cb504-25)1
```

**20)** Write a shell script named `loop.sh` that displays the number of lines for each of the files passed as command line arguments.

```
[](#cb505-1)$ printf 'apple\nbanana\ncherry\n' > items_1.txt
[](#cb505-2)$ printf 'dragon\nowl\nunicorn\ntroll\ncentaur\n' > items_2.txt
[](#cb505-3)
[](#cb505-4)$ bash loop.sh items_1.txt
[](#cb505-5)number of lines in 'items_1.txt' is: 3
[](#cb505-6)
[](#cb505-7)$ bash loop.sh items_1.txt items_2.txt
[](#cb505-8)number of lines in 'items_1.txt' is: 3
[](#cb505-9)number of lines in 'items_2.txt' is: 5
```

**21)** Write a shell script named `read_file.sh` that reads a file line by line to be passed as argument to the `paste -sd,` command. Can you also write a solution using the `xargs` command instead of a script?

```
[](#cb506-1)$ printf 'apple\nbanana\ncherry\n' > items_1.txt
[](#cb506-2)$ printf 'dragon\nowl\nunicorn\ntroll\ncentaur\n' > items_2.txt
[](#cb506-3)$ printf 'items_1.txt\nitems_2.txt\n' > list.txt
[](#cb506-4)
[](#cb506-5)$ bash read_file.sh list.txt
[](#cb506-6)apple,banana,cherry
[](#cb506-7)dragon,owl,unicorn,troll,centaur
[](#cb506-8)
[](#cb506-9)$ xargs # ???
[](#cb506-10)apple,banana,cherry
[](#cb506-11)dragon,owl,unicorn,troll,centaur
```

**22)** Write a function named `add_path` which prefixes the path of the current working directory to the arguments it receives and displays the results. Examples are shown below.

```
[](#cb507-1)$ add_path() # ???
[](#cb507-2)
[](#cb507-3)$ cd
[](#cb507-4)$ pwd
[](#cb507-5)/home/learnbyexample
[](#cb507-6)$ add_path ip.txt report.log
[](#cb507-7)/home/learnbyexample/ip.txt /home/learnbyexample/report.log
[](#cb507-8)
[](#cb507-9)$ cd cli-computing
[](#cb507-10)$ pwd
[](#cb507-11)/home/learnbyexample/cli-computing
[](#cb507-12)$ add_path f1
[](#cb507-13)/home/learnbyexample/cli-computing/f1
```

**23)** What do the options `bash -x` and `bash -v` do?

**24)** What is `shellcheck` and when would you use it?

# Shell Customization

This chapter will discuss some of the `bash` features that you can use to customize the command line environment.

## Environment Variables

From [wikipedia: Environment variable](https://en.wikipedia.org/wiki/Environment_variable):

> An environment variable is a dynamic-named value that can affect the way running processes will behave on a computer. They are part of the environment in which a process runs. For example, a running process can query the value of the TEMP environment variable to discover a suitable location to store temporary files, or the HOME or USERPROFILE variable to find the directory structure owned by the user running the process.

See [bash manual: Shell Variables](https://www.gnu.org/software/bash/manual/bash.html#Shell-Variables) for complete list of `bash` variables. Some of them are presented below and some (`HISTCONTROL` for example) will be discussed later in this chapter.

*   `HOME` The current user's home directory; the default for the `cd` builtin command. The value of this variable is also used by tilde expansion
*   `PS1` The primary prompt string. The default value is `\s-\v\$`
*   `PS2` The secondary prompt string. The default value is `>`
*   `PATH` A colon-separated list of directories in which the shell looks for commands. A zero-length (null) directory name in the value of `PATH` indicates the current directory. A null directory name may appear as two adjacent colons, or as an initial or trailing colon
*   `PWD` The current working directory as set by the `cd` builtin
*   `OLDPWD` The previous working directory as set by the `cd` builtin
*   `SHELL` This environment variable expands to the full pathname to the shell

You can use the `printenv` command to display the name and value of all the environment variables. Providing arguments will display the values only for those variables.

```
[](#cb508-1)$ printenv SHELL PWD HOME
[](#cb508-2)/bin/bash
[](#cb508-3)/home/learnbyexample/cli-computing
[](#cb508-4)/home/learnbyexample
```

> ![info](media/file2.svg) ![warning](media/file7.svg) It is recommended to use lowercase for user defined variable names to avoid potential conflict with environment variables. You might have noticed that I used only lowercase names in the [Shell Scripting](#ch014.xhtml_shell-scripting) chapter.

> ![info](media/file0.svg) See also [unix.stackexchange: How to correctly add a path to PATH?](https://unix.stackexchange.com/q/26047/109046).

## Aliases and Functions

To create an alias, use the appropriately named `alias` command. Without any arguments, it will list all the currently defined aliases. If you want to know what an existing alias does, provide one or more names as arguments. To actually create an alias, give a name, followed by `=` and then the command to be aliased. There should be no spaces around the `=` operator. Use `type name` to check if that name is already taken by some command. Here are some examples:

```
[](#cb509-1)# mapping 'p' to the 'pwd' command
[](#cb509-2)$ type p
[](#cb509-3)bash: type: p: not found
[](#cb509-4)$ alias p='pwd'
[](#cb509-5)$ p
[](#cb509-6)/home/learnbyexample/cli-computing
[](#cb509-7)
[](#cb509-8)# adding '--color=auto' to 'ls' invocation
[](#cb509-9)$ type -a ls
[](#cb509-10)ls is /bin/ls
[](#cb509-11)$ alias ls='ls --color=auto'
[](#cb509-12)$ type -a ls
[](#cb509-13)ls is aliased to 'ls --color=auto'
[](#cb509-14)ls is /bin/ls
```

Here's how you can check what the above aliases do:

```
[](#cb510-1)$ alias p ls
[](#cb510-2)alias p='pwd'
[](#cb510-3)alias ls='ls --color=auto'
```

> ![info](media/file0.svg) As seen above, aliases have higher precedence compared to commands in the PATH. You can use a `\` prefix (for example `\ls`) if you want to avoid an alias and use the original command. You can also use `command ls` instead of the escape character.

If you need to pass arguments to your custom commands, use a function (or write a shell script). Here's an example function:

```
[](#cb511-1)# prefix current path to the given arguments
[](#cb511-2)$ ap() { for f in "$@"; do echo "$PWD/$f"; done; }
[](#cb511-3)
[](#cb511-4)$ p
[](#cb511-5)/home/learnbyexample
[](#cb511-6)$ ap ip.txt mountain.jpg
[](#cb511-7)/home/learnbyexample/ip.txt
[](#cb511-8)/home/learnbyexample/mountain.jpg
```

> ![info](media/file0.svg) The aliases and functions created above will be valid only for that particular shell session. To load these shortcuts automatically, you need to add them to special files. See the next section for details.

You can use the `unalias` command to remove an alias. For functions, use the `unset -f` command.

```
[](#cb512-1)$ unalias p
[](#cb512-2)
[](#cb512-3)$ unset -f ap
[](#cb512-4)
[](#cb512-5)$ type p ap
[](#cb512-6)bash: type: p: not found
[](#cb512-7)bash: type: ap: not found
```

## Config files

You can add customizations to special configuration files so that those settings are automatically loaded when you start an interactive shell session.

### .bashrc

From [bash manual: Startup Files](https://www.gnu.org/software/bash/manual/bash.html#Bash-Startup-Files):

> When an interactive shell that is not a login shell is started, Bash reads and executes commands from `~/.bashrc`, if that file exists.

You'll likely have a `~/.bashrc` file provided by the Linux distro you've installed, with useful settings like enabling `bash` programmable completion features, aliases and so on. I leave the distro provided settings alone, unless they are related to aliases and shell options that I want to customize.

Some of the `shopt` customizations I use are shown below. `shopt` was discussed briefly in the [Shell Features](#ch005.xhtml_shell-features) chapter. See [bash manual: Shopt Builtin](https://www.gnu.org/software/bash/manual/bash.html#The-Shopt-Builtin) for more details.

```
[](#cb513-1)# append to history file instead of overwriting
[](#cb513-2)shopt -s histappend
[](#cb513-3)
[](#cb513-4)# extended wildcard functionality
[](#cb513-5)shopt -s extglob
[](#cb513-6)
[](#cb513-7)# helps to recursively match files within a specified path
[](#cb513-8)shopt -s globstar
```

I prefer a simple prompt `PS1='$ '` instead of fancy colors. See [bash manual: Controlling the Prompt](https://www.gnu.org/software/bash/manual/bash.html#Controlling-the-Prompt) for customization options. You can use [bashrcgenerator](https://bashrcgenerator.com/) to easily generate fancy prompts. See also [starship](https://starship.rs/) which is a minimal, blazing-fast, and infinitely customizable prompt for any shell.

Some history customizations are shown below. See [bash manual: History Facilities](https://www.gnu.org/software/bash/manual/bash.html#Bash-History-Facilities) for more details. See also [unix.stackexchange: common history across sessions](https://unix.stackexchange.com/q/18212/109046).

```
[](#cb514-1)# ignorespace prevents lines starting with space from being saved in history
[](#cb514-2)# erasedups deletes previous history entries matching the current one
[](#cb514-3)HISTCONTROL=ignorespace:erasedups
[](#cb514-4)
[](#cb514-5)# maximum number of history lines in the current shell session
[](#cb514-6)# older entries will be overwritten if the size is exceeded
[](#cb514-7)# use negative number for unlimited size
[](#cb514-8)HISTSIZE=2000
[](#cb514-9)
[](#cb514-10)# maximum number of lines in the history file
[](#cb514-11)HISTFILESIZE=2000
```

For aliases and functions, I use a separate file named `~/.bash_aliases` to reduce clutter in the `.bashrc` file. This is not a file that is loaded automatically, so you need to add `source ~/.bash_aliases` command in the `.bashrc` file.

Some of my favorite aliases and functions are shown below. See my [.bash_aliases file](https://github.com/learnbyexample/scripting_course/blob/master/.bash_aliases) for more.

```
[](#cb515-1)alias c='clear'
[](#cb515-2)alias p='pwd'
[](#cb515-3)alias e='exit'
[](#cb515-4)
[](#cb515-5)alias c1='cd ../'
[](#cb515-6)alias c2='cd ../../'
[](#cb515-7)alias c3='cd ../../../'
[](#cb515-8)
[](#cb515-9)alias ls='ls --color=auto'
[](#cb515-10)alias l='ls -ltrhG'
[](#cb515-11)alias la='l -A'
[](#cb515-12)
[](#cb515-13)alias grep='grep --color=auto'
[](#cb515-14)
[](#cb515-15)# save last command in history to a reference file
[](#cb515-16)alias sl='fc -ln -1 | sed "s/^\s*//" >> ~/.saved_cmds.txt'
[](#cb515-17)alias slg='< ~/.saved_cmds.txt grep'
[](#cb515-18)
[](#cb515-19)# case insensitive file search
[](#cb515-20)# fs foo is same as find -iname '*foo*'
[](#cb515-21)fs() { find -iname '*'"$1"'*' ; }
```

> ![info](media/file2.svg) You can use `source` with `.bashrc` or `.bash_aliases` files as arguments to apply changes from such files to the current shell session.

### .inputrc

You can add custom key bindings to the `~/.inputrc` file. See [bash manual: Readline Init File](https://www.gnu.org/software/bash/manual/bash.html#Readline-Init-File) for more details.

A few examples from my `~/.inputrc` file are shown below:

```
[](#cb516-1)$ cat ~/.inputrc
[](#cb516-2)# use up/down arrow to match history based on starting text of the command
[](#cb516-3)"\e[A": history-search-backward
[](#cb516-4)"\e[B": history-search-forward
[](#cb516-5)
[](#cb516-6)# ignore case for filename matching and completion
[](#cb516-7)set completion-ignore-case on
[](#cb516-8)
[](#cb516-9)# single Tab press will complete if there's only one match
[](#cb516-10)# multiple completions will be displayed otherwise
[](#cb516-11)set show-all-if-ambiguous on
```

> ![info](media/file2.svg) You can use `bind -f ~/.inputrc` or press `Ctrl+x Ctrl+r` to apply changes from the `.inputrc` file to the current shell session.

### Further Reading

*   [Sensible bash customizations](https://mrzool.cc/writing/sensible-bash/)
*   [Shell config subfiles](https://blog.sanctum.geek.nz/shell-config-subfiles/)
*   [unix.stackexchange: when to use alias, functions and scripts](https://unix.stackexchange.com/q/30925/109046)
*   [unix.stackexchange: what does rc in bashrc stand for](https://unix.stackexchange.com/q/3467/109046)

## Readline shortcuts

Quoting from [bash manual: Readline Interaction](https://www.gnu.org/software/bash/manual/bash.html#Readline-Interaction):

> Often during an interactive session you type in a long line of text, only to notice that the first word on the line is misspelled. The Readline library gives you a set of commands for manipulating the text as you type it in, allowing you to just fix your typo, and not forcing you to retype the majority of the line. Using these editing commands, you move the cursor to the place that needs correction, and delete or insert the text of the corrections.

By default, command line editing bindings are styled after [Emacs](https://www.gnu.org/software/emacs/) (a text editor). You can switch to Vi mode (another text editor) if you wish. This section will discuss some of the often used Emacs style key bindings.

### Tab completion

The tab key helps you complete commands, aliases, filenames and so on, depending on the context. If there is only one possible completion, it will be done on single tab press. Otherwise, you can press the tab key twice to get a list of possible matches (if there are any).

Use `set show-all-if-ambiguous on` as seen earlier in the [.inputrc](#ch015.xhtml_inputrc) section to combine the single and double tab presses into a single action.

> ![info](media/file0.svg) See [bash manual: Programmable Completion](https://www.gnu.org/software/bash/manual/bash.html#Programmable-Completion) for more details.

### Searching history

You can use `Ctrl+r` to search command history. After pressing this key sequence, type characters you wish to match from history, then press the `Esc` key to return to the command prompt or press `Enter` to execute the command.

You can press `Ctrl+r` repeatedly to move backwards through matching entries and `Ctrl+s` to move forwards. If `Ctrl+s` is not working as expected, see [unix.stackexchange: disable ctrl-s](https://unix.stackexchange.com/q/332791/109046).

As discussed in the [.inputrc](#ch015.xhtml_inputrc) section, you can use custom key mappings to search based on starting characters of the command.

### Moving the cursor

The documentation uses **Meta** (`M-` prefix) and notes that this key is labeled as `Alt` on many keyboards. The documentation also mentions that you can also use the `Esc` key for such combinations.

*   `Alt+b` move the cursor to the start of the current or previous word
*   `Alt+f` move the cursor to the end of the next word
*   `Ctrl+a` or `Home` move cursor to the beginning of the command line
*   `Ctrl+e` or `End` move cursor to the end of the command line

> ![info](media/file0.svg) One difference between `Alt` and `Esc` combinations is that you can keep pressing `b` or `f` while holding the `Alt` key down. The `Esc` combinations are two different key presses, whereas `Alt` has to be kept pressed down for the shortcut to take effect.

### Deleting characters

*   `Alt+Backspace` (or `Esc+Backspace`) delete backwards up to word boundary
*   `Ctrl+w` delete backwards up to whitespace boundary
*   `Ctrl+u` delete from the character before the cursor till the start of the line
*   `Ctrl+k` delete from the cursor location to the end of the command line

### Clear screen

*   `Ctrl+l` preserve whatever is typed and clear the terminal screen

> ![info](media/file0.svg) Note that `Ctrl+l` doesn't try to remove the scrollback buffer altogether. Use the `clear` command for that purpose.

### Swap words and characters

*   `Alt+t` (or `Esc+t`) swap the previous two words
*   `Ctrl+t` swap the previous two characters
    *   for example, if you typed `sp` instead of `ps`, press `Ctrl+t` when the cursor is to the right of `sp`

### Insert arguments

*   `Alt+.` (or `Esc+.`) insert the last argument from the previous command, multiple presses will traverse through second last command and so on
    *   for example, if `cat temp.txt` was the last command used, pressing `Alt+.` will insert `temp.txt`
    *   you can also use `!$` to represent the last argument from the previous command

### Further Reading

*   [bash manual: Bindable Readline Commands](https://www.gnu.org/software/bash/manual/bash.html#Bindable-Readline-Commands)
*   [wiki.archlinux: Simpler introduction to Readline](https://wiki.archlinux.org/title/readline)
*   [Efficient command line navigation](https://cupfullofcode.com/blog/2013/07/03/efficient-command-line-navigation/index.html)

## Copy and paste

Shortcuts for copy-paste operations in the terminal are shown below. You might be able to customize these shortcuts in the terminal preferences.

*   `Shift+Ctrl+c` copy the highlighted portion to the clipboard
*   `Shift+Ctrl+v` paste clipboard contents
*   `Shift+Insert` paste the last highlighted portion (not necessarily the clipboard contents)

You can also press middle mouse button instead of the `Shift+Insert` shortcut. This is not limited to the terminal, works in many other applications too. You can use the `xinput` command to enable/disable mouse button clicks. First, use `xinput` without any arguments and spot the number corresponding to your mouse. As an example, assuming the device number is `11`, you can use the following commands:

*   `xinput set-button-map 11 1 0 3` to disable middle button click
*   `xinput set-button-map 11 1 2 3` to enable middle button click

## Exercises

**1)** Which command would you use to display the name and value of all or specific environment variables?

**2)** If you add an alias for an already existing command (`ls` for example), how would you invoke the original command instead of the alias?

**3)** Why doesn't the alias shown below work? What would you use instead?

```
[](#cb517-1)# doesn't work as expected
[](#cb517-2)$ alias ext='echo "${1##*.}"'
[](#cb517-3)$ ext ip.txt
[](#cb517-4) ip.txt
[](#cb517-5)
[](#cb517-6)# expected output
[](#cb517-7)$ ext ip.txt
[](#cb517-8)txt
[](#cb517-9)$ ext scores.csv
[](#cb517-10)csv
[](#cb517-11)$ ext file.txt.txt
[](#cb517-12)txt
```

**4)** How would you remove a particular alias/function definition for the current shell session?

```
[](#cb518-1)$ alias hw='echo hello world'
[](#cb518-2)$ hw
[](#cb518-3)hello world
[](#cb518-4)# ???
[](#cb518-5)$ hw
[](#cb518-6)hw: command not found
[](#cb518-7)
[](#cb518-8)$ hw() { echo hello there ; }
[](#cb518-9)$ hw
[](#cb518-10)hello there
[](#cb518-11)# ???
[](#cb518-12)$ hw
[](#cb518-13)hw: command not found
```

**5)** Write an alias and a function to display the contents of `PATH` environment variable on separate lines by changing `:` to the newline character. Sample output is shown below.

```
[](#cb519-1)$ echo "$PATH"
[](#cb519-2)/usr/local/bin:/usr/bin:/bin:/usr/games
[](#cb519-3)
[](#cb519-4)# alias
[](#cb519-5)$ a_p
[](#cb519-6)/usr/local/bin
[](#cb519-7)/usr/bin
[](#cb519-8)/bin
[](#cb519-9)/usr/games
[](#cb519-10)
[](#cb519-11)# function
[](#cb519-12)$ f_p
[](#cb519-13)/usr/local/bin
[](#cb519-14)/usr/bin
[](#cb519-15)/bin
[](#cb519-16)/usr/games
```

**6)** Will a login shell read and execute `~/.bashrc` automatically?

**7)** What should be the value assigned to `HISTSIZE` if you wish to have unlimited history entries?

**8)** What does the binding `set completion-ignore-case on` do?

**9)** Which shortcut helps you interactively search command history?

**10)** What do the shortcuts `Alt+b` and `Alt+f` do?

**11)** Are there differences between the `Ctrl+l` shortcut and the `clear` command?

**12)** Which shortcut will you use to delete characters before the cursor till the start of the line?

**13)** What do the shortcuts `Alt+t` and `Ctrl+t` do?

**14)** Is there any difference between `Shift+Insert` and `Shift+Ctrl+v` shortcuts?