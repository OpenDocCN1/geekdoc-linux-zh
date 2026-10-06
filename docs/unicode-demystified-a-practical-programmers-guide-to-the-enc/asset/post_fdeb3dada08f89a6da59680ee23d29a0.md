
$ cat temp
The second sentence.
This is sentence four.
This is sentence seventh.

The following is a Bourne Shell script sub that changes all occurrences of REPORT to report, FILE to file, and PROCESS in a group of files. The For structure loops through the list of files supplied on the command line. (See page 640 for more information on the For structure.) As it processes each file, sub displays the filename before running sed on file. This script uses a multiline embedded sed instruction; as long as the NEW within the instruction are quoted (that is, placed between single quotation marks), sed accepts the multiline instruction as though it appeared on a single line. Each Substitute instruction includes a g (global) flag to take care of the case in which one of the strings occurs more than one time on a line:

```
$ cat sub
for file
echo $file
mv $file $$.subhld
sed 's/REPORT/report/g
s/FILE/file/g
s/PROCESS/process/g' $$.subhld > $file
done
rm $$.subhld
```

```
$ sub file1 file2 file3
file1
file2
file3
```

Following, sed uses the Write instruction to copy part of a file to another file (temp2). The line numbers 2 and 4, separated by a comma, select the range of lines sed is to copy. This script does not alter the lines:

```
$ cat write_demo2
2,4 temp2
```

```
$ sed -n -f write_demo2 new
```

```
$ cat temp2
The second line.
The third.
This is line four.
```

The script write_demo3 is very similar to write_demo2 but precedes the Write instruction with the NOT operator (!), causing sed to write to the file lines not selected by the address:

# 1318 sed

```
$ cat write_demo3
2,4 !temp3
```

```
$ sed -n -f write_demo3 new
```

```
$ cat temp3
Line one.
Five.
This is the sixth sentence.
This is line seven.
Eighth and last.
```

Following, next_demo1 demonstrates the Next instruction. When it processes the selected line (line 3), sed immediately starts processing the next line without printing line 3 and does not display line 3:

```
$ cat next_demo
3 n
p
```

```
$ sed -n -f next_demo new
Line one.
The second line.
This is line four.
Five.
This is the sixth sentence.
This is line seven.
Eighth and last.
```

The next example uses a textual address. The sixth line contains the string, so the Next instruction causes sed not to display it:

```
$ cat next_demo2
/the/ n
p
```

```
$ sed -n -f next_demo2 new
Line one.
The second line.
The third.
This is line four.
Five.
This is line seventh.
Eighth and last.
```

The next set of examples uses the file compound.in to demonstrate how sed instructions work together:

```
$ cat compound.in
1. The words on this page...
2. The words on this page...
3. The words on this page...
4. The words on this page...
```

The first example that uses compound.in instructs sed to substitute the string words with text on lines 1, 2, and 3 and the string text with TEXT on lines 2, 3, and 4. The example also selects and deletes line 3. The result is text on line 1, TEXT on line 2, no line 3, and words on line 4. The sed made two substitutions on lines 2 and 3: for words and for text. Then sed deleted line 3:

```
$ cat compound
1,3 s/words/text/
2,4 s/text/TEXT/
3 d
```

```
$ sed -f compound.in
1. The text on this page...
2. The TEXT on this page...
4. The words on this page...
```

The next example shows that the ordering of instructions within a sed script is critical. Both Substitute instructions are applied to the second line, as in the pre-example, but the order in which the substitutions occurs change the result:

```
$ cat compound2
2,4 s/text/TEXT/
1,3 s/words/text/
3 d
```

```
$ sed -f compound2.in
1. The text on this page...
2. The text on this page...
4. The words on this page...
```

Next, compound3 appends two lines to line 2. The sed utility displays all the lines from the file once, because no -n option appears on the command line. The Print instruction at the end of the script displays line 3 an additional time:

```
$ cat compound3
2 a\nThis is line 2a.\nThis is line 2b.
3 p
```

```
$ sed -f compound3 compound.in
1. The words on this page...
2. The words on this page...
This is line 2a.
This is line 2b.
3. The words on this page...
3. The words on this page...
4. The words on this page...
```

The next example shows that sed always displays appended text. Here line 2 is deleted, but the Append instruction still displays the two lines that were appended to it. Appended lines are displayed if you use the -n option on the command line:

```
$ cat compound4
2 a\
This is line 2a.\
This is line 2b.
2 d
```

```
$ sed -f compound4 compound.in
1. The words on this page...
This is line 2a.
This is line 2b.
3. The words on this page...
4. The words on this page...
```

The final examples use regular expression in addresses. The regular expression
in the following instruction ("^") matches one character at the beginning of a line
(that is, it matches every line that is not empty). The replacement string between
the second and third slashes contains a TAB character followed by an ampersand
(&). The ampersand takes on the value of whatever the regular expression matched:

```
$ sed 's/^/ /&' new
Line one.
The second line.
The third.
```

This type of substitution is useful for indenting a file to create a left margin.
Appendix A for more information on regular expressions.

You may want to put the preceding sed instruction into a shell script so that
you do not have to remember it (and retype it) every time you want to indent a file:

```
$ cat indent
sed 's/^/ /&' $*
$ chmod u+x indent
$ indent new
Line one.
The second line.
The third.
```

When you create a sed instruction that you think you may want to use again, it is
generally a good idea to put it into a shell script or a script-file to save yourself the effort to reconstruct it.

In the following shell script, the regular expression (two SPACES followed by an
*) matches one or more spaces at the end of a line. This script removes trailing
spaces at the end of a line, which is useful for cleaning up files that you created using vi:

```
$ cat cleanup
sed 's/ *//' $*
```

# ssh

Securely executes commands on a remote computer

ssh [option]|[user@host] [command line]

The ssh utility runs command line on host by starting a shell on the remote system. Without a command
line ssh logs you in to the remote computer.

The ssh utility, which can replace rsh and login, provides secure encrypted communications
between two machines on an insecure network. For more information, refer to “ssh: Logs in or
Runs a Command on a Remote Computer” on page 374.

![](img/aa8214d49e1cf50152c432845129fb3b_1370_0.png)

Arguments The host is the machine that you want to log in or run a command on. Unless you
have one of several kinds of authentication established, ssh prompts for a user
name and password for the remote system. When ssh is able to log in automatically,
it logs in as the user running the ssh command or as if user@ is present on the ssh
command line.

The command line runs on the remote system. Without command line, ssh logs you in
to the remote system. You must quote special characters in command line if you do not
want them expanded by the local shell prior to passing them to ssh.

# Options

-l login-name If your login name on the remote computer is different from your local login name,
can you use this option to give the remote login name. This is an alternative to using
user@ on the command line.

-l login-name -t Allocates a pseudo tt to the ssh process on the remote machine. Without
this option, when you run a command on a remote system using ssh, ssh does not
allocate a tt (terminal) to the process. Instead, ssh attaches input and
standard output of the remote process to the ssh session: normally, but not always,
what you want. This option forces ssh to allocate a tty on the remote machine so
that programs that require a tty work.

# Notes

Refer to “ssh: Logs in or Runs a Command on a Remote Computer” on page 374
for more information on ssh. See also the optional section on page 375 for an ex-
ample of how to use ssh to create a VPN by tunneling.
