
## EXAMPLE 9.50

```
1 % set pathvar = /home/danny/program.c
2 % echo $pathvar:r
/home/danny/program
3 % echo $pathvar:h
/home/danny
4 % echo $pathvar:t
program.c
5 % echo $pathvar:e
c
6 % set pathvar = ( /home/* )
echo $pathvar
/home/jody /home/local /home/lost+found /home/perl /home/tmp
7 % echo $pathvar:gt
jody local lost+found perl tmp
```

## EXPLANATION

- 1 The variable pathvar is set to /home/danny/program.c
- 2 When :r is appended to the variable, the extension is removed when displayed.
- 3 When :h is appended to the variable, the head of the path is displayed; that is, the last element of the path is removed.
- 4 When :t is appended to the variable, the tail end of the path (the last element) is displayed.
- 5 When :e is appended to the variable, the extension is displayed.
- 6 The variable is set to /home/*. The asterisk expands to all the pathnames in the current directory starting in /home/.
- 7 When :gt is appended to the variable, the tail end of each (global) of the path elements is displayed.

## 9.11 Command Substitution

A string or variable can be assigned the output of a UNIX command by placing the command in backquotes. This is called command substitution. (On the keyboard, the backquote is normally below the tilde character.) If the output of a command is assigned to a variable, it is stored as a wordlist (see "Arrays" on page 447) not a string, so that each of the words in the list can be accessed separately. To access a word from the list, a subscript is appended to the variable name. Subscripts start at 1.

## EXAMPLE 9.60

```
1 % echo The name of my machine is `uname -n`.
The name of my machine is stardust.
2 % echo The present working directory is `pwd`.
The present working directory is /home/stardust/john.
3 % set d = `date`
% echo $d
Sat Jun 20 14:24:21 PDT 2004
4 % echo $d[2] $d[6]
Jun 2004
5 % set d = "`date`"
% echo $d[1]
Sat Jun 20 14:24:21 PDT 2004
```

## EXPLANATION

- 1 The UNIX command uname -n is enclosed in backquotes. When the shell encounters the backquotes, it will execute the enclosed command, uname -n, and substitute the output of the command, stardust, into the string. When the echo command prints its arguments to standard output, the name of the machine will be one of its arguments.
- 2 The UNIX command pwd is executed by the shell and the output is substituted in place within the string.
- 3 The local variable d is assigned the output of the date command. The output is stored as a list of words (an array).
- 4 Elements 2 and 6 of the d array are printed. The subscripts start at 1.
- 5 Because the output is enclosed in double quotes, it is a single string rather than a wordlist.

### 9.11.1 Wordlists and Command Substitution

When a command is enclosed in backquotes and assigned to a variable, the resulting value is an array (wordlist). Each element of the array can be accessed by appending a subscript to the array name. The subscripts start at 1. If a subscript that is greater than the number of words in the array is used, the C shell prints Subscript out of range. If the output of a command consists of more than one line, the newlines are stripped from each line and replaced with a single space.

## EXAMPLE 9.61

```
1 % set d = `date`
% echo $d
Fri Aug 27 14:04:49 PDT 2004
```

## EXAMPLE 9.61 (CONTINUED)

```
2  % echo $d[1-3]
Fri Aug 27
3  % echo $d[6]
2004
4  % echo $d[7]
Subscript out of range.
5  % echo "The calendar for the month of November is `cal 11 2004`"
The calendar for month of November is November 2004 S M Tu W
Th F S 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21
22 23 24 25 26 27 28 29 30
```

## EXPLANATION

- 1. The variable d is assigned the output of the UNIX date command. The output is stored as an array. The value of the variable is displayed.
- 2. The first three elements of the array are displayed.
- 3. The sixth element of the array is displayed.
- 4. There are not seven elements in the array. The shell reports that the subscript is out of range.
- 5. The output spans more than one line. Each newline is replaced with a space. This may not be the output you expected.

## EXAMPLE 9.62

```
1  % set machine = `users | awk '/tom/{print $1}'`
2  % echo $machine
dumbo bambi dolphin
3  % echo $#machine
3
4  % echo $machine[$#machine]
dolphin
5  % echo $machine
dumbo bambi dolphin
6  % shift $machine
% echo $machine
bambi dolphin
7  % echo $machine[1]
bambi
8  % echo $#machine
2
```
