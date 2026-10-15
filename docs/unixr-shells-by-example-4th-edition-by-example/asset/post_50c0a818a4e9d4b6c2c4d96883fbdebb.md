
# Comments.

Comments are lines preceded by a pound sign. They are used to document your script. It is sometimes difficult to understand what the script is supposed to do if it is not commented. Although comments are important, they are often too sparse or not even used at all. Try to get used to commenting what you are doing not only for someone else, but also for yourself. Two days from now you may not remember exactly what you were trying to do.

## Making the Script Executable.

When you create a file, it is not given execute permission. You need this permission to run your script. Use the chmod command to turn on execute permission.

### EXAMPLE 10.1

```
1 % chmod +x myscript
2 % ls -lF myscript
-rwxr-xr-x 1 ellie 0 Jul 13:00 myscript*
```

### EXPLANATION

- 1 The chmod command is used to turn on execute permission for the user, the group, and others.
- 2 The output of the ls command indicates that all users have execute permission on the myscript file. The asterisk at the end of the filename (resulting from the -F option) also indicates that this is an executable program.

## An Example Scripting Session.

In the following example, the user will create the script in the editor. After saving the file, the execute permissions are turned on with the chmod command, and the script is executed. If there are errors in the program, the C shell will respond immediately.

### EXAMPLE 10.2

```
(The Script - info)
#!/bin/csh -f
# Scriptname: info
1 echo Hello $ {LOGNAME}!
2 echo The hour is `date +%H`
3 echo "This machine is `uname -n`"
4 echo The calendar for this month is
5 cal
6 echo The processes you are running are:
7 ps -ef | grep "A $LOGNAME"
8 echo "Thanks for coming. See you soon!\!\!"

(The Command Line)
% chmod +x info
% info
```

### EXAMPLE 10.2 (CONTINUED)

```
1 Hello ellie!
2 The hour is 09
3 This machine is jody
4 The calendar for this month is
5 July 2004
   S M Tu W Th F S
      1  2  3
 4  5  6  7  8  9 10
11 12 13 14 15 16 17
18 19 20 21 22 23 24
25 26 27 28 29 30 31
7 The processes you are running are:
< output of ps prints here >
8 Thanks for coming. See you soon!!
```

### EXPLANATION

1 The user is greeted. The variable LOGNAME holds the user's name. On BSD systems, USER is used. The curly braces shield the variable from the exclamation point. The exclamation point does not need to be escaped because it will not be interpreted as a history character unless there is a character appended to it.

2 The date command is enclosed in backquotes. The shell will perform command substitution and the date's output, the current hour, will be substituted into the echo string.

3 The uname -n command displays the machine name.

4, 5 The cal command is not enclosed in backquotes because when the shell performs command substitution, the newlines are all stripped from the output. This produces a strange-looking calendar. By putting the cal command on a line by itself, the formatting is preserved. The calendar for this month is printed.

6, 7 The user's processes are printed. Use ps -aux for BSD or ps au with Linux.
The string is printed. Note that the two exclamation points are prepended with backslashes. This is necessary to prevent history substitution.

8

> a. Linux supports a variety of different style options, including UNIX98, BSD and GNU. See your man page for ps.

## 10.2 Reading User Input

### 10.2.1 The $ < Variable

To make a script interactive, a special C shell variable is used to read standard input into a variable. The $ < symbol reads a line from standard input up to but not including the newline, and assigns the line to a variable.1

> 1. Another way to read one line of input is set variable = `head -1'.

### EXAMPLE 10.3

```
(The Script - greeting)
#!/bin/csh -f
# The greeting script
1 echo -n "What is your name? "
2 set name = $<
3 echo Greetings to you, $name.

(The Command Line)
% chmod +x greeting
% greeting
1 What is your name? Dan Savage
3 Greetings to you, Dan Savage.
```

### EXPLANATION

- 1 The string is echoed to the screen. The -n option causes the echo command to suppress the newline at the end of the string. On some versions of echo, use a \c at the end of the string to suppress the newline; for example, echo hello\c.
- 2 Whatever is typed at the terminal, up to a newline, is stored as a string in the name variable.
- 3 The string is printed after variable substitution is performed.

## 10.2.2 Creating a Wordlist from the Input String

Because the input from the $ < > variable is stored as a string, you may want to break the string into a wordlist.

### EXAMPLE 10.4

```
1 % echo What is your full name? 
2 % set name = $<
Lola Justin Lue
3 % echo Hi $name[1]
Hi Lola Justin Lue
4 % echo $name[2]
Subscript out of range.
5 % set name = ( $name )
6 % echo Hi $name[1]
Hi Lola
7 % echo $name[2] $name[3]
Justin Lue
```
