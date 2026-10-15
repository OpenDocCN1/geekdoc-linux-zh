
## EXPLANATION

+   1 The outer for loop is started. The first time in the loop, Jan is assigned to month.
+   2 The inner for loop starts. The first time in this loop, 1 is assigned to week. The inner loop iterates completely before going back to the outer loop.
+   3 If the user enters either an n or presses Enter, line 4 is executed.
+   4 The continue command with an argument of 2 starts control at the top of the second outermost loop. The continue without an argument returns control to the top of the innermost loop.
+   5 Control is returned to the innermost for loop.
+   6 This done terminates the innermost loop.
+   7 This done terminates the outermost loop.

## 8.6.7 I/O Redirection and Subshells

Input can be piped or redirected to a loop from a file. Output can also be piped or redirected to a file from a loop. The shell starts a subshell to handle I/O redirection and pipes. Any variables defined within the loop will not be known to the rest of the script when the loop terminates.

## Redirecting the Output of a Loop to a File.

See Example 8.41 for a demonstration of how to redirect the output of a loop to a file.

## EXAMPLE 8.41

```
(The Command Line)
1 $ cat memo
abc
def
ghi

(The Script)
#!/bin/sh
# Program name: numberit
# Put line numbers on all lines of memo
2 if [ $# -lt 1 ]
then
3 echo "Usage: $0 filename" >&2
exit 1
fi
4 count=1        # Initialize count
5 cat $1 | while read line   # Input is coming from file on command line
do
```

## EXAMPLE 8.41 (CONTINUED)

```
6  [ $count -eq 1 ] && echo "Processing file $1..." > /dev/tty
7  echo $count $line
8  count=`expr $count + 1`
9  done > tmp$$        # Output is going to a temporary file
10 mv tmp$$ $1
```

(The Command Line)

```
11 $ numberit memo
    Processing file memo...
```

```
12 $ cat memo
    1 abc
    2 def
    3 ghi
```

## EXPLANATION

+   1 The contents of file memo are displayed.
+   2 If the user did not provide a command-line argument when running this script, the number of arguments ($#) will be less than 1 and the error message appears.
+   3 The usage message is sent to stderr (>&2) if the number of arguments is less than 1.
+   4 The count variable is assigned the value 1.
+   5 The UNIX cat command displays the contents of the filename stored in $1, and the output is piped to the while loop. The read command is assigned the first line of the file the first time in the loop, the second line of the file the next time through the loop, and so forth. The read command returns a 0 exit status if it is successful in reading input and 1 if it fails.
+   6 If the value of count is 1, the echo command is executed and its output is sent to /dev/tty, the screen.
+   7 The echo command prints the value of count, followed by the line in the file.
+   8 The count is incremented by 1.
+   9 The output of this entire loop, each line of the file in $1, is redirected to the file tmp$$, with the exception of the first line of the file, which is redirected to the terminal, /dev/tty.
+   10 The tmp file is renamed to the filename assigned to $1.
+   11 The program is executed. The file to be processed is called memo.
+   12 The file memo is displayed after the script has finished, demonstrating that line numbers have been prepended to each line.

> a. $$ expands to the PID number of the current shell. By appending this number to the filename, the filename is made unique.

## 8.6 Looping Commands

## EXAMPLE 8.4

```
(The Input File)
$ cat testing
apples
pears
peaches

(The Script)
#!/bin/sh
# This program demonstrates the scope of variables when
# assigned within loops where the looping command uses
# redirection. A subshell is started when the loop uses
# redirection, making all variables created within the loop
# local to the shell where the loop is being executed.
1  while read line
2  do
3      echo $line   # This line will be redirected to outfile
       name=JOE
4  done < testing > outfile  # Redirection of input and output
5  echo Hi there $name

(The Output)
Hi there
```

## EXPLANATION

+   1. If the exit status of the read command is successful, the body of the while loop is entered. The read command is getting input from the file testing, named after the done on line 4. Each time through the loop, the read command reads another line from the file testing.
+   2. The value of line will be redirected to outfile in line 4.
+   3. The variable name is assigned JOE. Because redirection is utilized in this loop, the variable is local to the loop.
+   4. The done keyword consists of the redirection of input from the file testing, and the redirection of output to the file outfile. All output from this loop will go to outfile.
+   5. When out of the loop, name is undefined. It was local to the while loop and known only within the body of that loop. Because the variable name has no value, only the string Hi there is displayed.
