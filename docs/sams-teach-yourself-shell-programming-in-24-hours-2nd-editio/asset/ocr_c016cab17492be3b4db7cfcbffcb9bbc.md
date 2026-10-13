Here the variable arg will be set to each argument in turn. The specified list of commands, $list, will be executed for each argument. The following function illustrates the use of this for loop:

```
echoargs () {
  for arg in "$@"
  do
    echo $arg
  done
  return 0
}
```

# How can I forward all the arguments given to my script to another command?

A common task of shell programmers is writing a wrapper script for a command. A wrapper script might need to define a set of variables and change the environment in some way before a particular command starts executing.

When writing wrapper scripts, you need to forward all the arguments given to your script to a command. Usually the following is sufficient:

```
cmd "$@"
```

Here cmd is the name of the command you want to execute.

The one problem with this is that if no arguments were specified to your script, some versions of the shell will expand "$@" to "". If no arguments were specified, you want to execute cmd, not cmd "". To avoid this problem, you can use the following:

```
command ${@:-"$@"}
```

Here you are using one of the forms of variable substitution discussed in Chapter 9, "Substitution." In this case you check to see whether the variable $@ has a value. If it does, you substitute the value "$@" for it. If your script was not given any command-line arguments, $0 will be null; thus no value will be substituted.

# How do I use the value of a shell variable in a sed command?

The simplest method to use variables in a sed command is to enclose your sed command in double quotes (" ") instead of single quotes (' '). Because the shell performs variable substitution on double-quoted strings, the shell will substitute the value of any variables you specify before sed executes.

For example, the command

```
sed "/$DEL/d" file1 > file2
```

deletes all the lines in file1 that contain the value stored in the variable $DEL.