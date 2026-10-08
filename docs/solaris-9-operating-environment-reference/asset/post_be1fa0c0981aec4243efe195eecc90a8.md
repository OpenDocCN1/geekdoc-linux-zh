
modify the value of any of these parameters or create new parameters, none of
affect the environment unless you use the export command to bind the shell's
parameter to the environment (see also set -a). You can remove a parameter from the
environment seen by any executed command is thus composed of any unmodified name-value pairs originally inherited by the
shell, minus any pairs removed by unset, plus any modifications or additions, all of
which must be noted in export commands.

You can augment the environment for any command by prefixing it with one or more
assignments to parameters. Thus:

```
TERM=450 command
```

and

```
(export TERM; TERM=450; command)
```

are equivalent as far as the execution of command is concerned if command is not a special
command (see "Special Commands" on page 1274). If command is a special command,
then

```
TERM=450 command
```

modifies the variable in the current shell.
If -k option is set, all keyword arguments are placed in the environment, even if
they occur after the command name.

The following example prints a=b c and c.

```
$ echo a=b c
a=b c
$ set -k
$ echo a=b c
c$
```

> Note — If a command is executed and a command with the same name is
installed in a directory in the search path before the directory where the
original command was found, the shell continues to execute the original
command. Use the hash command to correct this situation.

# Signals

The INTERRUPT QUIT signals for an invoked command are ignored if the command
is followed by &:; otherwise, signals have the values inherited by the shell from its
parent, with the exception of signal 11 (but also the trap command).

# Execution

Each time a command is executed, the command substitution, parameter substitution,
ank interpretation, input/output redirection, file-name generation listed above
are carried out. If the command name matches the name of a defined function, the
function is executed in the shell process (note how this differs from the execution of shell
scripts that require a subshell for invocation). If the command name does not match
t name of a defined function matches one of the special commands listed below, it
is executed in the shell process. The positional parameters $1, $2, . . . are set to the
arguments of the function, nor neither matches a special command
a new process is created and an attempt is made to
or execute the command via exec(2).

# 1274

# sh, jsh

The shell parameter PATH defines the search path for the directory containing the command. Alternative directory names are separated by a colon (:). The default path is /usr/bin. The current directory is specified by a null path name that can appear immediately after the equal sign, between two colon delimiters anywhere in the path, or at the end of the path. If the command name contains a r, the search path is not used. Otherwise, each directory in the path is searched for an executable file. If the file has execution permission but is not a, it is assumed to be a file containing shell commands. A subshell is spawned to read it. A parenthesized command is also executed in a subshell.

The location in the search path where a command was found by the shell (to avoid unnecessary exec commands later). If the command was found in a relative directory, its location must be recalculated whenever the current directory changes. The shell forgets all remembered locations whenever the PATH variable is changed or the hash -r command is executed (see below).

# Special Commands

Input/output redirection is permitted for these commands. File descriptor 1 is the default output location. When job control is enabled, additional special commands are added to the shell's environment (see "Job Control" on page 1279).

- - Do not. Return a exit code.
- - filename Read and execute commands from filename, and return. Use the search path specified by PATH to the directory containing filename.

```
bg [%jobid ...]
```

When job control is enabled, the bg command to your environment to manipulate jobs. Resume the execution of a stopped job. If you omit %jobid, assume the current job. (See "Job Control" on page 1279 for more detail.)

- - break [n] Exit from the enclosing or while loop if any. If you specify n, break levels.

- - cd [argument] Change the current directory to argument. The shell parameter HOME is the default argument. The shell parameter CDPATH defines the search path for the directory containing argument. Alternate directory names with a colon (:). The default path is null (specifying the current directory). Note that the current directory is specified by a null path name that can appear immediately after the equal sign or between the colon delimiters anywhere else in the path list. If argument begins with a /, do not use the search path. search each directory in the path for argument.

- - chdir [dir]

The shell's working directory to dir. If you specify no argument, change to your home directory. If dir is a relative path not found in the current directory, check for it in directories listed in the CDPATH variable. If dir is the name of a shell variable whose value starts with a /, change to the directory by that value.

# sh, jsh

continue [n]

Resume the next iteration of the enclosing for or while loop. If n is specified, resume at the nth enclosing loop.

echo [arguments...]

Write the words in arguments to the standard output separated by space characters. See echo(1) for fuller usage and description.

eval [argument...]

exec [argument...]

Execute the command in place of the shell without creating a new process.

exit [n]

Exit the shell with status specified by n.

export [name...]

Mark the names for automatic export to the environment.

fg [%jobid...]

When job control is enabled, the fg command to your environment to manipulate jobs. Resume the execution of a stopped job into the foreground. If you omit %jobid, assume the current job. (See "Job Control" on page 1279 for more detail.)

getopts

Use in shell scripts to parse legal options (see intro(1)).

hash [-r] [name...]

For each name, determine the location in the search path. The -r option forgets remembered locations. If you specify no arguments, forget all remembered locations.

```
kill [-sig] %job ...
```

```
kill -1
```

Send either the TERM (terminate) signal or the specified signal to the specific jobs or processes. Give signals either by name or by (as given in signal(3) stripped of the SIG prefix, with the exception that SIGCHLD is named CHLD). If the signal being sent is TERM (terminate) or HUP (hangup), then the job or process a CONTP (continue) signal if stopped. The jobargument can be the process ID of a process that is not a member of one of the active jobs. See "Job Control" on kill 1279 for a description of the format of job in the second form.

login [argument...]

Equivalent to exec argument... See login(1) for usage and description.

```
newgrp [argument]
```

Equivalent to exec newgrp argument. See newgrp(1) for usage and description.

```
pwd
```

Print the current working directory. See pwd(1) for usage and description.

```
read name...
```

Read one line from the standard input, and using the IFS input field separator (normally space or Tab) to delimit word boundaries, assign the first word to the first name, the second word to the second name, and so forth, with leftover words assigned to the last name. You can continue lines \newline. You can quote characters other than newline by ceding them with a backslash. These backslashes are removed before words are assigned to names, and no interpretation is done on the character that follows the backslash. The return code is 0 unless an end-of-file is encountered.
