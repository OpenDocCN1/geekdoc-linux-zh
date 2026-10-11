visible to the parent process that originally called the script. These variables are called private, or local, variables.

For example, if you call a script that in turn calls another script, any variables declared in the second script will be invisible to the first script. To make the variable created in the second script visible to the first script, you need to make it a global variable. You use the `export` built-in command to make a variable global.

You can use the `echo` built-in command to see the value of a variable if you type

```
`echo variable_name`
```

By default, `echo` prints exactly what you typed to the standard output. In the prior example, variable_name, what you typed would be displayed. To see the value of a variable, preface the variable's name with $, as in

```
`echo $variable_name`
```

This will cause `echo` to print the value of the variable to your display. Use the same syntax in a script when you are interested in the value and not the variable's name.

# Aliases

Aliases are user variables that are used to modify your environment. They are short names that have a value of a command. Often the value also contains arguments to be sent to the command.

Aliases can shorten the number of keys you have to type to enter frequently used commands or enable you to use an easier name for any command. The syntax for the alias command is

```
`alias [name=command]`
```

Aliases can be set at the command line but will be in effect only for that login session. Some helpful aliases that are often set systemwide are

```
`alias rm="rm -i"`
`alias cp="cp -i"`
`alias mv="mv -i"`
```

These commands set `rm`, `cp`, and `mv` to interactive mode every time they are invoked. In order to be systemwide, aliases must be entered by root in the /etc/bashrc file.

You can define your own personal aliases by editing the .bashrc file in your home directory, such as adding

```
`alias ls1="ls -1"`
`alias lsc="ls -color"`
`alias lsa="ls -AF"`
```