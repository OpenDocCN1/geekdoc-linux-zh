# Functions

Modern shells support functions—long or short sequences of commands that can be referenced or reused often as desired in a shell program.

To define a function, you use the general format:

```
name () ... command; }
```

where name is the name of the function, the parentheses denote that a function is being defined, and the commands enclosed between the curly braces define the body of the function. These commands will be executed whenever the function is executed.

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
$ nrrun memo  Run it in memol
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