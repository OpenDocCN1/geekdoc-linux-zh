The “dot” command causes the indicated file to be read and executed by the shell, just as if the lines from the file were typed at that point. Note that `file` does not have to be executable, only readable. Also, the shell uses the PATH variable to find `file`.

*Example*

```
. progdefs                         Execute commands in progdefs
```

The preceding command causes the shell to search the current PATH for the file `progdefs`. When it finds it, it reads and executes the commands from the file.

Note that because `file` is not executed by a subshell, variables set and/or changed within `file` remain in effect after execution of the commands in `file` is complete.

# The **alias** Command

*General Format:* `alias name=string [name=string ...]`

The alias command assigns `string` to the alias `name`. Whenever `name` is used as a command, the shell substitutes `string`, performing command-line substitution after `string` is in place.

*Examples*

```
alias ll='ls -l'
alias dir='basename $(pwd)'
```

If an alias ends with a blank, the word following the alias is also checked to see whether it’s an alias.

The format

```
alias name
```

causes the alias for name to be printed out.

```
alias
```

alias with no arguments lists all aliases.

`alias` returns an exit status of zero unless a `name` is given (as in `alias name`) for which no alias has been defined.

# The **bg** Command

*General Format:* `bg job_id`

If job control is enabled, the job identified by `job_id` is put into the background. If no argument is given, the most recently suspended job is put into the background.

*Example*

```
bg %2
```