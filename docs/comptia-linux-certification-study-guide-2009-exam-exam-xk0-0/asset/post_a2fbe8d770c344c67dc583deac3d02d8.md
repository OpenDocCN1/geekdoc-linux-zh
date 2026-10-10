
- **Process ID (PID)** A unique number assigned when a new process (program) is started, and used to reference that process.
- **Parent process ID (PPID)** The PID of the process that spawned (started) a new process.

## INTRODUCTION

Some people claim Linux is inferior due to its extensive use of the command line interface (CLI). While newer versions of Linux have made it increasingly easier to avoid using it, the power and versatility of the command line is one of the key strengths in the entire system, if you are willing to invest the time to really learn it. It reminds me of “The Force” – surrounding all things and binding them. The command line is your light saber, “an elegant weapon from a more civilized age,”¹ but formidable in the hands of a Linux Jedi. Step forward and begin your training!

Hyperbole? Maybe, but the command line has a number of strengths. It is easily scripted for repetitive tasks, which can then be scheduled and implemented across multiple machines – a key advantage for administrators of multiple systems. It is consistent across different distributions and versions, different desktops, and window managers. It is straightforward to manage through remote access (ssh), and ubiquitous – the exam assumes you will be managing a desktop or server, but Linux is showing up in countless embedded appliances, and their full power is seldom available from the graphic interface basic users are allowed to see. A commanding knowledge of the CLI is the key to passing the Linux+ exam and will distinguish you as a valuable asset in any company. Be warned, though: like any powerful tool, it can also wreak untold havoc if you don’t know what you are doing.

So, what is BASH, exactly? It’s a command interpreter, a way for a user to submit instructions to the computer. One of the original UNIX shells was the “Bourne” shell, invoked with an “sh” (short for sh(1)). An updated version was developed and (a bit whimsically) called the “Bourne again shell” [BASH].

> **Note**
> Although BASH has evolved into the current standard in most Linux, BSD, and OSX (since v10.3), there are several other shells to choose from. Other popular ones are zsh; ksh (“korn” shell); and “csh” (see shell), which uses syntax and scripting common to the “C” programming language, so it’s popular with C/C++ programmers.

If you'd like to try some of the others, use your favorite package manager to install one, and invoke it from BASH by typing zsh, ksh, or csh. Bash is cleverly named, “bash.” The shell setting can be made permanent per user by editing the users' /etc/passwd file. On a typical Linux installation, “sh” is a link to /usr/bin/bash.

## BASH COMMANDS

How do you get to a command line? If you haven't installed a graphical user interface (GUI), the system will boot you directly into a command shell. Otherwise, you'll have to find your systems terminal program. In the version of openSUSE used in this book, it's called Terminal and located at the bottom of the list of programs that pops up when you click on the green lizard start button on the bottom left corner of the screen, as shown in Figure 6.1.

The terminal program is used so often that you may find it convenient to drag the Terminal icon to the taskbar for more direct access.

![](img/95b3ebd6248b36778ccf73988aaab2f2_165_0.png)

FIGURE 6.1 The terminal program konsole in KDE.

> **Note**
> You can also type `Alt + F2` to pop up the “run an application” window, and type in `konsole` in KDE or `gnome-terminal` if you use the gnome desktop.

It is frequently convenient to run several command shell windows simultaneously; you can read a “man” page describing the use of a command while trying the command, or monitor a log file while performing system management. Konsole (KDE's terminal program) supports multiple tabs with a separate instance of a command line in each, which can be convenient.

> **Note**
> To make it easier to keep track of multiple windows, `konsole` (and `gnome-terminal`) lets you rename each terminal instance – per tab or discrete window. Try it! In `konsole` type `Ctrl + Shift + N` (or click **file** | **New Tab**) to open a new tab (the tabs themselves appear on the bottom of the `konsole` window), and `Ctrl + Alt + s` (or click **edit** | **rename**) to rename it. Note that the icon for `konsole` on the taskbar at the bottom of the screen is also renamed, making it easier to go straight to the terminal window you want when you have several minimized or covered.

While digging through the various terminal program options, feel free to play with the settings for background, transparency, font, foreground/background color, and others. It isn't on the test (but hey, you're going to be staring at this for countless hours), therefore, you might as well make it something that's easy to read and pleasing to look at.

> **Exam Warning**
> Note that if you don't use a "monospaced" font (where every character is the same width on the screen) columns won't align correctly, and some commands use a variety of colors, making the output invisible if your background matches one of them. A pretty blue background, for example, will render all directories invisible in the default output of the `ls` command and can induce momentary heart failure.

### Navigating Directories

OK, you've got a terminal window, now what? A good starting place is basic directory navigation. Type `pwd` (*print working directory*) to see what directory you are in. `konsole` will start you in your home directory: `/home/your_user_name/`. You can see the contents of your current directory

![](img/95b3ebd6248b36778ccf73988aaab2f2_167_0.png)

**FIGURE 6.2**

*The KDE “konsole” windows; power at your fingertips.*

by entering `ls` (*to list things*). Enter `ls` with a path to see the contents of other directories (try `ls /`, `ls /etc`), and use `cd` (*change directory*) to change your current working directory (`cd`, `cd /etc` – try using `pwd` and `ls` in each directory as you move about).

If you find yourself frequently jumping back and forth between directories, you may find it handy to use `pushd` and `popd` as an easy way to save a directory (or several). These utilities work like a stack of index cards. Think of `pushd` as writing a directory on an index card and placing it on a stack, and `popd` as picking up the card on the top of the stack and changing to that directory. Try `pushd /var/log` and notice that the current directory is now `/var/log`.

When you first open a terminal window, it will give you a command prompt, which is typically your machine name and username, or maybe your current directory ending with a `$` for a normal user or a `#` if you are running as “root” (the administrator account) – see Figure 6.2.

## Using File Commands

The Linux file structure, like most computer systems, is a series of files, folders, and subfolders. Unlike Microsoft-based systems, there is no concept of “drive letter” – no `C:`. The very “top” of the files is the *root* directory – think

156 CHAPTER 6: Using BASH

![](img/95b3ebd6248b36778ccf73988aaab2f2_168_0.png)

of the files and folders as the roots of a tree. The root folder (called "/") is at the top, with folders and subfolders branching downward from there (that is, "/home/chappel/Documents" for the Documents folder in user chappel's home directory).

So, if you open a command window while logged in as user chappel, you'll see a prompt and be in the present working directory, as shown in Figure 6.3.

Clearly, manipulating the files and folders on the system is an important capability. Although GUI file managers make it easy to do many basic filing tasks, they can't match the power and flexibility at the fingertips of a command-line master.

Starting with the basics, mkdir creates a directory and rmdir deletes it (provided there are no files in the directory). The command touch will create an empty file; cp will copy the file, mv will move (or rename) it, and rm will delete it.

> **Note**  
> If *touch* seems like an odd name for a command that creates files, it's because it was originally intended to change the timestamp on an existing file - so you could see the last time it had been "touched," literally. This is very handy for keeping track
