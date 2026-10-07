# Lab 3.1: Command Sequences

LAB 3.1

You will see when you write your own functions and scripts that you use numbers for exit codes: Zero means "true" and any other number means "false".

The standard value for false is 1. Don't use another value unless you have a particular reason for doing so.

Next, you need to think about the logical operators and and or because the && operator works like and and the || operator works like or for exit codes. If you combine two logic values using and, the result is true if the first value and the second value are both true, and false otherwise. If you combine two logic values using or, the result is true if the first value or the second value is true (both).

The secret to understanding && is that if you use it to connect two commands, the shell will run just enough commands to figure out what the result of the && operator will be, and nothing more. Furthermore, the shell guarantees that it will execute the commands in left-to-right sequence until it knows the result of the && operator.

+   a) Run the following two command lines and explain the output:
true && print hello
false && print hello

+   b) What happens if you have multiple && operators in one command line? For example, what is the output of this command:
true && true && false && print hello