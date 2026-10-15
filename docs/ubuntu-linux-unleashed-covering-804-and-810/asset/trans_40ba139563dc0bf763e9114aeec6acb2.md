
"What are you trying to tell me?" asked the programmer.

Master Foo pointed at the programmer's head. Then he pointed at a rock.

"Why can't you make yourself clear?" demanded the programmer.

Master Foo frowned thoughtfully, tapped the programmer twice on the nose, and dropped him in a nearby trash can.

As the programmer was attempting to extricate himself from the garbage, the dog wandered over and piddled on him.

At that moment, the programmer achieved enlightenment.

Whimsical as the story is, it does illustrate that there are some things that the GUI just does not do well. Enter the command line: It is a powerful and flexible operating environment on Linux, and—if you practice—can actually be quite fun, too!

In this chapter, you will learn how to master the command line so that you are able to perform common tasks through it, and also link commands together to create new command groups. We will also be looking at the two most popular Linux text editors: Vim and Emacs. The command line is also known as the shell, the console, the command prompt, and the CLI (command-line interpreter). For the purposes of this chapter these are interchangeable, although there are fine-grained differences between them!

## Why Use the Shell?

Moving from the GUI to the command line is a conscious choice for most people, although it is increasingly rare that it is an either/or choice. While in X, you can press Ctrl+Alt+F1 at any time to switch to a terminal, but most people tend to run an X terminal application that allows them to have the point-and-click applications and the command-line applications side by side.

Reasons for running the shell include:

- You want to chain two or more commands together.
- You want to use a command or parameter available only on the shell.
- You are working on a text-only system.
- You have used it for a long time and feel comfortable there.

Chaining two or more commands together is what gives the shell its real power. Hundreds of commands are available and, by combining them in different ways, you get hundreds of new commands. Some of the shell commands are available through the GUI, but these commands usually have only a small subset of their parameters available, which limits what you are able to do with them.

Working from a text-only system encapsulates both working locally with a broken GUI and also connecting to a remote, text-only system. If your Linux server is experiencing problems, the last thing you want to do is load it down with a GUI connection—working in text mode is faster and more efficient.

The last use is the most common: People use the shell just because it is familiar to them, with many people even using the shell to start GUI applications just because it saves them taking their hands off the keyboard for a moment! This is not a bad thing; it provides fluency and ease with the system and is a perfectly valid way of working.

## Basic Commands

It is impossible to know how many commands the average shell citizen uses, but if we had to guess, we would place it at about 25:

- cat—Prints the contents of a file
- cd—Changes directories
- chmod—Changes file access permissions
- cp—Copies files
- du—Prints disk usage
- emacs—Text editor
- find—Finds files by searching
- gcc—The C/C++/Fortran compiler
- grep—Searches for a string in input
- less—Filter for paging through output
- ln—Creates links between files
- locate—Finds files from an index
- ls—Lists files in the current directory
- make—Compiles and installs programs
- man—The manual page reader
- mkdir—Makes directories
- mv—Moves files
- ps—Lists processes
- rm—Deletes files and directories
- ssh—Connects to other machines
- tail—Prints the last lines of a file
- top—Prints resource usage
- vim—A text editor
- which—Prints the location of a command
