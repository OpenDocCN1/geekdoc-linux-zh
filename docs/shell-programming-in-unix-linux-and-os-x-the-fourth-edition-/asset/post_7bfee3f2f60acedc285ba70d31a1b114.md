
## Resetting Traps

After you’ve changed the default action to be taken on receipt of a signal, you can change it back again with trap if you simply omit the first argument; so

```shell
trap HUP INT
```

resets the action to be taken on receipt of the SIGHUP or SIGINT signals back to the default behavior for the shell.

Many shell programs also use a construct like this

```shell
trap "/bin/rm -f $tempfile; exit" INT QUIT EXIT
```

to ensure that the rm command won’t produce an error message if the temporary file hasn’t yet been created upon exit. The trap handler removes the temporary file if it exists and does nothing if it doesn’t.

## More on I/O

You know about the standard constructs <, >, and >> for input redirection, output redirection, and output redirection with append, respectively. You also know that you can redirect standard error from any command simply by writing 2> instead of just >:

```shell
command 2> file
```

Sometimes you may want to explicitly write to standard error in your program. With a slight variation on the above, you can redirect standard output to standard error by writing

```shell
command >&2
```

The notation >& specifies output redirection to a file associated with the file descriptor that follows. File descriptor 0 is standard input, descriptor 1 is standard output, and descriptor 2 is standard error. It’s important to remember that no space is permitted between the > and the &.

To write a message to standard error:

```shell
echo "Invalid number of arguments" >&2
```

You may want to redirect both standard output (often abbreviated “stdout”) and standard error output (“stderr”) from a program into the same file. If you know the name of the file, this is straightforward:

```shell
command > foo 2>> foo
```

Here both stdout and stderr will be written to foo.

You can also write

```shell
command > foo 2>&1
```

to achieve the same effect; standard output is redirected to foo, and standard error is redirected to standard output (which has already been redirected to foo). Because the shell evaluates redirection from left to right on the command line, the last example won’t work properly if the stderr redirection sequence appears first on the command line

```shell
command 2>&1 > foo
```

because this would first redirect standard error to standard output then standard output to foo.

You can also dynamically redirect standard input or output in a program using the exec command:

```shell
exec < datafile
```

redirects standard input from the file datafile. Subsequent commands executed that read from standard input will read from datafile instead. The command

```shell
exec > /tmp/output
```

does the same thing with standard output: all commands that subsequently write to standard output will write to /tmp/output unless explicitly redirected elsewhere.

Naturally, standard error can be reassigned as well:

```shell
exec 2> /tmp/errors
```

All subsequent output to standard error will go to /tmp/errors.

### <&- and >&-

The sequence >&- has the effect of closing standard output. If preceded by a file descriptor, the associated file is closed instead. So writing

```shell
ls >&-
```

causes the output from ls to go nowhere because standard output is closed by the shell before ls is executed. Not hugely useful, we admit!

## In-line Input Redirection

If the << characters follow a command in the format

```shell
command <<word
```

the shell uses the lines that follow as the input for command, until a line that contains just word is found. Here’s a simple example:

```text
$ wc -l <<ENDOFDATA
> here's a line
> and another
> and yet another
> ENDOFDATA
3
$
```

Use lines up to ENDOFDATA as standard input

The shell fed every line typed into the shell as the standard input stream of `wc` until it encountered the line containing just `EOF` followed by RETURN.

In-line input redirection—also referred to as *here documents* by some programmers—is a powerful feature when used inside shell programs. It lets you specify the standard input to a command directly in the program, thus obviating the need to write it into a separate file, or to use `echo` to get it into the standard input of the command.

Here’s a common example of how this feature is used within a shell program:

```shell
$ cat mailmsg
mail $* <<END-OF-DATA

Attention:

Our monthly computer users group meeting
will take place on Friday, March 4, 2016 at
8pm in room 1A-08. Please try to attend.

END-OF-DATA
$
```

To send this message to all members of the group as stored in the file `users_list`, you could invoke

```shell
mailmsg $(cat users_list)
```

The shell performs parameter substitution for the redirected input data, executes back-quoted commands, and recognizes the backslash character.

Special characters within a *here document* are generally ignored, but if you include dollar signs, back quotes, or backslashes in these lines, they can be interpreted. To have them ignored, precede them with a backslash character. Alternatively, if you want the shell to leave all input lines completely untouched, precede the end of document word that follows the `<<` with a backslash.

Let’s highlight the difference between the two:

```text
$ cat <<FOOBAR
> $HOME
> *****
>       \$foobar
> `date`
> FOOBAR                         Terminates the input
/usr/steve
^^^^^^^
       \$foobar
Wed Oct  2 15:23:15 EDT 2002
$
```

Since the shell supplies all the lines up to FOOBAR as the input to `cat` it substitutes the value for `$HOME` but not for `foobar` because the latter is prefaced with a backslash. The `date` command is also executed because back quotes are interpreted by the shell.

To side-step all the issues with the shell interpreting the contents of the lines, use backslash on the *end-of-document* word instead:

```text
$ cat <<\FOOBAR
> \\\\\\\\
> `date`
> $HOME
> FOOBAR
\\\\
`date`
$HOME
$
```

Use care when selecting the word that follows the `<<`. Generally, just make sure that it’s weird enough so that the chances of it accidentally appearing in the subsequent lines of data are minuscule.

You now know about the `<<\` sequence, but there’s another one that most modern shells understand: If the first character that follows the `<<` is a dash (`-`), any leading tab characters in the input will be removed by the shell. This is useful for visually indenting the redirected text for readability while still having it output appear in normal left-aligned form:

```text
$ cat <<-END
>             Indented lines
>             because tabs are cool
> END
Indented lines
because tabs are cool
$
```

## Shell Archives

One of the best uses of the in-line input redirection feature is for creating shell *archive* files. With this technique, one or more related shell programs can be put into a single file and then sent to someone else using the standard Unix `mail` commands. When the archive is received, it can be “unpacked” by invoking it as a shell program.

For example, here’s an archived version of the lu, add, and rem programs used by rolo:

```shell
$ cat rolousb
#
# Archived programs used by rolo.
#

echo Extracting lu
cat >lu <<\THE-END-OF-DATA
#
# Look someone up in the phone book
#

if [ "$#" -ne 1 ]
then
        echo "Incorrect number of arguments"
        echo "Usage: lu name"
        exit 1
fi

name=$1
grep "$name" $PHONEBOOK

if [ $? -ne 0 ]
then
        echo "I couldn't find $name in the phone book"
fi
THE-END-OF-DATA

echo Extracting add
cat >add <<\THE-END-OF-DATA
#
# Program to add someone to the phonebook file
#

if [ "$#" -ne 2 ]
then
        echo "Incorrect number of arguments"
        echo "Usage: add name number"
        exit 1
fi

echo "$1    $2" >> $PHONEBOOK
sort -o $PHONEBOOK $PHONEBOOK
THE-END-OF-DATA

echo Extracting rem
cat >rem <<\THE-END-OF-DATA
#
# Remove someone from the phone book
#

if [ "$#" -ne 1 ]
then
        echo "Incorrect number of arguments"
        echo "Usage: rem name"
        exit 1
fi

name=$1

#
# Find number of matching entries
#

matches=$(grep "$name" $PHONEBOOK | wc -l)

#
# If more than one match, issue message, else remove it
#

if [ "$matches" -gt 1 ]
then
        echo "More than one match; please qualify further"
elif [ "$matches" -eq 1 ]
then
        grep -v "$name" $PHONEBOOK > /tmp/phonebook
        mv /tmp/phonebook $PHONEBOOK
else
        echo "I couldn't find $name in the phone book"
fi
THE-END-OF-DATA
$
```

To be complete, this archive would include **rolo** as well, but we didn’t include it here to conserve space in the book.

This shell archive offers one portable file, **rolosubs**, that contains the source for all three programs **lu**, **add**, and **rem**, and can be sent to someone else using `mail`:

```text
$ mail tony@aisystems.com < rolosubs          Mail the archive
$ mail tony@aisystems.com                      Mail tony a message
Tony,

        I mailed you a shell archive containing the programs
        lu, add, and rem. rolo itself will be sent along shortly.
Pat
Ctrl+d
$
```

When tony receives the file in his mail, she can extract the three programs by saving the message, then running the shell on the file (after having first removed any email header lines that might have ended up in the beginning of the file):
