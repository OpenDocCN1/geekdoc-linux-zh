
# Advanced Bash-Scripting Guide

Although *recursion* is possible in a shell script, it tends to be slow and its implementation is often an ugly kludge.

An acronym is an *ersatz* word formed by pasting together the initial letters of the words into a tongue-twisting phrase. This immoral and pernicious practice deserves appropriately severe punishment. Public flogging suffices.

Many of the features of *ksh88*, and a few from the updated *ksh92* have been merged into Bash.

By convention, user-written shell scripts that are Bourne compliant carry a name with a *-sh extension. System scripts, like those found in `/etc/rc.d`, do not necessarily conform to this nomenclature.

More commonly seen in the literature as *she-bang* or *sh-bang*. This is from concatenation of the tokens sharp (#) and *bang* (!).

Some flavor of UNIX (those based on 4.2 BSD) allegedly took a four-byte magic number, requiring a blank after the ... #! /bin/bash. According to Svencheck this is a probable myth.

A line in a shell script will be the first thing the command interpreter (sh or bash) sees. Since this line begins with a #, it will be correctly interpreted as a comment when the command interpreter executes the script. The line has served its purpose - calling the command interpreter.

If, in the script contains an extra *#!* line, then **bash** will interpret it as a comment.

```bash
#!/bin/bash
echo "Part 1 of script."
a=1

#!/bin/bash
# This does *not* launch a new script.

echo "Part 2 of script."
echo $a Value of $a stays at 1.
```

This allows some cute tricks.

```bash
#!/bin/rm
# Self-deleting script.

# Nothing seems to happen when you run this... except that the file disappears.

WHATEVER=85
echo "this line will never print (betcha!)."
exit WHATEVER # Doesn't matter. The script will not exit here.
# Try an echo $? after script termination.
# You'll get a 0, not 85.
```

Also, starting a README with #!/bin/more, and making it executable. The result is a self-documenting documentation file. (a here document using cat is a better alternative -- see Example-19).

Portable Operating System Interface, an attempt to standardize UNIX-like OSes. The POSIX specifications are listed on the Open Group site.

To avoid this, a script may have #!/bin/env she-bang line. This may be useful on UNIX machines where bash is not located in /bin. If Bash is your default shell, then # isn't at the beginning of a script. However, launching a script from a different shell, such as tcsh, then you will need...

# Appendix T. ASCII Table

| ID | Description |
| :--- | :--- |
| 13 | Caution: invoking a Bash script by turns off Bash-specific extensions, and the script may therefore fail to execute. |
| 14 | A script needs read as well as execution permission to run, since the shell needs to read it. |
| 15 | Why not simply invoke the script with? If the directory you are in (PWD) is where script is located, does this work? This fails, for security reasons, the current directory (./) is not by default included in user's PATH. It is therefore necessary to explicitly invoke the script in the current directory with. |
| 16 | An operator is an agent that carries out an operation. Some examples are the common arithmetic operators, +. In Bash, there is some overlap between the concepts of operator and keyword. |
| 17 | This is most commonly known as the ternary operator. Unfortunately, the ternary is an ugly word. It doesn't roll the tongue, and ternary is by far the most elegant usage. |
| 18 | American Standard Code for Information. This is a system for encoding text characters (alphabetic, numeric, and a limited set of symbols) that can be stored and manipulated by computers. |
| 19 | A PID, or process ID, is a number assigned to a running process. PIDs may be viewed with ps command. |
| 20 | **Definition:** A process is a currently executing command (or program), sometimes referred to as a shell does the expansion. |
| 21 | The shell does brace expansion as part of a pipe run as subshell. |
```bash
ls | read first; secondline;
# Error. The code in braces runs as subshell
# so the output of "first" cannot be passed to variables.
echo "First line is $secondline" # Won't.
```
| 22 | Even in lines to have magical powers, so does transform its target (roughly) fashion. The coder comes up with that runs on Linux will win with accolades. |
| 23 | Bash stores a list of commands previously used with the command-line in buffer. |
| 24 | A newline is also a whitespace character. This explains why a blank line, consisting only of linefeed, is considered whitespace. |
| 25 | Technically, the name of a variable is called lvalue, meaning that it appears on the left side of an assignment statement, as in VARIABLE=. A variable's value is an rvalue, meaning that it appears on the right side of an assignment statement, as in VARIABLE. |
| 26 | Note that functions also take positional parameters. |
| 27 | The process calling sets the parameter. By convention, this parameter is the name of the script. See the manpage (manual page) for exec. |
| 28 | If the script is sourced or symlinked, then this will not work. It is safer to check Bash Source. |
| 29 | Unless there is a file name in the current working directory. Yet another reason to quote (Thank you, Harald Koenig, for pointing this out.). |
| 30 | Encapsulating " within double quotes gives an error when used from the command line. This is because of history. Within a script, this problem does not occur, as the Bash mechanism is disabled then. More of concern is the apparently inconsistent behavior of within double quotes, and especially following a command. |
```bash
bash$ echo hello!\nhello!
bash$ echo "hello!\"
hello\!
```
```bash
bash$ echo \\
>
bash$ echo "\""
>
bash$ echo \a
a
bash$ echo "\a"
\a
```
```bash
bash$ echo \t
ty
Wait, wait.
```
Double quotes following an echo sometimes escape. Moreover, the -e option to echo causes the "t" to be interpreted as a tab. (Thank you, Wayne Pollock, for pointing this out, and Geoff Lee and Daniel Barclay for explaining it.) |
| 31 | "Word splitting," in this context, means dividing a character string into separate and discrete arguments. |
| 32 | In those instances there is no return terminating the function. |
| 33 | A token is a symbol or short string with a special meaning to attach to it (meta-meaning). In Bash, certain tokens, such as [ and . (dot-command), may expand to keywords and commands. |
| 34 | Per the 1913 edition of Webster's Dictionary: |

| Deprecate |
| --- |
| To pray against, as an evil; to seek to avert by prayer; to desire the removal of; to seek deliverance from; to express deep regret for; to disapprove of strongly. |
| 35 | Be aware that sudo binaries may open security holes. The sudo flag has no effect on shell scripts. |
| 36 | On Linux systems, the sticky bit is no longer used for files, only on directories. |
| 37 | As S. points out, in a compound test, quoting the variable string might not suffice. [ -n "$string" -o "$a" = "$b" ] |
| 38 | In a different context, += can serve as concatenation. This is useful for modifying environmental variables. |
| 39 | Side effects are, of course, unintended and undesirable consequences. |
| 40 | Precedence, in this context, has approximately the same priority as |
| 41 | A stack register is a set of consecutive memory locations, such that the values (pushed) are retrieved (popped) in reverse order. The last value is the first retrieved. This is sometimes called LIFO (last-in-first-out) or pushdown. |
| 42 | The PID of the currently running script is $, of course. |
| 43 | Somewhat analogous to recursion |
| 44 | The words "argument" and "parameter" are often used interchangeably. In the context of this document, they have the same meaning: a variable passed to a script or function. |
| 45 | Within a script, a subshell $$ returns the PID of the script, not the subshell. |
| 46 | "randomness", insofar as it exists at all, can only be found in completely unordered natural phenomena, such as radioactive decay. Computers computer-generated sequences of "random" numbers are referred to as pseudorandom. |
