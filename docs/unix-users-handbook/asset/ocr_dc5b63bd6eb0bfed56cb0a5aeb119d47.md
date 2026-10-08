keywords listed above. Aliases can be created, listed, and exported with the alias command and can be removed with the unalias command. Exported aliases remain in effect for subshells but must be reinitialized for separate invocations of the shell (see Invoking ksh below).

Aliasing is performed when scripts are read, not while they are executed. Therefore, for it to take effect, alias must be executed before the command referring to the alias is read.

Aliases are frequently used as a shorthand for full path names. An option to the aliasing facility allows the value of the alias to be automatically set to the full path name of the corresponding command. These aliases are called tracked aliases. The value of a tracked alias is defined the first time the identifier is read and becomes undefined each time the PATH variable is reset. These aliases remain tracked so that the next reference redefines the value. Several tracked aliases are compiled into the shell. The -h option of the set command converts each command name that is an identifier into a tracked alias.

The following exported aliases are compiled into the shell but can be unset or redefined:

```
```
autoload='tystest -fu'
false='let 0'
functions='tystest -f'
hash='alias -t -'
history='fc -1'
integer='tystest -i'
nohup='nohup '
r='fc -e -'
stop='kill -STOP'
suspend='kill -STOP $'
true=';'
type=' whence -v'
```
```

# Tilde Substitution

After alias substitution is performed, each word is checked to see if it begins with an unquoted ~- . If it does, the word up to a / is checked to see if it matches a user name in the /etc/passwd file. If a match is found, the ~ and the matched login name are replaced by the login directory of the matched user. This is called a tilde substitution. If no match is found, the original text is left unchanged. A ~, alone or before a /, is replaced by the value of the HOME parameter. A ~ followed by a + or - is replaced by the value of the parameter PWD and OLDPWD, respectively. In addition, tilde substitution is attempted when the value of a parameter assignment begins with a ~.

# Command Substitution

The standard output from a command enclosed in parentheses preceded by a dollar sign ( $(command) ) or a pair of back single quotes (accent grave) (` command` ) can be used as part or all of a word; trailing new-lines are removed. In the second (archaic) form, the string between the quotes is processed for special quoting characters before the command is executed (see Quoting below). The command substitution $(cat file) can be replaced by the equivalent but faster $(<file).

Command substitution of most special commands (built-ins) that do not perform I/O redirection are carried out without creating a separate process. However, command substitution of a function creates a separate process to execute the function and all commands (built-in or otherwise) in the function.

An arithmetic expression enclosed in double parentheses preceded by a dollar sign ($((expression))) is replaced by the value of the