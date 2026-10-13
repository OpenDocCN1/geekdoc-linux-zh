
Notice that if the file already exists, the echo command that prompts for the yes/no response is executed. The read command that follows causes the shell to wait for the user to type a response. What this shows is that the shell doesn’t prompt the user when it’s waiting for data; it’s up to the programmer to add a useful prompt to the program.

The data that is typed is stored in the variable answer and is then tested against the characters yes to determine whether the copy process should proceed. The quotes around the reference to the variable answer in the test

```
[ "$answer" != yes ]
```

are necessary in case the user just presses the Enter key without typing any data. In that case, the shell would store a null value in answer and, without the quotes, test would issue an error message.

Also note the use of the semicolon to move the then statements onto the same line as the if statement. This is a common shell programmer notational trick, as mentioned in the previous chapter.

## Special echo Escape Characters

A slight annoyance with mycp is that after the echo command is run, the response typed by the user appears on the next line. This happens because the echo command automatically adds a terminating newline character after the last argument.

Fortunately, this can be suppressed if the last two characters given to echo are the special escape characters `\c`. This tells echo to omit the newline after displaying the last argument. If you changed the echo command in mycp to read like this:

```
echo "$to already exists; overwrite (yes/no)? \c"
```

The user’s input would be typed right after the message on the same line. Bear in mind that the `\c` is interpreted by echo and not by the shell, meaning that it must be quoted so that the backslash makes it to echo.

> **Note**
>
> Some Linux and Mac OS X systems have shells that don’t interpret these echo escape characters, so the above would be shown as
>
> `newfile.txt already exists; overwrite (yes/no)? \c`
>
> If testing reveals that your shell works like that, change those specific invocations of echo to the separate program `/bin/echo` and they’ll work fine. All your other echo statements can remain as just regular echo commands, of course.

The echo command can also interpret other special characters (see note if yours doesn’t work as expected). These must each be preceded by a backslash and are summarized in Table 9.1.

**Table 9.1** *echo* **Escape Characters**

| Character | Prints |
|---|---|
| `\b` | Backspace |
| `\c` | The line without a terminating newline |
| `\f` | Formfeed |
| `\n` | Newline |
| `\r` | Carriage return |
| `\t` | Tab character |
| `\\` | Backslash character |
| `\0nnn` | The character whose ASCII value is *nnn*, where *nnn* is a one- to three-digit octal number |

## An Improved Version of `mycp`

Suppose that you have a program called `prog1` in your current directory and you want to copy it into your bin directory. With the regular `cp` program, you could use the shortcut of just specifying the destination directory to have the file copied there with its existing filename. But take another look at the `mycp` program and determine what happens if you type in

```
mycp prog1 bin
```

The `-e` test on `bin` will succeed (because `-e` tests for existence of a file), and `mycp` will display the "already exists" message and wait for a yes/no answer. That’s a dangerous mistake, particularly if the user types yes!

If the second argument is a *directory*, `mycp` should instead check to see whether the `from` file exists *inside* the specified directory.

The next version of `mycp` performs this check. It also has the modified `echo` command that includes the `\c` to suppress the terminating newline.

```sh
$ cat mycp
#
# Copy a file -- version 2

if [ "$#" -ne 2 ] ; then
        echo "Usage: mycp from to"
        exit 1
fi

from="$1"
to="$2"

#
# See if destination file is a directory
#

if [ -d "$to" ] ; then
        to="$to/$(basename $from)"
fi

#
# See if the destination file already exists
#

if [ -e "$to" ] ; then
        echo "$to already exists; overwrite (yes/no)? \c"
        read answer

        if [ "$answer" != yes ] ; then
                echo "Copy not performed"
                exit 0
        fi
fi
#
# Either destination doesn't exist or "yes" was typed
#

cp $from $to        # proceed with the copy
$
```

If the destination file is a directory, the program changes the variable `to` to more precisely identify the destination filename by including the directory name: `$to/$(basename $from)`. This ensures that the subsequent test for the existence of the ordinary file `$to` will be done on the file in the directory, not on the directory itself.

The basename command gives the basename of its argument with all directory components stripped away (for example, `/usr/bin/troff` produces `troff`; basename `troff` also produces `troff`). This extra step ensures that the copy is made from and to the correct place. (As an example, if `mycp /tmp/data bin` is typed, where `bin` is a directory, you want to copy `/tmp/data` into `bin/data` and not into `bin/tmp/data`.)

Here’s some sample output. Note the effect of the `\c` escape characters.

```text
$ ls                 Check out current directory
bin
prog1
$ ls bin             Look inside bin
lu
nu
prog1
```

```sh
$ mycp prog1 prog2    Simple case
$ mycp prog1 bin      Copy into directory
bin/prog1 already exists; overwrite (yes/no)? yes
$
```

## A Final Version of `mycp`

The last modification to mycp makes the program virtually equivalent to the standard Linux cp command by allowing a variable number of arguments. Recall that with the standard command any number of files can precede the name of a directory, as in

```sh
cp prog1 prog2 greetings bin
```

To modify mycp to accept any number of files in a similar format, you can use this approach:

1. Get each argument but the last from the command line and store it in the shell variable `filelist`.
2. Store the last argument in the variable `to`.
3. If `$to` is not a directory, test the argument count as there must be exactly two arguments.
4. If `$to` is a directory, for each file in `$filelist`, check whether the file already exists in the destination directory. If it doesn’t, add the filename to the variable `copylist`. If it does exist, ask the user whether the file should be overwritten. If the answer is yes, add the filename to `copylist`.
5. If `copylist` is non-null, copy the files in it to `$to`.

If this algorithm seems a bit fuzzy, the program and a detailed explanation will help clear things up. Note the modified command usage message.

```sh
$ cat mycp
#
# Copy a file -- final version
#

numargs=$#                 # save this for later use
filelist=
copylist=

#
# Process the arguments, storing all but the last in filelist
#

while [ "$#" -gt 1 ] ; do
        filelist="$filelist $1"
        shift

done
to="$1"

#
# If less than two args, or if more than two args and last arg
# is not a directory, then issue an error message
#

if [ "$numargs" -lt 2 -o "$numargs" -gt 2 -a ! -d "$to" ] ; then
    echo "Usage: mycp file1 file2"
    echo "       mycp file(s) dir"
    exit 1
fi

#
# Sequence through each file in filelist
#

for from in $filelist ; do
    #
    # See if destination file is a directory
    #

    if [ -d "$to" ] ; then
        tofile="$to/$(basename $from)"
    else
        tofile="$to"
    fi

    #
    # Add file to copylist if file doesn't already exist
    # or if user says it's okay to overwrite
    #

    if [ -e "$tofile" ] ; then
        echo "$tofile already exists; overwrite (yes/no)? \c"
        read answer

        if [ "$answer" = yes ] ; then
            copylist="$copylist $from"
        fi
    else
        copylist="$copylist $from"
    fi
done

#
# Now do the copy -- first make sure there's something to copy
#
if [ -n "$copylist" ] ; then
        cp $copylist $to        # proceed with the copy
fi
$
```

Let’s look at some sample output before delving into the code itself.

```
$ ls -C
bin        lu        names        prog1
prog2
```

See what’s around

```
$ ls bin
lu
nu
prog1
```

And what’s in bin?

```
$ mycp
Usage: mycp file1 file2
       mycp file(s) dir
```

No arguments

```
$ mycp names prog1 prog2
Usage: mycp file1 file2
       mycp file(s) dir
```

Last arg isn’t a directory

```
$ mycp names prog1 prog2 lu bin
bin/prog1 already exists; overwrite (yes/no)? yes
bin/lu already exists; overwrite (yes/no)? no
```

Legitimate use

```
$ ls -l bin
total 5
-rw-r--r--   1 steve   steve   543 Jul 19 14:10 lu
-rw-r--r--   1 steve   steve   949 Jul 21 17:11 names
-rw-r--r--   1 steve   steve    38 Jul 19 09:55 nu
-rw-r--r--   1 steve   steve   498 Jul 21 17:11 prog1
-rw-r--r--   1 steve   steve   498 Jul 21 17:11 prog2
$
```

See what happened

In the last case, `prog1` was overwritten and `lu` wasn’t, as per the user’s request.

When the program starts execution, it saves the number of arguments in the variable `numargs`. This is done because the argument variables are changed later in the program by the `shift` command.

Next a loop is entered that is executed as long as the number of arguments is greater than one. The purpose of this loop is to get the last argument on the line. While doing this, the loop stashes away the other arguments into the shell variable `filelist`, which ultimately will contain a list of all the files to be copied. The statement

```sh
filelist="$filelist $1"
```
