
# Command Summary 337

pat₁| pat_₂

which means to match either pat₁ or pat_₂

Examples

```
case l1 in
  -1) lopt=TRUE;
  -w) wopt=TRUE;
  -c) copt=TRUE;
  *) echo "Unknown option";
esac
case $choice in
  [1-9]) valid=TRUE;
  *) "Please choose a number from 1-9";
esac
```

# The cd Command

General Format: cd directory

Execution of this command causes the shell to make directory the current directory. If directory is omitted, the shell makes the directory specified in the HOME variable the current directory.

If the shell variable CDPATH is null, directory must be a full path (for example, /users/steve/documents) or relative to the current directory (for example, documents or ../pat).

If CDPATH is non-null and directory is not a full path, the shell searches the colon-delimited list in CDPATH for a directory containing directory.

Examples

```
$ cd documents/memos  Change to documents/memos
$ cd ~               Change to HOME directory
```

An argument - causes the shell to move the user back to the previous directory. The pathname of the new current directory is printed out.

Examples

```
$ pwd
/usr/lib/uucp
$ cd /
$ cd -
/usr/lib/uucp
$ 
```

The cd command sets the shell variable PWD to the new current directory, and OLDPWD to the previous directory.

# The continue Command

General Format: continue

Execution of this command within a for, while, or until loop causes any commands that follow the continue to be skipped. Execution of the loop then continues as normal.

If the format

continue n

is used, the commands within the n innermost loops are skipped. Execution of the loops then continues as normal.

# The echo Command

General Format: echo args

This command causes args to be written to standard output. Each word from args is delimited by a blank space. A newline character is written at the end. If args is omitted, the effect is to simply skip a line.

Certain backslashed characters have a special meaning to echo as shown in Table A.8.

Table A.8 echo Escape Characters
| Character | Prints |
| :--- | :--- |
| \a | Alert |
| \b | Backspace |
| \c | The line without a terminating newline |
| \f | Formfeed |
| \n | Newline |
| \r | Carriage return |
| \t | Tab character |
| \v | Vertical tab character |
| \\ | Backslash character |
| \0nnn | The whose ASCII value is nnn, where nnn is a one-to- three-digit octal number that starts with a zero |

Remember to quote these characters so that the echo command, rather than the shell, interprets them.

# Command Summary 339

# Examples

```
$ echo *
bin docs mail mise srcrc
$ echo
```

List all files in the current directory

Skip a line

```
$ echo 'X\tY'
X       Y
$ echo "\nSales Report"
```

Print X and Y, separated by a tab

Skip two lines before displaying Sales Report

```
Sales Report
$ echo "Wake up!!\a"
Wake up!
$
```

Print message and beep terminal

# The eval Command

General Format: eval args

Execution of this command causes the shell to evaluate args and then execute the results. This is useful for the shell to execute "double-scan" a command.

# Example

```
$ x='abc def'
$ y=$x
$ echo $y
$ eval $y
abc def
```

Assign $x to y

# The exec Command

General Format: exec command args

When the shell executes exec command, it initiates execution of the specified command with the indicated arguments. Unlike other commands, command replaces the current process (no new process is created). After command starts, there is no return to the program that initiated exec. If I/O redirection is specified, the input and output for the shell is redirected accordingly.

# Examples

```
exec /bin/sh < datafile
```

Replace current process with sh reassign input to datafile

# The exit Command

General Format: exit n

Execution of exit causes the shell program to be immediately terminated. The exit status of the program is the value of n, if supplied. If n is not supplied, the status is that of the last command executed.

An exit status of zero is used to indicate success, and non-zero to indicate failure (such as an error). This convention is used by the shell in evaluation of conditions for if, while, and until commands, with the && and || constructs.

Examples

```
who | grep /dev/null
exit 1
if grep then...
Exit with status of last grep
fi
```

Note that executing exit directly from login shell has the effect of logging off.

# The export Command

General Format: export variables

The export command tells the shell that the indicated variables are marked as exported; their values are passed down to subshells.

Examples

```
export PATH PS1
export date
```

Variables may be set when using the form

So lines as

```
PATH=$HOME/bin; export CDPATH=$HOME:/usr/local
```
can be rewritten

```
export PATH=$HOME/bin CDPATH=$HOME:/usr/local
```

The output of export with -p argument is a list of the exported variables and their values in the form

```
export variable=value
```

or

if variable has been exported but does not have its value set.

# The false Command

General Format: false

The false command returns a nonzero exit status.

# The fc Command

General Format: fc -e editor -ln first last [old=new]

The fc command is used to edit commands in the history. A range of commands is specified from first to last, where first and last can be either numbers or strings; a negative number takes as an offset from the current command number, while a string specifies the recently entered command beginning with that string. The commands are read into the editor and executed upon exit. If no editor is specified, the value of the shell variable FCEDIT is used; if FCEDIT is not set, ed is used.

The -l option lists the commands from first to last (that is, an editor is not invoked). If -n option is specified, these commands are not preceded by command numbers.

The -r option to fc reverses the order of the commands.

If last is not specified, it defaults to first. If first is also not specified, it defaults to the previous command for editing and to -16 for listing.

The -s option causes the selected command to be executed without editing it. The format

```
fc -s old=new first
```

causes the command first to be re-executed the old in the command is replaced with new. If first isn't specified, the previous command is used, and if old=new isn't specified, the command is not changed.

Examples

```
fc -l List the last 16 commands
fc -e sed Read the last sed command into vi
fc 100 110 Read commands 100 to 110 into $FCEDIT
fc -s Re-execute the previous command
fc -s abc=def 104 Re-execute command 104, replacing abc with def
```

# The fg Command

General Format: fg job_id

If job control is enabled, the job specified by job_id is brought to the foreground. If no argument is given, the most recently suspended job or the last job sent to the background is brought to the foreground.

Example

fg $2

# The for Command

General Format:

```
for var in word, word, ... word_n
do
    command
    command
done
```

Execution of this command causes the commands enclosed between the do and done to be executed as many times as there are words listed after the in.

The first time through the loop, the first word—word—is assigned to the variable var and the commands between the do and done executed. The second time through the loop, the second word—word—is assigned to var and the commands in the loop executed again.

This process continues until the last variable in the list—word_n—is assigned to var and the commands between the do and done executed. At that point, execution of the for loop is terminated. Execution then continues with the command that immediately follows the done.

The special format

```
for var
do
```

done

indicates that the positional parameters "$1", "$2", ... are to be used in the list and is equivalent to

```
for var in "$@"
do
```

done

Example

```
# nroff all of the files in the current directory
for file in *
```
