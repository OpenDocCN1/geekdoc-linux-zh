
```bash
$ cat ~/.bash_profile
if [ -f ~/.bashrc ]; then
    . ~/.bashrc                          # Read local startup file if it exists
fi
PATH=$PATH:/usr/local/bin               # Add /usr/local/bin to PATH
export PS1='\h \w \u\$'
```

The first command in the preceding **.bash_profile** file executes the commands in the user’s .bashrc file if it exists. The next command adds to the PATH variable (page 359). Typically PATH is set and exported in /etc/profile, so it does not need to be exported in a user’s startup file. The final command sets and exports PS1 (page 361), which controls the user’s prompt.

The first command in the .bashrc file shown below executes the commands in the /etc/bashrc file if it exists. Next the file sets noclobber (page 156), unsets MAILCHECK (page 361), exports LANG (page 366) and viminit (for vim initialization), and defines several aliases. The final command defines a function (page 396) that swaps the names of two files.

```bash
$ cat ~/.bashrc
if [ -f /etc/bashrc ]; then
    source /etc/bashrc                  # read global startup file if it exists
fi

set -o noclobber                        # prevent overwriting files
unset MAILCHECK                         # turn off "You have new mail" notice
export LANG=C                           # set LANG variable
export viminit='set ai aw'              # set vim options
alias df='df -h'                        # set up aliases
alias rm='rm -i'                       # always do interactive rm's
alias lt='ls -ltrh | tail'
alias hw='history | tail'
alias ch='chmod 755 '

function switch() {                     # a function to exchange
    local tmp=$$switch                 # the names of two files
    mv "$1" $tmp
    mv "$2" "$1"
    mv $tmp "$2"
}
```

![](img/243613168ac865b539f12460d966088e_388_0.png)

# . (Dot) or source: Runs a Startup File in the Current Shell

After you edit a startup file such as .bashrc, you do not have to log out and log in again to put the changes into effect. Instead, you can run the startup file using the . (dot) or source builtin (they are the same command). As with other commands, the . must be followed by a space on the command line. Using . or source is similar to running a shell script, except these commands run the script as part of the current process. Consequently, when you use . or source to run a script, changes you make to variables from within the script affect the shell you run the script from. If you ran a startup file as a regular shell script and did not use the . or *source* builtin, the variables created in the startup file would remain in effect only in the subshell running the script—not in the shell you ran the script from. You can use the . or *source* command to run any shell script—not just a startup file—but undesirable side effects (such as changes in the values of shell variables you rely on) might occur. For more information refer to “Environment, Environment Variables, and Inheritance” on page 1032.

In the following example, the *.bashrc* sets several variables and sets *PS1*, the *bash* prompt, to the name of the host. The . builtin puts the new values into effect.

```
$ cat ./.bashrc
export TERM=xterm              # set the terminal type
export PS1="`hostname -f` : "   # set the prompt string
export CDPATH=:$HOME          # add HOME to CDPATH string
stty kill '^Au'               # set kill line to control-u
$ . ./.bashrc

Guava:
```

## COMMANDS THAT ARE SYMBOLS

The Bourne Again Shell uses the symbols (, ), [, ], and $ in a variety of ways. To minimize confusion, Table 9-1 lists the most common use of each of these symbols and the page on which it is discussed.

**Table 9-1 Built-in commands that are symbols**

| Symbol | Command |
| :--- | :--- |
| `( )` | Subshell (page 344) |
| `$( )` | Command substitution (page 410) |
| `(( ))` | Arithmetic evaluation; a synonym for *let* (use when the enclosed value contains an equal sign; page 1056) |
| `$(( ))` | Arithmetic expansion (not for use with an enclosed equal sign; page 408) |
| `[ ]` | The *test* command (pages 983 and 986) |
| `[[ ]]` | Conditional expression; similar to `[ ]` but adds string comparisons (page 1057) |

# REDIRECTING STANDARD ERROR

Chapter 5 covered the concept of standard output and explained how to redirect standard output of a command. In addition to standard output, commands can send output to *standard error*. A command might send error messages to standard error to keep them from getting mixed up with the information it sends to standard output.

Just as it does with standard output, by default the shell directs standard error to the screen. Unless you redirect one or the other, you might not know the difference between the output a command sends to standard output and the output it sends to standard error. One difference is that the system buffers standard output but does not buffer standard error. This section describes the syntax used by bash to redirect standard error and to distinguish between standard output and standard error.

### File descriptors

A file descriptor is the place a program sends its output to and gets its input from. When you execute a program, the shell opens three file descriptors for the program: 0 (standard input), 1 (standard output), and 2 (standard error). The redirect output symbol (page 154) is shorthand for 1>, which tells the shell to redirect standard output. Similarly < (page 155) is short for 0<, which redirects standard input. The symbols 2> redirect standard error. For more information refer to “File Descriptors” on page 1016.

The following examples demonstrate how to redirect standard output and standard error to different files and to the same file. When you run the cat utility with the name of a file that does not exist and the name of a file that does exist, cat sends an error message to standard error and copies the file that does exist to standard output. Unless you redirect them, both messages appear on the screen.

```
$ cat y
This is y.
$ cat x
cat: x: No such file or directory

$ cat x y
cat: x: No such file or directory
This is y.
```

When you redirect standard output of a command, output sent to standard error is not affected and still appears on the screen.

```
$ cat x y > hold
cat: x: No such file or directory
$ cat hold
This is y.
```

Similarly, when you send standard output through a pipeline, standard error is not affected. The following example sends standard output of cat through a pipeline to tr, which in this example converts lowercase characters to uppercase. (See the tr info page for more information.) The text that cat sends to standard error is not translated because it goes directly to the screen rather than through the pipeline.

```
$ cat x y | tr "[a-z]" "[A-Z]"
cat: x: No such file or directory
THIS IS Y.
```

The following example redirects standard output and standard error to different files. The shell redirects standard output (file descriptor 1) to the filename following 1>. You can specify > in place of 1>. The shell redirects standard error (file descriptor 2) to the filename following 2>.

```
$ cat x y 1> hold1 2> hold2
$ cat hold1
This is y.
$ cat hold2
cat: x: No such file or directory
```

### Combining standard output and standard error

In the next example, the `&>` token redirects standard output and standard error to a single file:

```
$ cat x y &> hold
$ cat hold
cat: x: No such file or directory
This is y.
```

### Duplicating a file descriptor

In the next example, first `1>` redirects standard output to `hold`, and then `2>&1` declares file descriptor 2 to be a duplicate of file descriptor 1. As a result, both standard output and standard error are redirected to `hold`.

```
$ cat x y 1> hold 2>&1
$ cat hold
cat: x: No such file or directory
This is y.
```

In this case, `1> hold` precedes `2>&1`. If they had appeared in the opposite order, standard error would have been made a duplicate of standard output before standard output was redirected to `hold`. Only standard output would have been redirected to `hold` in that case.

### Sending errors through a pipeline

The next example declares file descriptor 2 to be a duplicate of file descriptor 1 and sends the output for file descriptor 1 (as well as file descriptor 2) through a pipeline to the `tr` command.

```
$ cat x y 2>&1 | tr "[a-z]" "[A-Z]"
CAT: X: NO SUCH FILE OR DIRECTORY
THIS IS Y.
```

The token `&1` is shorthand for `2>&1`:

```
$ cat x y 1& tr "[a-z]" "[A-Z]"
CAT: X: NO SUCH FILE OR DIRECTORY
THIS IS Y.
```

### Sending errors to standard error

You can use `1>&2` (or simply `>&2`; the 1 is not required) to redirect standard output of a command to standard error. Shell scripts use this technique to send the output of `echo` to standard error. In the following script, standard output of the first `echo` is redirected to standard error:

```
$ cat message_demo
echo This is an error message. 1>&2
echo This is not an error message.
```
