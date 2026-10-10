
Note that each option is preceded by a hyphen.

Most commands allow you to specify multiple options. Thus, to prepare a reversed long listing of all files in the directory `Dir`, flagging directories and executable files, you could type

$ ls -a -l -r -F Dir (Return)

Or you could combine the options:

$ ls -alrF Dir (Return)

Incidentally, anything that follows the command name—including the options and file names—is generally referred to as an argument.

### 8.4 The Standard Input, Output, and Error

Whenever you run a UNIX command, the operating system opens up three standard channels for input and output:

- Standard input. The standard input (or stdin) is the place the program normally looks for input.
- Standard output. The standard output (or stdout) is where the program sends its output.
- Standard error. The standard error (or stderr) is used by the program to display error messages.

### 8.5 Redirection

Most of the time we use terms "standard input" and "standard output" as synonyms for the keyboard and terminal screen, respectively. However, the shell allows you to redirect the standard output so that output goes into a file instead. For example, you have already seen how to use the output redirection operator (>) to create a file containing a calendar:

$ cal 1999 > calendar.file (Return)

You can add output to a file using the append operator (>>):

$ cal 2000 >> calendar.file (Return)

It is also possible to redirect the standard input so that a process takes its input from a file rather than the keyboard. For example, the mail command allows you to send and read electronic mail. To send the contents of the file `my.message` to the user `jones`, you could enter the command line

$ mail jones < my.message (Return)

You can combine input and output redirection in the same command line. For example, the following command line invokes the *wc* utility to count the lines, words, and characters in the file `input`, then redirects the results into the file `output`:

$ wc < input > output (Return)

### 8.6 Grouping Commands

Normally you type one command at a time, following each command by a (Return), which is the signal for the shell to begin its work. However, it is possible to put multiple commands on the same line, if you separate the commands with semicolons. Thus the command line

$ who; ls; cal (Return)

has the same effect as the three separate command lines

$ who (Return)
$ ls (Return)
$ cal (Return)

Grouping commands can be especially useful when you want to redirect the output into a file. You could make a calendar for the summer of 1999 in three steps:

$ cal 6 1999 > summer99 (Return)
$ cal 7 1999 >> summer99 (Return)
$ cal 8 1999 >> summer99 (Return)

You could accomplish the same thing with just one line:

$ (cal 6 1999; cal 7 1999; cal 8 1999) > summer99 (Return)

Note the parentheses; these are necessary to make sure the calendars for June, July, and August are all redirected into the same file. Suppose you were to omit the parentheses, like this:

$ cal 6 1999; cal 7 1999; cal 8 1999 > summer99 (Return)

In this case, the calendars for June and July would appear on the screen, and only the August calendar would be redirected into the file.

### 8.7 Pipes

Suppose you wanted to display the calendars for the years 1999, 2000, and 2001, one right after the other. You could type the command line

$ cal 1999; cal 2000; cal 2001 (Return)

This will print the calendars on the standard output, but they will scroll by so fast that you cannot read them. One way around this problem is to redirect the output into a file:

$ (cal 1999; cal 2000; cal 2001) > temp (Return)

Now you can view the contents of `temp` using the `more` or `pg` utility:

$ more temp (Return)

or

$ pg temp (Return)

This will work, but it requires that you create a temporary file just to look at the output from the commands. You can avoid creating a file by using what is called a *pipe* which connects the output from one utility to the input of another. A vertical bar (|) is the pipe symbol. You would pipe the output from *command1* to *command2* like this:

command1 | command2

Thus, to view the calendars for 1999, 2000, and 2001, we can pipe the output of the `cal` utility to either `more` or `pg`:

$ (cal 1999; cal 2000; cal 2001) | more (Return)

or

$ (cal 1999; cal 2000; cal 2001) | pg (Return)

Note how this differs from redirection with > or >>. Redirection places the output from a utility into a file; the piping operation directs the output to another utility.

### 8.8 Tees

A *tee* allows you to save the output from a command in a file at the same time the output is piped to another command. We could take the output from **command1** and send it to the file **outfile** and to **command2** like this:

command1 | tee outfile | command2

Thus the command line

$ (cal 2000; cal 2001) | tee calfile | more (Return)

places copies of the calendars for 2000 and 2001 into the file *calfile* as they are also displayed on the terminal screen by *more*.

### 8.9 Filters

A **filter** takes a stream of data from its standard input, transforms the data in some way, and sends the results to the standard output. Here are some of the filters commonly found on UNIX systems.

| Filter | Function |
| :--- | :--- |
| cat | Concatenate and display text |
| comm | Compare sorted files, selecting or rejecting lines common to both |
| crypt | Encode or decode text |
| cut | Cut out selected fields from input lines |
| diff | Display line-by-line differences between two files |
| egrep | Search text for a pattern using full regular expressions |
| fgrep | Search text for a character string |
| fmt | Format text |
| grep | Search a file for a pattern |
| head | Display the beginning (head) of a file |
| more | Show text, one screenful at a time |
| nl | Number lines |
| paste | Merge lines of text |
| pg | Show text, one screenful at a time |
| pr | Format and print text |
| sort | Sort and/or merge text |
| spell | Check for spelling errors |
| tail | Display last part of a file |
| tr | Translate characters |
| uniq | Display lines in a file that are unique |
| wc | Count number of lines, words, and characters in text |

Filters are often used with pipes and tee. Consider the **sort** utility, which, as you might expect, sorts its input. Suppose you wanted to list, alphabetically by their login names, the users currently logged onto your machine. You could do this by piping the output from **who** into **sort**:

$ who | sort (Return)

You can also give **sort** the name of a file to sort:

$ sort poems (Return)

This would sort the lines of the file `poems` alphabetically by the first character of the line.

### 8.10 Wildcards

Typing and retyping file names can be a nuisance, especially if the names are long or there are very many of them. You can abbreviate file names using wildcards, which are characters that can stand for other characters (just as a joker in a pack of cards can stand for other cards in the pack). The wildcard symbols are the asterisk (*), the question mark (?), and the square brackets [ ]. To see how these symbols are used, suppose that you had a directory named `Fun` containing the following files:

- backgammon
- backpacking
- baseball
- basketball
- biking
- blackjack
- boxing
- bridge
- camping
- canoeing
- checkers
- chess
- crossword
- dancing
- eating
- fencing
- fishing
- football
- golf
- hearts
- hiking
- karate
- poker
- rugby
- sailing
- skiing
- softball
- swimming
- team1
- team2
- team3
- team4
- teamA
- teamB
- teamC
- teamD
- teamM
- teamW
- teamX
- teamY
- teamZ
- track
- wrestling

The asterisk (*) is by far the most commonly used wildcard. It matches any character or string of characters, including blanks. As you can see, the directory `Fun` contains a large number of files. Using wildcards you can avoid having to list all of them when you are interested in just a few. For example, the command

$ ls f* (Return)

will cause the shell to list only those files beginning in f:

fencing fishing football

The command

$ ls *ball (Return)

will cause the shell to list the files that end in ball:

baseball basketball football softball
