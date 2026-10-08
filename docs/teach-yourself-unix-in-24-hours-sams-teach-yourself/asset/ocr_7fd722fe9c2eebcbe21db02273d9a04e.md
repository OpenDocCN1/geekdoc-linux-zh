# What Is This UNIX Stuff?

![](bbox=[0.129, 0.14, 0.199, 0.166])

1. The mkdir man page is succinct and exemplary:

% man mkdir

MKDIR(1) DYNIX Programmer's Manual MKDIR(1)

NAME

mkdir - make a directory

SYNOPSIS

mkdir dirname ...

DESCRIPTION mkdir creates specified directories in mode 777. Standard entries, for the directory itself, and '..' for its parent, are made automatically.

mkdir requires write permission in the parent directory.

SEE ALSO

mkdir(1)

Revision 1.4.2.2 88/08/13

%

> Note in the example, that in the first line, the command itself is in boldface type, but everything else is not bold. Throughout this book, whenever an example contains both user input and UNIX output, the user input will be bold so that you can spot easily what is supposed to enter.

![](bbox=[0.129, 0.532, 0.199, 0.584])

JUST A MINUTE

The first line of the output tells me that's found the mkdir command in Section 1 (user commands) of the man pages, with the middle phrase, DYNIX Programmer's Manual, indicating that I'm running on a version of UNIX called DYNIX. The NAME section details the name of the command and a one-line summary of what it does. SYNOPSIS explains how to use the command, including all possible flags and options.

DESCRIPTION is where all the meaningful information is, and it can run for dozens of pages, explaining how complex commands like ls or vi work. SEE ALSO suggests other commands that are related in some way. The Revision line at the bottom is different on each version of man, and it indicates the last time, presumably, that this document was revised.