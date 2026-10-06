There's still one subtle problem with this script though. The script always reads the next line of text into the pattern space before executing the sed commands. When it reaches the last line of text, there isn't a line of text to read, so the N command causes the sed editor to stop. If the matching test is on last line in the data stream, the commands won't catch the matching data:

```
$ cat data4
The first meeting of the Linux System
Administrator's group will be held on Tuesday.
All System Administrators should attend this meeting.
$ sed '
> s/System\nAdministrator/Desktop\nUser/
> s/System Administrator/Desktop User/
> data4
The first meeting of the Linux Desktop
User's group will be held on Tuesday.
All System Administrators should attend this meeting.
$
```

Since the System Administrator appears in the last line of the data stream, the N command misses it, as there isn't another line to read into the pattern space to combine. You can easily resolve this by moving your single-line commands before the N command and having only the multiline commands after the N command, like this:

```
$ sed '
> s/System Administrator/Desktop User/
> s/System\nAdministrator/Desktop\nUser/
> data4
The first meeting of the Linux Desktop
User's group will be held on Tuesday.
All Desktop Users should attend this meeting.
$
```

Now, the substitution command that looks for the phrase in a single line works just fine on the last line in the data stream, and the multiline substitution command covers the occurrence in the middle of the data stream.

# The multiline delete command

Chapter 16 introduced the single-line delete command (d). The sed editor uses it to delete the current line in the pattern space. When working with the N command though, you must be careful when using the single-line delete command:

```
$ sed '
> N
```