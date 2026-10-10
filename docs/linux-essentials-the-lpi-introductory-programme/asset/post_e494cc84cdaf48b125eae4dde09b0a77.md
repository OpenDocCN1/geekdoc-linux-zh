
**3.7** [2] Using the text from the previous exercise, cut the line
```code
Linux is brilliant,
```
and paste it back three times, so that the text now looks like
```code
Roses are red,
Violets are blue,
Linux is brilliant,
Linux is brilliant,
Linux is brilliant,
I know this is true.
```
Then position the cursor on the “i” of “is” in the first of these lines, mark that position, navigate to the “i” of “is” on the third line, and remove the marked region.

### Commands in this Chapter

| Command | Description | Manual | Page |
| :--- | :--- | :--- | :--- |
| logquit | Terminates a shell session | bash(1) | 49 |
| pico | Very simple text editor from the PINE/Alpine package | pico(1) | 52 |

### Summary

- Before using a Linux system, you have to log in giving your user name and password. After using the system, you have to log out again.
- Linux offers various graphical environments, which for the most part work in a similar fashion and fairly intuitively.
- A terminal window allows you to enter textual shell commands within a graphical environment.
- GNU Nano is a simple text editor.

![](img/44bdd771e9c9b1353d2401c2892b2459_56_0.png)

## 4 Who’s Afraid Of The Big Bad Shell?

### Contents

4.1 Why? ... 58
4.1.1 What Is The Shell? ... 58
4.2 Commands ... 59
4.2.1 Why Commands? ... 59
4.2.2 Command Structure ... 60
4.2.3 Command Types ... 61
4.2.4 Even More Rules ... 61

### Goals

- Appreciating the advantages of a command-line user interface
- Working with Bourne-Again Shell (Bash) commands
- Understanding the structure of Linux commands

### Prerequisites

- Basic knowledge of using computers is helpful

### 4.1 Why?

More so than other modern operating systems, Linux (like Unix) is based on the idea of entering textual commands via the keyboard. This may sound antiqued to some, especially if one is used to systems like Windows, who have been trying for 15 years or so to brainwash their audience into thinking that graphical user interfaces are the be-all and end-all. For many people who come to Linux from Windows, the comparative prominence of the command line interface is at first a "culture shock" like that suffered by a 21st-century person if they suddenly got transported to King Arthur's court – no cellular coverage, bad table manners, and dreadful dentists!

However, things aren't as bad as all that. On the one hand, nowadays there are graphical interfaces even for Linux, which are equal to what Windows or Mac-OS X have to offer, or in some respects even surpass these as far as convenience and power are concerned. On the other hand, graphical interfaces and the text-oriented command line are not mutually exclusive, but in fact complementary (according to the philosophy "the right tool for every job").

At the end of the day this only means that you as a budding Linux user will do well to *also* get used to the text-oriented user interface, known as the "shell". Of course nobody wants to prevent you from using a graphical desktop for everything you can do. The shell, however, is a convenient way to perform many extremely powerful operations that are rather difficult to express graphically. To reject the shell is like rejecting all gears except first in your car$^{1}$. Sure, you'll get there eventually even in first gear, but only comparatively slowly and with a horrible amount of noise. So why not learn how to really floor it with Linux? And if you watch closely, we'll be able to show you another trick or two.

### 4.1.1 What Is The Shell?

Users cannot communicate directly with the operating system kernel. This is only possible through programs accessing it via "system calls". However, you must be able to start such programs in some way. This is the task of the shell, a special user program that (usually) reads commands from the keyboard and interprets them (for example) as commands to be executed. Accordingly, the shell serves as an "interface" to the computer that encloses the actual operating system like a shell (as in "shellfish"—hence the name) and hides it from view. Of course the shell is only one program among many that access the operating system.

![](img/44bdd771e9c9b1353d2401c2892b2459_57_0.png)

Even today's graphical "desktops" like KDE can be considered "shells". Instead of reading text commands via the keyboard, they read graphical commands—via the mouse—but as the text commands follow a certain "grammar", the mouse commands do just the same. For example, you select objects by clicking on them and then determine what to do with them: opening, copying, deleting, ...

Even the very first Unix—and-1960s vintage—had a shell. The oldest shell to be found outside museums today was developed in the mid-1970s for "Unix version 7" by Stephen L. Bourne. This so-called "Bourne shell" contains most basic functions and was in very wide-spread use, but is very rarely seen in its original form today.

- Bourne shell
- C shell
- Korn shell
- Bourne-again shell

Other classic Unix shells include the C Shell, created at the University of California in Berkeley and (very vaguely) based on the C programming language, and the largely Bourne-shell compatible, but functionally enhanced, Korn shell (by David Korn, also at AT&T).

Standard on Linux systems is the Bourne-again shell, bash for short. It was developed under the auspices of the Free Software Foundation's GNU project by Brian Fox and Chet Ramey and unifies many functions of the Korn and C shells.

> $^{1}$ This metaphor is for Europeans and other people who can manage a stick shift; our American readers of course all use those wimpy automatic transmissions. It's like they were all running Windows.

Besides the mentioned shells, there are many more. On Unix, a shell is simply an application program like all others, and you need no special privileges to write one—you simply need to adhere to the “rules of the game” that govern how a shell communicates with other programs.

Shells may be invoked interactively to read user commands (normally on a “terminal” of some sort). Most shells can also read commands from files containing pre-cooked command sequences. Such files are called “shell scripts”.

A shell performs the following steps:

1. Read a command from the terminal (or the file)
2. Validate the command
3. Run the command directly or start the corresponding program
4. Output the result to the screen (or elsewhere)
5. Continue at step 1.

In addition to this standard command loop, a shell generally contains further features such as a programming language. This includes complex command structures involving loops, conditions, and variables (usually in shell scripts, less frequently in interactive use). A sophisticated method for recycling recently used commands also makes a user’s life easier.

Shell sessions can generally be terminated using the exit command. This also applies to the shell that you obtained immediately after logging in.

Although, as we mentioned, there are several different shells, we shall concentrate here on bash as the standard shell on most Linux distributions. The LPI exams also refer to bash exclusively.

### Exercises

**4.1** [2] Log off and on again and check the output of the “echo $0” command in the login shell. Start a new shell using the “bash” command and enter “echo $0” again. Compare the output of the two commands. Do you notice anything unusual?

### 4.2 Commands

#### 4.2.1 Why Commands?

A computer’s operation, no matter which operating system it is running, can be loosely described in three steps:

1. The computer waits for user input
2. The user selects a command and enters it via the keyboard or mouse
3. The computer executes the command

In a Linux system, the shell displays a “prompt”, meaning that commands can be entered. This prompt usually consists of a user and host (computer) name, the current directory, and a final character:

```
joe@red: /home > _
```

In this example, user joe works on computer red in the /home directory.
