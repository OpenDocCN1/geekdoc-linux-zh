
## Setting History.

The C shell history variable is set to the number of events you want to save from the history list and display on the screen. Normally, this is set in the .cshrc file, the user's initialization file.

### EXAMPLE 9.12

```
set history=50
```

### EXPLANATION

The last 50 commands typed at the terminal are saved and may be displayed on the screen by typing the history command.

## Saving History.

To save history events across logins, set the savehist variable. This variable is normally set in the .cshrc file, the user's initialization file.

### EXAMPLE 9.13

```
set savehist=25
```

### EXPLANATION

The last 25 commands from the history list are saved and will be at the top of the history list the next time you log in.

## Displaying History.

The history command displays the events in the history list. The history command also has options that control the number of events and the format of the events that will be displayed. The numbering of events does not necessarily start at 1. If you have 100 commands on the history list, and you have set the history variable to 25, you will only see the last 25 commands saved. (The TC shell supports the use of the arrow keys. See "Accessing Commands from the History File" on page 470.)

### EXAMPLE 9.14

```
% history
1 ls
2 vi file1
3 df
4 ps -eaf
5 history
6 more /etc/passwd
7 cd
8 echo $USER
9 set
```

### EXPLANATION

The history list is displayed. Each command is numbered.

### EXAMPLE 9.15

```
% history -h    # Print without line numbers
ls
vi file1
df
ps -eaf
history
more /etc/passwd
cd
echo $USER
set
history -n
```

### EXPLANATION

The history list is displayed without line numbers.

### EXAMPLE 9.16

```
% history -r    # Print the history list in reverse
11 history -r
10 history -h
9 set
8 echo $USER
7 cd
6 more /etc/passwd
5 history
4 ps -eaf
3 df
2 vi file1
1 ls
```

### EXPLANATION

The history list is displayed in reverse order.

### EXAMPLE 9.17

```
% history 5    # Prints the last 5 events on the history list
7 echo $USER
8 cd
9 set
10 history -n
11 history 5
```

### EXPLANATION

The last five commands on the history list are displayed.

## Re-executing Commands.

To re-execute a command from the history list, the exclamation point (bang) is used. If you type two exclamation points (!!), the last command is re-executed. If you type the exclamation point followed by a number, the number is associated with the command from the history list and the command is executed. If you type an exclamation point and a letter, the last command that started with that letter is executed. The caret (^) is also used as a shortcut method for editing the previous command.

### EXAMPLE 9.18

```
1 % date
Mon Apr 26 8 12:27:35 PST 2004
2 % !!
date
Mon Apr 26 12:28:25 PST 2004
3 % !3
date
Mon Apr 26 12:29:26 PST 2004
4 % !d
date
Mon Apr 26 12:30:09 PST 2004
5 % dare
dare: Command not found.
6 % ^A^t
date
Mon Apr 26 12:33:25 PST 2004
```

### EXPLANATION

- 1 The date command is executed at the command line. The history list is updated.
- 2 The !! (bang bang) gets the last command from the history list; the command is re-executed.
- 3 The third command on the history list is re-executed.
- 4 The last command on the history list that started with the letter d is re-executed.
- 5 The command is mistyped.
- 6 The carets are used to substitute letters from the last command on the history list. The first occurrence of an r is replaced with a t.

### EXAMPLE 9.19

```
1 % cat file1 file2 file3
<Contents of file1, file2, and file3 are displayed here>
% vi 1:1
vi file1
```

### EXAMPLE 9.19 (CONTINUED)

```
2
% cat file1 file2 file3
<Contents of file1, file2, and file3 are displayed here>

% ls !:2
ls file2
file2
```

```
3
% cat file1 file2 file3
% ls !:3
ls file3
file3
```

```
4
% echo a b c
a b c
% echo !$
echo c
c
```

```
5
% echo a b c
a b c
% echo !^ 
echo a
a
```

```
6
% echo a b c
a b c
% echo !:
 echo a b c
a b c
```

```
7
% !!:p
echo a b c
```

### EXPLANATION

1 The cat command displays the contents of file1, file2, and file3 to the screen. The history list is updated. The command line is broken into words, starting with word number 0. If the word number is preceded by a colon, that word can be extracted from the history list. The !:1 notation means: get the first argument from the last command on the history list and replace it in the command string. The first argument from the last command is file1. (Word 0 is the command itself.)

2 The !:2 is replaced with the second argument of the last command, file2, and given as an argument to ls. file2 is printed. (file2 is the third word.)

3 ls !:3 reads: go to the last command on the history list and get the fourth word (words start at 0) and pass it to the ls command as an argument (file3 is the fourth word).
