
## Preview of the Next Hour

The next hour takes an in-depth look at the different shells available in Unix, how to configure them, and how to choose which you’d like to use. You will also learn about the contents of the default configuration files for both `csh` and `sh`, the two most common shells in Unix.

## Hour 13. Introduction to Command Shells

### Goals for This Hour

In this hour, you will learn

- What shells are available and how they differ from one another
- How to identify which shell you’re running
- How to choose a new shell
- More about the environment of your shell
- How to explore bash configuration files

Welcome to your 13th hour of learning Unix. Don’t worry, this is a lucky hour: No horror film tropes to worry about. Actually, you should take a moment to pat yourself on the back. You’ve come a long way, and you’re already quite a sophisticated user. In the past few hours, I’ve occasionally touched on the differences between the various command shells, but I haven’t really stopped to explain what shells are available, how they differ from one another, and which is the best for your style of interaction. That’s what this hour is all about.

Shells, you’ll recall, are the command-line interface programs through which you tell the computer what to do. All Unix systems include the C shell (`csh`) and its predecessor, the Bourne shell (`sh`). All modern Unix systems also include some nifty newer shells, notably Korn shell (`ksh`) and a new rewrite of `sh` humorously called the Bourne Again shell (`bash`). It’s the bash shell that I’m going to focus on for all our shell-specific discussion because it’s one of the most popular shells, and it’s so powerful and flexible—it includes all the cool features of both `csh` and `sh` and adds tons of additional stuff—that it’s a great place to start.

Various shells are available in Unix, but two are guaranteed to be included in just about all Unix versions: the Bourne shell (`sh`) and the C shell (`csh`). Primarily, however, you’ll learn about bash and `ksh` in this lesson.

### The (Command) Shell Game

You can’t get very far with Unix on most systems without having a command-line interpreter. This lesson quickly gets you up and running with the bash command shell.

### Task 13.1: What Shells Are Available?

If I asked an expert how many command interpreters are available for the PC, the immediate answer would be "one, of course." After a few minutes of reflection, however, the answer might be expanded to include the classic DOS command line (which is still in Windows!) and various third-party interfaces as well as the standard Windows user interface. This expanded answer reflects the reality that whenever different people use a computer, different styles of interacting with the machine and different products to meet these needs evolve. Similarly, the Macintosh has several command interpreters. If you decide that you don’t like the standard GUI, perhaps you will find that the command-line Terminal app or even the X11 environment works better.

From the very beginning, Unix has been a programmer’s operating system, designed to allow programmers to extend the system easily and gracefully. It should come as no surprise that quite a few command shells are available. Not only that, but technically any program can serve as a command shell, so you could even start right in emacs if you wanted and then use escapes to Unix for actual commands. (Don’t laugh! I know people who’ve done this.)

The original shell was written by Ken Thompson, back in the early Unix laboratory days, as part of his design of the Unix file system. Somewhere along the way, Steven Bourne, also at AT&T, got ahold of the shell and started expanding it. By the time Unix began to be widely distributed, `sh` was known as the Bourne shell. Characterized by speed and simplicity, it was the default shell for writing shell scripts, but now it is rarely used as a command shell for users.

The next shell was designed by the productive Bill Joy, author of vi. Entranced by the design and features of the C programming language, Joy decided to create a command shell that shared much of the C language structure and that would make it easier to write sophisticated shell scripts: the C shell, or `csh`. He also expanded the shell concept to add command aliases, command history, and job control. Command aliases enable users to rename and reconfigure commands easily. Command history ensures that users never have to enter commands a second time. Job control enables users to run multiple programs at once. Before bash appeared on the scene, the C shell was the shell I used from the day I first logged in to a BSD Unix system in 1980.

**Note:** A command alias is a shortcut for a command that allows you to enter a shorter string for the entire command. The command history is a mechanism by which the shell remembers commands you have typed and allows you to repeat the command without retyping the whole command. Job control is a mechanism that allows you to start, stop, and suspend commands.

In the 1990s, another AT&T Labs (now Lucent) software wizard, David Korn, built an eponymous shell. The Korn shell, also known as `ksh`, is designed to be a superset of the Bourne shell, sharing its configuration files (`.profile`) and command syntax but including many of the more powerful features of the C shell, too, including command
