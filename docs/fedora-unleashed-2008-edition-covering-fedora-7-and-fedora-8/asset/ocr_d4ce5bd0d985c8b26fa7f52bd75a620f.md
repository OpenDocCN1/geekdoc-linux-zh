# **Command-Line Error**

If you get the message `bash: trivial.pl: command not found` or `bash: ./trivial.pl: Permission denied`, it means that you either typed the command line incorrectly or forgot to make `trivial.pl` executable (with the `chmod` command):

```
`$ chmod +x trivial.pl`
```

You can force the command to execute in the current directory as follows:

```
`$ ./trivial.pl`
```

Or you can use Perl to run the program like this:

```
`$ perl trivial.pl`
```

The sample program in the listing is a two-line Perl program. Typing in the program and running it (using Perl or making the program executable) shows how to create your first Perl program, a process duplicated by Linux users around the world every day!

# **NOTE**

> `#!` is often pronounced `she-bang`, which is short for `sharp` (the musicians name for the `#` character), and `bang`, which is another name for the exclamation point. This notation is also used in shell scripts. Refer to Chapter 33, "Writing and Executing a Shell Script," for more information about writing shell scripts.

The `#!` line is technically not part of the Perl code at all. The `#` character indicates that the rest of the screen line is a comment. The comment is a message to the shell, telling it where it should go to find the executable to run this program. The interpreter ignores the comment line.

Exceptions to this practice include when the `#` character is in a quoted string and when it is being used as the delimiter in a regular expression. Comments are useful to document your scripts, like this:

```
```
#!/usr/bin/perl
# a simple example to print a greeting
print "hello there\n";
```
```

A block of code, such as what might appear inside a loop or a branch of a conditional statement, is indicated with curly braces (`{}`) . For example, here is an infinite loop:

```
```
#!/usr/bin/perl
# a block of code to print a greeting forever
while (1) {
    print "hello there\n";
}
```
```