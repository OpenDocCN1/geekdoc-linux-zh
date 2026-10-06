between the function header and the closing curly brace. Defining them as functions would,
hover, make them inaccessible as standalone commands.

# Removing a Function Definition

To remove the definition of a function from the shell, use the unset command with the -f
option. Look familiar? Is it the same command you use to remove the definition of a variable
from the shell.

```
$ unset -f nu
$ nu
sh: nu: not found
$
```

# The return Command

If you use exit from inside a function, its effect is not only to terminate execution of the
function but also of the shell program that called the function. It exits all the way back to the
command line. If you instead want to just exit the function, use the return command, whose
format is

return n

The value n is used as the return status of the function. If omitted, the status is that of the last
command executed. This is also what gets returned if you don't include a return statement in
your function. The return status is in all other ways equivalent to the exit status: you can access
its value through the shell variable $, and you can test it if, while, and until commands.

# The type Command

When you type in the name of a command to execute, it's useful to know whether the
command is a function, a shell built-in, a standard Unix command or even a shell
alias. This is where the type command comes in handy. The type command takes one or more
names as its argument and tells you what it knows about it. Here are some examples:

```
$ nu() { who | wc -l; }
$ type pwd
pwd is a shell builtin
$ type ls
is is aliased to '/bin/ls -F
$ type cat
cat is /bin/cat
$ type nu
nu is a function
$
```