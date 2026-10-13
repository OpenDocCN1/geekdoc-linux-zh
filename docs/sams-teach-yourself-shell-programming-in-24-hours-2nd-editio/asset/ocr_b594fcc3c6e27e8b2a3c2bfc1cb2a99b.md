> Some programmers use true in place of : when creating infinite loops. Using the : is more efficient because it is a shell built-in command, whereas true is an external command and must be read from disk.

# : and Variable Substitution

Another use of the : command takes advantage of the fact that the shell evaluates arguments to it. This is a useful way to invoke variable substitution. For example:

```
: ${LINES:=24} ${TERM?'TERM not set'}
```

The : is a no-op, but the shell still evaluates its arguments. Thus LINES is set to 24 if LINES is empty or undefined. If TERM is empty or undefined, the whole script aborts with the error message "TERM not set".

# : and the C shell

You might sometimes find the : used as the first line of a older shell scripts. Some early versions of the C shell contained a bug that automatically assumes that any script whose first character is # is a C shell script. For this reason Bourne shell scripts had to start with something other than a # sign; the : was often used for this purpose.

Current versions of the C shell do not contain this bug, but some older Bourne shell scripts still use : as the first line.

# The type Command

The type command tells you the full pathname of a command if the shell can find that command in the search path, $PATH. The basic syntax is

```
type cmd1 ... cmdN
```

Here cmd1...cmdN are command names. If a command is not an external command that exists on disk, type tells you whether it is one of the following:

+   - A shell built-in command
+   - A shell keyword or reserved word
+   - An alias

If the given command is an alias for another command, type also gives the command that is actually invoked when you run the alias. For example,

```
$ type true vi case ulimit history
true is /bin/true
vi is /usr/bin/vi
```