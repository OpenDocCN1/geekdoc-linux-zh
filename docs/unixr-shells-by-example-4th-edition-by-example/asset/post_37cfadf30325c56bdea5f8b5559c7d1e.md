
## Using a Script As an Argument to ksh.

If you don't make a script executable, you can execute it by passing it as an argument to the ksh command.

### EXAMPLE 12.3

```
(The Command Line)
$ ksh myscript
```

### EXPLANATION

If the ksh program is given a script name as its argument, it will execute the script and the #! line is not necessary or even used.

## A Scripting Session.

In Example 12.4, the user will create a script in the editor. After saving the file, the execute permissions are turned on, and the script is executed. If there are errors in the program, the Korn shell will respond immediately.

### EXAMPLE 12.4

```
(The Script)
1 #!/bin/ksh
2 # This is the first Korn shell program of the day.
# Scriptname: greetings
# Written by: Karen Korny
3 print "Hello $LOGNAME, it's nice talking to you."
4 print "Your present working directory is $pwd."
print "You are working on a machine called $(uname -n)."
print "Here is a list of your files."
5 ls   # List files in the present working directory
print "Bye for now $LOGNAME. The time is $(date +%T)!"
```

```
(The Command Line)
$ chmod +x greetings
$ greetings
3 Hello karen, it's nice talking to you.
4 Your present working directory is /home/lion/karen/junk
You are working on a machine called lion.
Here is a list of your files.
5 Afiles cplus library prac
Answerbook cprog library prac1
bourne joke notes perl5
Bye for now karen. The time is 18:05:07!
```

### EXPLANATION

- 1 The first line of the script, #!/bin/ksh, lets the kernel know what interpreter will execute the lines in this program.
- 2 The comments are nonexecutable lines preceded by a #. They can be on a line by themselves or inserted in a line after a command.
- 3 The print command displays the line on the screen, after variable substitution is performed by the shell.
- 4 The print command displays the line on the screen, after command substitution is performed by the shell.
- 5 The ls command is executed. The comment, any text on the line after the pound sign (#), will be ignored by the shell.

## 12.2 Reading User Input

The read command is used to take input from the terminal or from a file until the newline is reached. The Korn shell provides some additional options for the read command. See Table 12.1 for different read formats. See Table 12.2 for read options.

### Table 12.1 read Formats

| Format | Meaning |
|---|---|
| read answer | Reads a line from standard input and assigns it to the variable answer. |
| read first last | Reads a line from standard input to the first whitespace or newline, putting the first word typed into the variable first and the rest of the line into the variable last. |
| read response?"Do you feel okay?" | Displays the string Do you feel okay? to standard error and waits for the user to type a reply, then puts the reply in the variable response. This form of read requires and accepts only one variable. Whatever the user types, until the newline, will be stored in response. |
| read -u3 line | Reads a line from file descriptor 3 into variable line. |
| read | Reads input into a built-in variable, REPLY. |

### Table 12.2 read Options

| Options | Meaning |
|---|---|
| -p | Reads a line of input from a coprocess. |
| -r | Treats newline character, the \n, as a literal. |
| -s | Copies a line into the history file. |
| -un | Reads from file descriptor n; the default is fd 0, or standard input. |
| **On Versions of ksh Newer Than 1988** | |
| -A | Stores the fields as an array; index starting at zero. |
| -d char | Used as an alternate delimiter for terminating input; newline is the default. |
| -t sec | Puts a limit of seconds on the user's response time. |

### EXAMPLE 12.5

```
(The Script)
#!/bin/ksh
# Scriptname: nosy
print -n "Are you happy? "
1 read answer
print "$answer is the right response."
print -n "What is your full name? "
2 read first middle last
print "Hello $first"
print -n "Where do you work? "
3 read
4 print I guess $REPLY keeps you busy!
5 read place?"Where do you live? "
# New ksh read and print combined
print Welcome to $place, $first $last
```

```
(The Output)
$ nosy
Are you happy? Yes
1 Yes is the right response.
2 What is your full name? Jon Jake Jones
Hello Jon
3 Where do you work? Tandem
4 I guess Tandem keeps you busy!
5 Where do you live? Timbuktu
Welcome to Timbuktu, Jon Jones
```

### EXPLANATION

- 1. The read command accepts a line of user input and assigns the input to the variable answer.
- 2. The read command accepts input from the user and assigns the first word of input to the variable first, assigns the second word of input to the variable middle, and all the rest of the words to the end of the line to the variable last.
