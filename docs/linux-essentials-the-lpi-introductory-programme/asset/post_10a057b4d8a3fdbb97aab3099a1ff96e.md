
### Table 9.2: Key Strokes within bash

| Key Stroke | Function |
| :--- | :--- |
| ↑ or ↓ | Scroll through most recent commands |
| Ctrl + r | Search command history |
| ← or → | Move cursor within current command line |
| Home or Ctrl + a | Jump to the beginning of the command line |
| End or Ctrl + e | Jump to the end of the command line |
| ← or Del | Delete character in front of/under the cursor, respectively |
| Ctrl + u | Swap the two characters in front of and under the cursor |
| Ctrl + l | Clear the screen |
| Ctrl + c | Interrupt a command |
| Ctrl + d | End the input (for login shells: log off) |

### Conditional Execution

Sometimes it is useful to make the execution of the second command depend on whether the first was executed correctly or not. Every Unix process yields a return value which states whether it was executed correctly or whether errors of whatever kind have occurred. In the former case, the return value is 0; in the latter, it is different from 0.

You can find the return value of a child process of your shell by looking at the `$?` variable:

```bash
$ bash
$ exit 33
exit
$ echo $?
33
$ _
```

Start a child shell ...  
... and exit again immediately  
The value from our exit above

But this really has no bearing on the following.

With `&&` as the “separator” between two commands (where there would otherwise be the semicolon), the second command is only executed when the first has exited successfully. To demonstrate this, we use the shell’s `-c` option, with which you can pass a command to the child shell on the command line (impressive, isn’t it?):

```bash
$ bash -c "exit 0" && echo "Successful"
Successful
$ bash -c "exit 33" && echo "Successful"
Nothing — 33 isn’t success!
```

Conversely, with `||` as the “separator”, the second command is only executed if the first did not finish successfully:

```bash
$ bash -c "exit 0" || echo "Unsuccessful"
$ bash -c "exit 33" || echo "Unsuccessful"
Unsuccessful
```

# Exercises

- **9.8 [3]** What is wrong about the command “echo “He\lo!””? (Hint: Experiment with commands of the form “\1.*2” or “\1s*.”)

## 9.5 Commands From A File

You can store shell commands in a file and execute *en bloc*. (You will learn how to create a file conveniently in Chapter 3.) You just need to invoke the shell and pass the file name as a parameter:

```bash
$ bash my-commands
```

Such a file is also called a **shell script**, and the shell has extensive programming features that we can only outline very briefly here. (The Linup Front training manual *Advanced Linux* explains shell programming in great detail.)

💡 You can avoid having to prepend the *bash* command by inserting the magical incantation

```bash
#!/bin/bash
```

as the first line of your file and making the file “executable”:

```bash
$ chmod +x my-commands
```

(You will find out more about `chmod` and access rights in Chapter 14.) After this, the

```bash
$ ./my-commands
```

command will suffice.

If you invoke a shell script as above, whether with a prepended *bash* or as an executable file, it is executed in a *subshell*, a shell that is a child process of the current shell. This means that changes to, *e.g.*, shell or environment variables do not influence the current shell. For example, assume that the file *assignment* contains the line

```bash
foo=bar
```

Consider the following command sequence:

```bash
$ foo=quux
$ bash assignment          # Contains foo=bar
$ echo $foo
quux                       # No change; assignment was only in subshell
```

This is generally considered a feature, but every now and then it would be quite desirable to have commands from a file affect the *current* shell. That works, too: The *source* command reads the lines in a file exactly as if you would type them directly into the current shell—all changes to variables (among other things) hence take effect in your current shell:

```bash
$ foo=quux
$ source assignment        # Contains foo=bar
$ echo $foo
bar                        # Variable was changed!
```

A different name for the *source* command, by the way, is `.` (You read correctly – dot!) Hence

```bash
$ source assignment
```

is equivalent to

```bash
$ . assignment
```

Like program files for external commands, the files to be read using source or `.` are searched in the directories given by the PATH variable.

## 9.6 The Shell As A Programming Language

Being able to execute shell commands from a file is a good thing, to be sure. However, it is even better to be able to structure these shell commands such that they do not have to do the same thing every time, but---for example---can obtain command-line parameters. The advantages are obvious: In often-used procedures you save a lot of tedious typing, and in seldom-used procedures you can avoid mistakes that might creep in because you accidentally leave out some important step. We do not have space here for a full explanation of the shell as a programming language, but fortunately there is enough room for a few brief examples.

**Command-line parameters**  
When you pass command-line parameters to a shell script, the shell makes them available in the variables $1, $2, .... Consider the following example:

```bash
$ cat hello
#!/bin/bash
echo Hello $1, are you free $2?
$ ./hello Joe today
Hello Joe, are you free today?
$ ./hello Sue tomorrow
Hello Sue, are you free tomorrow?
```

The `$*` contains all parameters at once, and the number of parameters is in `$#`:

```bash
$ cat parameter
#!/bin/bash
echo $# parameters: $*
$ ./parameter
0 parameters:
$ ./parameter dog
1 parameters: dog
$ ./parameter dog cat mouse tree
4 parameters: dog cat mouse tree
```

**Loops**  
The for command lets you construct loops that iterate over a list of words (separated by white space):

```bash
$ for i in 1 2 3
> do
>     echo And $i!
> done
And 1!
And 2!
And 3!
```

Here, the `i` variable assumes each of the listed values in turn as the commands between `do` and `done` are executed.

This is even more fun if the words are taken from a variable:

```bash
$ list='4 5 6'
$ for i in $list
> do
>     echo And $i!
> done
And 4!
And 5!
And 6!
```

If you omit the “in ...”, the loop iterates over the command line parameters:

```bash
$ cat sort-wc
#!/bin/bash
# Sort files according to their line count
for f
do
    echo `wc -l <$f` lines in $f
done | sort -n
$ ./sort-wc /etc/passwd /etc/fstab /etc/motd
```

(The "wc -l" command counts the lines of its standard input or the file(s) passed on the command line.) Do note that you can redirect the standard output of a loop to `sort` using a pipeline!

### Alternatives

You can use the aforementioned `&&` and `||` operators to execute certain commands only under specific circumstances. The

```bash
#!/bin/bash
# grepqp REGEX
rm -rf backup; mkdir backup
for f in *.txt
do
    grep $1 "$f" && cp "$f" backup
done
```

script, for example, copies a file to the backup directory only if its name ends with .txt (the for loop ensures this) and which contain at least one line matching the regular expression that is passed as a parameter.

A useful tool for alternatives is the `test` command, which can check a large variety of conditions. It returns an exit code of 0 (success), if the condition holds, else a non-zero exit code (failure). For example, consider

```bash
#!/bin/bash
# filetest NAME1 NAME2 ...
for name
do
    test -d "$name" && echo $name: directory
    test -f "$name" && echo $name: file
    test -L "$name" && echo $name: symbolic link
done
```

This script looks at a number of file names passed as parameters and outputs for each one whether it refers to a directory, a (plain) file, or a symbolic link.

> ⚠ The test command exists both as a free-standing program in `/bin/test` and as a built-in command in bash and other shells. These variants can differ subtly especially as far as more outlandish tests are concerned. If in doubt, read the documentation.

### if

You can use the `if` command to make more than one command depend on a condition (in a convenient and readable fashion). You may write `[...]` instead of `"test ..."`:

```bash
#!/bin/bash
# filetest2 NAME1 NAME2 ...
for name
do
    if [ -L "$name" ]
    then
        echo $name: symbolic link
    elif [ -d "$name" ]
    then
        echo $name: directory
    elif [ -f "$name" ]
    then
        echo $name: file
    else
        echo $name: no idea
    fi
done
```

If the command after the `if` signals “success” (exit code 0), the commands after `then` will be executed, up to the next `elif`, `else`, or `fi`. If on the other hand it signals “failure”, the command after the next `elif` will be evaluated next and its exit code will be considered. The shell continues the pattern until the matching `fi` is reached. Commands after the `else` are executed if none of the `if` or `elif` commands resulted in “success”. The `elif` and `else` branches may be omitted if they are not required.

**More loops**  
With the `for` loop, the number of trips through the loop is fixed at the beginning (the number of words in the list). However, we often need to deal with situations where it is not clear at the beginning how often a loop should be executed. To handle this, the shell offers the `while` loop, which (like `if`) executes a command whose success or failure determines what to do about the loop: On success, the “dependent” commands will be executed, on failure execution will continue after the loop.

The following script reads a file like

```text
Aunt Maggie:maggie@example.net:the delightful tea cosy
Uncle Bob:bob@example.com:the great football
```

(whose name is passed on the command line) and constructs a thank-you e-mail message from each line (Linux is very useful in daily life):

```bash
#!/bin/bash
# birthday FILE
IFS=:
while read name email present
do

    (echo $name
    echo ""
    echo "Thank you very much for $present!"
    echo "I enjoyed it very much."
    echo ""
    echo "Best wishes"
    echo "Tim") | mail -s "Many thanks!" $email
done <$1
```

**read**  
The `read` command reads the input file line by line and splits each line at the colons
