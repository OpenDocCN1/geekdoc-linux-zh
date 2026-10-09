# Linux Command Line

CHAPTER 5

# CHAPTER OBJECTIVES

+   * Set environment variables
* Describe and use the features of the multi-user environment
* Use common shell commands and expressions
* Create, edit, and save files using vi

# USING THE COMMAND-LINE SHELL

Most, if not all, commands can be accomplished through the GUI tools. However, knowledge of the command-line interface (CLI) can make Linux administration much faster for most tasks. Some commands can be accomplished only though the command line. Using GUI tools requires mouse movements and finding commands through a maze of menus and toolbars, a cumbersome procedure for most administrators.

An experienced user can also write shell scripts. A shell script is a collection of commands stored in a file. The file is given execute permission and is used to do a wide variety of tasks. Scripts are discussed in the next chapter.

The first operating systems used a command line interpreter to interact with users. A command interpreter accepts input from a user via keyboard and translates every word, or interprets the words, and then does whatever action is called for. The first command interpreters were pretty basic and didn’t offer very many features. To provide a better way of interacting with the operating system, the shell (Figure 5–1) was developed. The first shell program was the Bourne shell (sh), developed by S. R. Bourne. Since then, other shells have been developed, including C shell (csh), the Korn shell (ksh), and the bash shell (Bourne Again Shell).

# Command Line Basics

The bash shell (see http://www.gnu.org/software/bash/bash.html) is the product of the Free Software Foundation and is used by most Linux operating systems. Several shells are typically available in Linux, but the bash shell is the default shell for users.

If you booted the system into runlevel 3, you are at a command line prompt. If you are using the X window system (GUI), you need to open a terminal window. A terminal window is a terminal emulator program that opens in a window and then runs a shell program. There are several different terminal programs: gnome-terminal, xterm, and others. Typically, within the GUI, you can right-click the screen and select terminal from the displayed pop-up menu.

A virtual terminal, discussed in Chapter 2, can also be used. Pressing Ctrl+Alt+F1 displays the first virtual terminal, Ctrl+Alt+F2 displays the second, and so on. Linux usually has six virtual terminals, and the seventh displays the GUI. The virtual terminals work with the CLI, but the GUI is still active and can be displayed by pressing Ctrl+Alt+F7. When the terminal displays the **login:** prompt, enter a valid ID and then a password to display the bash shell. The CLI prompt will be displayed. Typically, the prompt will be $,