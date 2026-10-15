
The following is a simple interactive use of the command. The date command is executed to show that the output has six fields. The set argv = 'date' command sets the positional parameters according to the output of the date command. In particular, $argv[1] is set to Sat, $argv[2] to Aug, $argv[3] to 7, $argv[4] to 13:26:42, $argv[5] to PDT, and $argv[6] to 2004. The echo $argv[*] command displays the values of all positional arguments. The third echo command displays the date in a commonly used form.

```
% date
Sun Sep 7 08:25:04 PKT 2014
% set argv = 'date'
% echo $argv[*]
Sun Sep 7 08:25:17 PKT 2014
% echo "$argv[2] $argv[3], $argv[6]"
Sep 7, 2014
%
```

The script in set_demo shows another use of the command. When the script is run with a file argument, it generates a line that contains the file name, the file's inode number, and the file size (in bytes). The set command is used to assign the output of ls -il command as the new values of the positional arguments $argv[1] through $argv[9]. We show the output of the ls -il command in case you do not remember the format of the output of this command.

```
% cat set_demo
#!/bin/csh
set filename = $argv[1]
set argv = 'ls -il $filename'
set inode = $argv[1]
set perms = $argv[2]
set size = $argv[6]
echo "File Name:      $filename"
echo "Inode Number:   $inode"
echo "Permissions:    $perms"
echo "Size (bytes):   $size"
exit 0
% ./set_demo lab3
File Name: lab3
Inode Number: 4313
Permissions: -rw-r--r--
Size (bytes): 221
% ls -il lab3
4313 -rw-r--r-- 1 sarwar sarwar 221 Sep 7 08:30 lab3
%
```

In the following in-chapter exercises, you will use the set and shift commands in order to reinforce the use and processing of command line arguments.

## EXERCISE 14.6

Write a shell script that displays all command line arguments, shifts them to the left by two positions, and redisplays them. Show the script along with a few sample runs.

## EXERCISE 14.7

Update the shell script in Exercise 14.1 so that, after accomplishing this task, it sets the positional arguments to the output of the who | head -1 command and displays the positional arguments again.

## 14.6 COMMENTS AND PROGRAM HEADERS

You should develop the habit of putting comments in your programs to describe the purpose of a particular series of commands. At times, you should even briefly describe the purpose of a variable or assignment statement. Also, you should use a program header for every shell script that you write. These are simply good software engineering practices. A program header is a set of introductory comments used to explain the script. Program header and in-code comments help a programmer who has been assigned the task of maintaining (i.e., modifying or enhancing) your code to understand it quickly. They also help you understand your own code, in particular, if you reread it after some period of time. Long ago, putting comments in the program code or creating separate documentation for programs was not a common practice. Such programs when inherited by a programmer or a team are very difficult to understand and maintain, and are commonly known as legacy code. You may find different definitions for legacy code in the literature.

A good program header must contain at least the following items. In addition, you can insert any other items that you feel are important or are commonly used in your organization or group as part of its coding rules.

- 1. Name of the file containing the script
- 2. Name of the author
- 3. Date written
- 4. Date last modified
- 5. Purpose of the script (in one or two lines)
- 6. A brief description of the algorithm used to implement the solution to the problem at hand

A comment line, including every line in the program header, must start with the number sign (#), as in.

```
# This is a comment line.
```

However, a comment does not have to start at a new line; it can follow a command, as in

```
set Var1=a Var2 Var3=b  # Assign "a" to Var1, "b" to Var3, and
# declare a variable Var2 with an initial
# value of null.
```

The following is a sample header for the set_demo script.

```
# File Name:        ~/Cshell/examples/set_demo
# Author:           Syed Mansoor Sarwar
# Date Written:     August 10, 1999 (by the original author)
# Modified:         May 21, 2004 (by the original author)
# Last Modified     September 7, 2014
# Purpose:          To illustrate how the set command works
# Brief Description: The script runs with a filename as the only
#                    command line argument, saves the filename,
#                    runs the set command to assign the output
#                    of the ls -il command to positional
#                    arguments ($1-$9), and displays file name,
#                    its inode number, file permissions, and
#                    file size (in bytes).
```

We do not show the program headers for all of the sample scripts in this textbook for the sake of brevity.

## 14.7 PROGRAM CONTROL FLOW COMMANDS

The program control flow commands/statements are used to determine the sequence in which statements in a shell script execute. The four basic types of statements for controlling the flow of a script are two-way branching, multiway branching, repetitive execution of a group of commands/statements, and transferring control to a particular statement via a jump or goto statement of some sort. The C shell statement for two-way branching is the if statement, the statements for multiway branching are the if and switch statements, and the statements for repetitive execution of some code are the foreach and while statements. In addition, the C shell has a goto statement that allows you to jump to any command in a program.

### 14.7.1 The if-then-else-endif Statement

The most basic form of the if statement is used for one-way branching, but the statement can also be used for multiway branching. The following is a brief description of the statement. The words in monospace type are keywords and must be used as shown in the syntax. Everything in brackets is optional. All the command lists are designed to help you accomplish the task at hand.
