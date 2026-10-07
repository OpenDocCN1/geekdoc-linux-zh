# 110 Lab 2.3: Command Syntax

Common symbols used to end here documents include the word END (using capital letters makes it stand out) or some exclamation marks ( !!! ). It's a good idea to pick one symbol and use it for all the here documents you write. The consistency will help you and the people who read your code to spot your use of here documents easily.

![](bbox=[0.145, 0.115, 0.235, 0.185])

Three plus signs (+++) might seem like a good termination symbol for here documents because it's easy to spot, but that's the code that tells many modems to go into their "command mode"!

![](bbox=[0.135, 0.275, 0.235, 0.325])

Type a cat command with a here document for stdin, and redirect stdout to a file.

+   d) What does the command do?

Answer: It copies the here document to the file. Your interaction should look some-like the following:
$ rm -f out
$ cat << !!! > out
> This is here.
> That is there.
> Never the twain shall meet.
> !!!
$ more out
This is here.
That is there.
Never the twain shall meet.
$

This example shows the syntax for using both << and other redirection for a single command, but it's not the kind of thing you would normally do in interactive mode. Here documents are used almost exclusively inside scripts and functions.

# LAB 2.3