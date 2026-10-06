# Introduction

It's no secret that the family of Unix and Unix-like operating systems have emerged over the last few decades as the most pervasive, most widely used group of operating systems in computing today. For programmers who have been using Unix for many years, this came as no surprise: The Unix system provides an elegant and efficient environment for program development. That's exactly what Dennis Ritchie and Ken Thompson sought to create when they developed Unix at Bell Laboratories back in the late 1960s.

> Note
Throughout this book we'll use the term Unix to refer generically to the broad family of Unix-based operating systems, true Unix operating systems as Solaris as well as Unix-like operating systems such as Linux and Mac OS X.

One of the strongest features of the Unix system is its wide collection of programs. More than 200 basic commands are distributed with the standard operating system and Linux adds to it, often shipping with 700-1000 standard commands! These commands (also known as tools) do everything from counting the number of lines in a file, to sending electronic mail, to displaying a calendar for any desired year.

But the real strength of the Unix system comes not from its large collection of commands but from the elegance and ease with which these commands can be combined to perform far more sophisticated tasks.

The standard user interface to Unix is the command line, which actually turns out to be a shell, a program that acts as a buffer between the user and the lowest levels of the system (the kernel). The shell is simply a program that reads the commands you type and converts them into a form easily understood by the system. It also includes programming constructs that let you make decisions, loop, and store values in variables.

The standard shell distributed with Unix derives from AT&T's distribution, which evolved from a version originally written by Stephen Bourne at Bell Labs. Since then, the IEEE has created standards based on the Bourne shell and all other recent shells. The current version of this standard, as of this writing, is the Shell and Utilities volume of IEEE Std 1003.1-2001, also known as the POSIX standard. This shell is what we use for the basis for the rest of this book.

The examples in this book were tested on a Mac running OS X 10.11