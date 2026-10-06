
The shell fed every line typed into the shell as the standard input stream of wc until encountered line containing ENDOFDATA.

In-line input redirection—also referred to as here documents by some programmers—is a powerful feature when used inside shell programs. It lets you specify the standard input to a command directly in the program, obviating the need to write it into a separate file, or to echo to get it into the standard input of the command.

Here’s a common example of how this feature is used within a shell program:

```
$ cat mailag
mail * <<END-OF-DATA
```

Attention:

Our monthly users group meeting
will take place on Friday, March 4, 2016 at
8pm in Room 1A-308. Please try to attend.

```
END-OF-DATA$$
```

To send this message to all members of the group as stored in the file users_list, you could invoice

```
mailmsg $(cat users_list)
```

The shell performs parameter substitution for the redirected input data, executes back-quoted commands, and recognizes the backslash character.

Special characters within a here document are generally ignored, but if you use dollar signs, back quotes, or backslashes in these lines, they can be interpreted. To have them ignored, precede them with a backslash character. Alternatively, if you want the shell to leave all input lines completely untouched, the end of document word that follows the << with a backslash.

Let’s highlight the difference between the two:

```
$ cat <<FOOBAR
> $HOME
> ******
> \foobar
> `date
> FOOBAR Terminates the file
/users/steve
*****
$foobar
Wed Oct 2 15:23:15 EDT 2002
$
```

## Chapter 12 Loose Ends

Since the shell supplies all the lines up to FOOBAR as the input to cat, it substitutes the value for HOME not for foobar; the latter is prefaced with a backslash. The date command is also executed because back quotes are interpreted by the shell.

To avoid all with the shell interpreting the contents of the lines, use backslash the end-of-document word instead:

```
$ cat <<FOOBAR
 > "date"
> $HOME
> FOOBAR
> \\
> "date"
> $HOME
$
```

Use care when selecting the word that follows the <<. Generally, just make sure that it's weird enough so that the chances of it accidentally appearing in the subsequent lines of data are minicule.

You now know about the << sequence, but there's another that most modern shells understand: if the first character that follows the << is a dash (-), any leading tab characters in the input will be removed by the shell. This is useful for visually indenting the lines of data for readability while having it appear in normal left-aligned form:

```
$ cat <<END
> Indented lines
> because tabs are cool
> END
```

Indented lines
because tabs are cool
$

## Shell Archives

One of the best uses of the in-line input redirection feature is for creating shell archive files. With this technique, one or more related programs can be put into a single file and then sent to someone else using standard Unix mail commands. When the archive is received, it can be "unpacked" by invoking it as a shell program.

For example, here's an archived version of the lu, add, and rem programs used by rolo:

```
$ cat rolonubs
#
# Archived programs used by rolo.
#
```

echo Extracting lu

```
cat >lu \THE-END-OF-DATA
#
# Look someone up in the phone book
#

if [ "$# -ne 1 ];
then
    echo "Incorrect number of arguments"
    echo "Usage: lu name"
    exit 1
fi

name=$1
grep $name $PHONEBOOK

if [ $? -ne 0 ];
then
    echo "I couldn't find name in the phone book"
fi
THE-END-OF-DATA

echo Extracting add
cat >add \THE-END-OF-DATA
#
# Program to add someone to the phone file
#

if [ "$# -ne 2 ];
then
    echo "Incorrect number of arguments"
    echo "Usage: add name number"
    exit 1
fi

echo $1 $2 >> $PHONEBOOK
sort -o $PHONEBOOK $PHONEBOOK
THE-END-OF-DATA

echo Extracting rem
cat >rem \THE-END-OF-DATA
#
# Remove someone from the phone book
#

if [ "$# -ne 1 ];
then
    echo "Incorrect number of arguments"
```

## Chapter 12 Loose Ends

```
echo "Usage: rem name"
exit 1
fi
```

name=$1

```
#
# Find number of matching entries
#
```

```
matches=$(grep "$name" $PHONEBOOK | wc -l)

#
# If more than one match, issue message, else remove it
#
```

```
if [ "$matches" -gt 1 ]
then
  echo "More than one match; please qualify further"
elif [ "$matches" -eq 1 ]
then
  grep -v "$name" $PHONEBOOK > /tmp/phonebook
mv /tmp/phonebook $PHONEBOOK
fi
echo "I couldn't find name in the phone book"
```

if [ "$matches" -gt 1 ]
then
  echo "More than one match; please qualify further"
elif [ "$matches" -eq 1 ]
then
  grep -v "$name" $PHONEBOOK > /tmp/phonebook
mv /tmp/phonebook $PHONEBOOK
fi

echo "I couldn't find name in the phone book"
THE-END-OF-DATA

To send this message to all members of the group as stored in the file users_list, you could invoice

```
mailmsg $(cat users_list)
```

The shell performs parameter substitution for the redirected input data, executes back-quoted commands, and recognizes the backslash character.

Special characters within a here document are generally ignored, but if you use dollar signs, back quotes, or backslashes in these lines, they can be interpreted. To have them ignored, precede them with a backslash character. Alternatively, if you want the shell to leave all input lines completely untouched, the end of document word that follows the << with a backslash.

Let’s highlight the difference between the two:

```
$ cat <<FOOBAR
> $HOME
> ******
> \foobar
> `date
> FOOBAR Terminates the file
/users/steve
*****
$foobar
Wed Oct 2 15:23:15 EDT 2002
$
```

## Chapter 12 Loose Ends

Since the shell supplies all the lines up to FOOBAR as the input to cat, it substitutes the value for HOME not for foobar; the latter is prefaced with a backslash. The date command is also executed because back quotes are interpreted by the shell.

To avoid all with the shell interpreting the contents of the lines, use backslash the end-of-document word instead:

```
$ cat <<FOOBAR
 > "date"
> $HOME
> FOOBAR
> \\
> "date"
> $HOME
$
```

Use care when selecting the word that follows the <<. Generally, just make sure that it's weird enough so that the chances of it accidentally appearing in the subsequent lines of data are minicule.

You now know about the << sequence, but there's another that most modern shells understand: if the first character that follows the << is a dash (-), any leading tab characters in the input will be removed by the shell. This is useful for visually indenting the lines of data for readability while having it appear in normal left-aligned form:

```
$ cat <<END
> Indented lines
> because tabs are cool
> END
```

Indented lines
because tabs are cool
$

## Shell Archives

One of the best uses of the in-line input redirection feature is for creating shell archive files. With this technique, one or more related programs can be put into a single file and then sent to someone else using standard Unix mail commands. When the archive is received, it can be "unpacked" by invoking it as a shell program.

For example, here's an archived version of the lu, add, and rem programs used by rolo:

```
$ cat rolonubs
#
# Archived programs used by rolo.
#
```

echo Extracting lu

```
cat >lu \THE-END-OF-DATA
#
# Look someone up in the phone book
#

if [ "$# -ne 1 ];
then
    echo "Incorrect number of arguments"
    echo "Usage: lu name"
    exit 1
fi

name=$1
grep $name $PHONEBOOK

if [ $? -ne 0 ];
then
    echo "I couldn't find name in the phone book"
fi
THE-END-OF-DATA

echo Extracting add
cat >add \THE-END-OF-DATA
#
# Program to add someone to the phone file
#

if [ "$# -ne 2 ];
then
    echo "Incorrect number of arguments"
    echo "Usage: add name number"
    exit 1
fi

echo $1 $2 >> $PHONEBOOK
sort -o $PHONEBOOK $PHONEBOOK
THE-END-OF-DATA

echo Extracting rem
cat >rem \THE-END-OF-DATA
#
# Remove someone from the phone book
#

if [ "$# -ne 1 ];
then
    echo "Incorrect number of arguments"
```

## Chapter 12 Loose Ends

```
echo "Usage: rem name"
exit 1
fi
```

name=$1

```
#
# Find number of matching entries
#
```

```
matches=$(grep "$name" $PHONEBOOK | wc -l)

#
# If more than one match, issue message, else remove it
#
```

```
if [ "$matches" -gt 1 ]
then
  echo "More than one match; please qualify further"
elif [ "$matches" -eq 1 ]
then
  grep -v "$name" $PHONEBOOK > /tmp/phonebook
mv /tmp/phonebook $PHONEBOOK
fi
```

## Functions

Modern shells support functions—long or short sequences of commands that can be referenced or reused often.

To define a function, you use the general format:

```
name () ... command; }
```

where name is the name of the function, the parentheses denote that a function is being defined, and the commands enclosed between curly braces define the body of the function. These commands will be executed whenever the function is executed.

Note that at least one whitespace character must separate the ( from the first command, and a semicolon must separate the last command from the closing brace if they occur on the same line.

The following defines a function called nu that displays the number of logged-in users:

```
nu () { wc -l; }
```

You execute a function the same way you execute an ordinary command: by typing its name into the shell:

```
$ nu
```

```
22
```

Functions are really useful for shell programmers and can alleviate lots of tedium in developing solutions. One key feature: arguments after the function on the command line are assigned to the positional parameters $1, $2, ..., within the function, just as with any other command.

Here's a function called nrrun that runs tbl, nroff, and lp on the file specified:

```
$ nrrun () { tbl $1 | nroff -mm -tlp | lp; }
$ nrrun memo  Run it in memo
```

request id is laser1-33 (standard input)

```
$
```

Functions exist only in the shell in which they are defined so can't be passed to subshells. Because the function is executed in the current shell, changes made to the current directory or to the variables remain after the function has completed execution, as if it had been invoked with the . command explored earlier in the book:

```
$ db () {
```

```
> PATH=$PATH:/uxn2/data
> PS1=DB:
> cd /uxn2/data
 }
```

```
$ db
```

Execute it

DB:
