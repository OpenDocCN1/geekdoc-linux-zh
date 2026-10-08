# alias, unalias

# Examples

# C Shell

The following example creates an alias for the alias command and uses the alias shortcut to create an alias for the history command and to create a moer alias for the more command.

```
castle% alias a alias
caste% a h history
caste% a moer more
```

The following example lists aliases that are set in the .cshrc file.

```
castle% alias
G3 172.16.8.21
a alias
c clear
history
mac 172.16.8.20
caste%
```

# Korn Shell

The following alias changes ls to give a more annotated output in columnar format.
alias ls="ls -CF"

The following alias creates a simple redo to repeat previous entries in the command history file.
alias r='fc -s'

The following alias uses 1-kilobyte units for du.
alias du="du -k"

Alternatively, you can create the alias in the following form, using a backslash to escape the space character and omitting the double quotes around the command.
alias du\=du -k

The following alias sets up nohup so that it can deal with an argument that is itself an alias name.
alias nohup="nohup 

The following example lists the default aliases that are set for the Korn Shell.

```
$ alias
autoload='typeset -fu'
command='command '
functions='typeset -f'
history='fc -1'
integer='typeset -i'
local=typeset
nohup='nohup '
r='fc -e -'
```