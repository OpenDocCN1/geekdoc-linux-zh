# More on Subshells 231

After this statement is executed, db will be replaced by /bin/sh. This means that it would now be pointless to have any commands follow the exec because they will never be executed.

exec can also be used to use standard input and reopen it with any file that you want to read. To change standard input to infile, for example, use the exec command in the form exec < infile

Any commands that subsequently read data from standard input will read from infile. Redirection of standard output is done similarly. The command exec > report

redirects all subsequent output written to the file report. Note in both of the previous examples that exec is not used to start execution of a new program, just to reassign standard input or standard output.

If you use exec to reassign standard input and later want to reassign it elsewhere, you can simply invoke exec again. To reassign standard input back to the terminal, you would write exec < /dev/tty

The concept also allows for reassignment of standard output.

# The (...) and { ...; } Constructs

Sometimes you want to group a set of commands together. For example, you may want to push a sort followed by your plotdata program into the background. Not connected with a pipe; just two commands after the other.

It turns out that you can group a set of commands together by enclosing them in parentheses or braces. The first form causes the commands to be executed by a subshell, the latter form by the current shell.

Here are some examples to illustrate how they work:

```
$ x=50
$(x=100)
$ echo $x
50
{ x=100; }
$ echo $x
100
$ pwd
/users/steve
$(cd bin; ls)
add
greings
lu
number
```

Execute in this subshell

Didn't change
Execute in the current shell

Where am I?

Change to bin and do an ls