The shell fed every line typed into the shell as the standard input stream of wc until encoun-	ered line containing ENDOFDATA.

In-line input redirection—also referred to as here documents by some programmers—is a
powerful feature when used inside shell programs. It lets you specify the standard input to a
command directly in the program, obviating the need to write it into a separate file, or to
echo to get it into the standard input of the command.

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
END-OF-DATA$\$
```

To send this message to all members of the group as stored in the file users_list, you could
invoice

```
mailmsg $(cat users_list)
```

The shell performs parameter substitution for the redirected input data, executes back-quoted
commands, and recognizes the backslash character.

Special characters within a here document are generally ignored, but if you use dollar signs,
back quotes, or backslashes in these lines, they can be interpreted. To have them ignored,
precede them with a backslash character. Alternatively, if you want the shell to leave all input
lines completely untouched, the end of document word that follows the << with a
backslash.

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