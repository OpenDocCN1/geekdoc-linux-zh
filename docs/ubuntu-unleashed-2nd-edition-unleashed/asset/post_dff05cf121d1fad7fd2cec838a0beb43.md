
## Command-Line Error

If you get the message bash: trivial.pl: command not found or bash: ./trivial.pl: Permission denied, you have either typed the command line incorrectly or forgotten to make trivial.pl executable (with the chmod command):

```sh
$ chmod +x trivial.pl
```

You can force the command to execute in the current directory as follows:

```sh
$ ./trivial.pl
```

Or you can use Perl to run the program like this:

```sh
$ perl trivial.pl
```

The sample program in the listing is a two-line Perl program. Typing in the program and running it (using Perl or making the program executable) shows how to create your first Perl program, a process duplicated by Linux users around the world every day!

### NOTE

#! is often pronounced she-bang, which is short for sharp (the musicians name for the # character), and bang, which is another name for the exclamation point. This notation is also used in shell scripts. See Chapter 15, “Automating Tasks,” for more information about writing shell scripts.

The #! line is technically not part of the Perl code at all. The # character indicates that the rest of the screen line is a comment. The comment is a message to the shell, telling it where it should go to find the executable to run this program. The interpreter ignores the comment line.

Exceptions to this practice include when the # character is in a quoted string and when it is being used as the delimiter in a regular expression. Comments are useful to document your scripts, like this:

```perl
#!/usr/bin/perl
# a simple example to print a greeting
print "hello there\n";
```

A block of code, such as what might appear inside a loop or a branch of a conditional statement, is indicated with curly braces ({}). For example, here is an infinite loop:

```perl
#!/usr/bin/perl
# a block of code to print a greeting forever
while (1) {
    print "hello there\n";
};
```

Perl statements are terminated with a semicolon. A Perl statement can extend over several actual screen lines because Perl is not concerned about whitespace.

The second line of the simple program prints the text enclosed in quotation marks. \n is the escape sequence for a newline character.

### TIP

Using the perldoc and man commands is an easy way to get more information about the version of Perl installed on your system. To learn how to use the perldoc command, enter the following:

```
$ perldoc perldoc
```

To get introductory information on Perl, you can use either of these commands:

```
$ perldoc perl
$ man perl
```

For an overview or table of contents of Perl's documentation, use the perldoc command like this:

```
$ perldoc perltoc
```

The documentation is extensive and well organized. Perl includes a number of standard Linux manual pages as brief guides to its capabilities, but perhaps the best way to learn more about Perl is to read its perlfunc document, which lists all the available Perl functions and their usage. You can view this document by using the perldoc script and typing perldoc perlfunc at the command line. You can also find this document online at http://www.cpan.org/doc/manual/html/pod/perlfunc.html.

## Perl Variables and Data Structures

Perl is a weakly typed language, meaning that it does not require that you declare a data type, such as a type of value (data) to be stored in a particular variable. C, for example, makes you declare that a particular variable is an integer, a character, a structure, or whatever the case may be. Perl variables are whatever type they need to be, and can change type when you need them to.

### Perl Variable Types

Perl has three variable types: scalars, arrays, and hashes. A different character is used to signify each variable type.

Scalar variables are indicated with the $ character, as in $penguin. Scalars can be numbers or strings, and they can change type from one to the other as needed. If you treat a number like a string, it becomes a string. If you treat a string like a number, it is translated into a number if it makes sense to do so; otherwise, it usually evaluates to 0. For example, the string "76trombones" evaluates as the number 76 if used in a numeric calculation, but the string "polar bear" evaluates to 0.
