# Chapter 4: Simple Variables 201

If you have alternative answers to the questions in this exercise, you are encouraged to post your answers and discuss them at the companion site for this book, located at:

http://www.phptr.com/phpptrinteractive/

# 4.3.1 ANSWERS

The first item repeats what you may already have done in the previous lab:

+   a) Write a command that assigns the default value, a dollar sign followed by a space, to PS1.
Answer:Your interaction should look like the following:
$ PS1="$ 
$

If your prompt wasn't the default string before, the space after the dollar sign would have been dropped from the value of PS1 because the shell discards all spaces and tab characters that are not inside equal quotes before it executes a command.

> One of the first things the shell does when it processes a command line is to split it into syntactic units that it calls tokens (sometimes called words) using spaces, tabs, and other special characters to find the token boundaries. The last thing the shell does before it executes a command is to remove any quotation marks that are not escaped with backslashes. The command being executed does not have any way to tell whether or not the user put quotes around the command line parameters.

This "token splitting" part of command line processing also explains why there can't be any spaces around the equal sign in an assignment command: The entire assignment command must be a single token when the command line is split.

![](bbox=[0.025, 0.575, 0.115, 0.665])