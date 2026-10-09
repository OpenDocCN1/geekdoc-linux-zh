
## type: DISPLAYS INFORMATION ABOUT A COMMAND

The `type` builtin provides information about a command:

```bash
$ type cat echo who if lt
cat is hashed (/bin/cat)
echo is a shell builtin
who is /usr/bin/who
if is a shell keyword
lt is aliased to 'ls -ltrh | tail'
```

The preceding output shows the files that would be executed if you gave `cat` or `who` as a command. Because `cat` has already been called from the current shell, it is in the *bash table* (page 1151) and `type` reports that `cat` is `hashed`. The output also shows that a call to `echo` runs the `echo` builtin, `if` is a keyword, and `lt` is an alias.

## read: ACCEPTS USER INPUT

One of the most common uses for user-created variables is storing information that a user enters in response to a prompt. Using `read`, scripts can accept input from the user and store that input in variables. The `read` builtin reads one line from standard input and assigns the words on the line to one or more variables:

```bash
$ cat read1
echo -n "Go ahead: "
read firstline
echo "You entered: $firstline"

$ ./read1
Go ahead: This is a line.
You entered: This is a line.
```

The first line of the `read1` script uses `echo` to prompt for a line of text. The `-n` option suppresses the following NEWLINE, allowing you to enter a line of text on the same line as the prompt. The second line reads the text into the variable `firstline`. The third line verifies the action of `read` by displaying the value of `firstline`. The variable is quoted (along with the text string) in this example because you, as the script writer, cannot anticipate which characters the user might enter in response to the prompt. Consider what would happen if the variable were not quoted and the user entered `*` in response to the prompt:

```bash
$ cat read1_no_quote
echo -n "Go ahead: "
read firstline
echo You entered: $firstline

$ ./read1_no_quote
Go ahead: *
You entered: read1 read1_no_quote script.1

$ ls
read1 read1_no_quote script.1
```

The `ls` command lists the same words as the script, demonstrating that the shell expands the asterisk into a list of files in the working directory. When the variable `$firstline` is surrounded by double quotation marks, the shell does not expand the asterisk. Thus the `read1` script behaves correctly:

```bash
$ ./read1
Go ahead: *
You entered: *
```

**REPLY** The `read` builtin includes several features that can make it easier to use. For example, when you do not specify a variable to receive `read`'s input, bash puts the input into the variable named `REPLY`. You can use the `-p` option to prompt the user instead of using a separate `echo` command. The following `read1a` script performs exactly the same task as `read1`:

```bash
$ cat read1a
read -p "Go ahead: "
echo "You entered: $REPLY"
```

The `read2` script prompts for a command line, reads the user's response, and assigns it to the variable `cmd`. The script then attempts to execute the command line that results from the expansion of the `cmd` variable:

```bash
$ cat read2
read -p "Enter a command: " cmd
$cmd
echo "Thanks"
```

In the following example, `read2` reads a command line that calls the `echo` builtin. The shell executes the command and then displays `Thanks`. Next `read2` reads a command line that executes the `who` utility:

```bash
$ ./read2
Enter a command: echo Please display this message.
Please display this message.
Thanks

$ ./read2
Enter a command: who
max     pts/4     2010-06-17 07:50  (:0.0)
sam     pts/12    2010-06-17 11:54  (bravo.example.com)
Thanks
```

If `cmd` does not expand into a valid command line, the shell issues an error message:

```bash
$ ./read2
Enter a command: xxx
./read2: line 2: xxx: command not found
Thanks
```

The `read3` script reads values into three variables. The `read` builtin assigns one word (a sequence of nonblank characters) to each variable:

```bash
$ cat read3
read -p "Enter something: " word1 word2 word3
echo "Word 1 is: $word1"
echo "Word 2 is: $word2"
echo "Word 3 is: $word3"

$ ./read3
Enter something: this is something
Word 1 is: this
Word 2 is: is
Word 3 is: something
```

When you enter more words than `read` has variables, `read` assigns one word to each variable, assigning all leftover words to the last variable. Both `read1` and `read2` assigned the first word and all leftover words to the one variable the scripts each had to work with. In the following example, `read` assigns five words to three variables: It assigns the first word to the first variable, the second word to the second variable, and the third through fifth words to the third variable.

```bash
$ ./read3
Enter something: this is something else, really.
Word 1 is: this
Word 2 is: is
Word 3 is: something else, really.
```

Table 27-4 lists some of the options supported by the `read` builtin.

### Table 27-4 read options

| Option | Function |
|---|---|
| `-a aname` | (array) Assigns each word of input to an element of array *aname* |
| `-d delim` | (delimiter) Uses *delim* to terminate the input instead of NEWLINE. |
| `-e` | (Readline) If input is coming from a keyboard, uses the Readline Library (page 340) to get input. |
| `-n num` | (number of characters) Reads *num* characters and returns. As soon as the user types *num* characters, `read` returns; there is no need to press RETURN. |
| `-p prompt` | (prompt) Displays *prompt* on standard error without a terminating NEWLINE before reading input. Displays *prompt* only when input comes from the keyboard. |
| `-s` | (silent) Does not echo characters. |
| `-u n` | (file descriptor) Uses the integer *n* as the file descriptor that `read` takes its input from. Thus |

```bash
read -u4 arg1 arg2
```

is equivalent to

```bash
read arg1 arg2 <&4
```

See “File Descriptors” (page 987) for a discussion of redirection and file descriptors.

The `read` builtin returns an exit status of 0 if it successfully reads any data. It has a nonzero exit status when it reaches the EOF (end of file).

The following example runs a **while** loop from the command line. It takes its input from the **names** file and terminates after reading the last line from **names**.

```bash
$ cat names
Alice Jones
Robert Smith
Alice Paulson
John Q. Public

$ while read first rest
> do
> echo $rest, $first
> done < names
Jones, Alice
Smith, Robert
Paulson, Alice
Q. Public, John
$
```

The placement of the redirection symbol (`<`) for the **while** structure is critical. It is important that you place the redirection symbol at the **done** statement and not at the call to `read`.

> **optional** Each time you redirect input, the shell opens the input file and repositions the read pointer at the start of the file:
>
> ```bash
> $ read line1 < names; echo $line1; read line2 < names; echo $line2
> Alice Jones
> Alice Jones
> ```
>
> Here each `read` opens `names` and starts at the beginning of the `names` file. In the following example, `names` is opened once, as standard input of the subshell created by the parentheses. Each `read` then reads successive lines of standard input:
>
> ```bash
> $ (read line1; echo $line1; read line2; echo $line2) < names
> Alice Jones
> Robert Smith
> ```
>
> Another way to get the same effect is to open the input file with `exec` and hold it open (refer to “File Descriptors” on page 987):
>
> ```bash
> $ exec 3< names
> $ read -u3 line1; echo $line1; read -u3 line2; echo $line2
> Alice Jones
> Robert Smith
> $ exec 3<&-
> ```

## exec: EXECUTES A COMMAND OR REDIRECTS FILE DESCRIPTORS

The **exec** builtin has two primary purposes: to run a command without creating a new process and to redirect a file descriptor—including standard input, output, or error—of a shell script from within the script (page 987). When the shell executes a command that is not built into the shell, it typically creates a new process. The new process inherits environment (global or exported) variables from its parent but does not inherit variables that are not exported by the parent. (For more information refer to “Locality of Variables” on page 992.) In contrast, `exec` executes a command in place of (overlays) the current process.

### exec: EXECUTES A COMMAND

The `exec` builtin used for running a command has the following syntax:

```bash
exec command arguments
```

Insofar as `exec` runs a command in the environment of the original process, it is similar to the `. (dot)` command (page 296). However, unlike the `. command`, which can run only shell scripts, `exec` can run both scripts and compiled programs. Also, whereas the `. command` returns control to the original script when it finishes running, `exec` does not. Finally, the `. command` gives the new program access to local variables, whereas `exec` does not.

Because the shell does not create a new process when you use `exec`, the command runs more quickly. However, because `exec` does not return control to the original program, it can be used only as the last command in a script. The following script shows that control is not returned to the script:

```bash
$ cat exec_demo
who
exec date
echo "This line is never displayed."

$ ./exec_demo
zach pty/7 May 20 7:05 (bravo.example.com)
hls pty/1 May 20 6:59 (:0.0)
Mon May 24 11:42:56 PDT 2010
```

The next example, a modified version of the `out` script (page 959), uses `exec` to execute the final command the script runs. Because `out` runs either `cat` or `less` and then terminates, the new version, named `out2`, uses `exec` with both `cat` and `less`:

```bash
$ cat out2
if [ $# -eq 0 ]
then
    echo "Usage: out2 [-v] filenames" 1>&2
    exit 1
fi
if [ "$1" = "-v" ]
then
    shift
    exec less "$@"
else
    exec cat -- "$@"
fi
```

### exec: REDIRECTS INPUT AND OUTPUT

The second major use of `exec` is to redirect a file descriptor—including standard input, output, or error—from within a script. The next command causes all subsequent input to a script that would have come from standard input to come from the file named `infile`:

```bash
exec < infile
```
