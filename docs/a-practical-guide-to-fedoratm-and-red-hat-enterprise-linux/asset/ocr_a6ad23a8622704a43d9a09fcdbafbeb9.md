Keyword variables have special meaning to the shell and usually have short, mnemonic names. When you start a shell (by logging in, for example), the shell inherits several keyword variables from the environment. Among these variables are HOME, which identifies your home directory, and PATH, which determines which directories the shell searches and in which order to locate commands you give the shell. The shell creates and initializes (with default values) other keyword variables when you start it. Still other variables do not exist until you set them.

You can change the values of most keyword shell variables. It is usually not necessary to change the values of keyword variables initialized in the /etc/profile or /etc/csh.cshrc systemwide startup files. If you need to change the value of a bash keyword variable, do so in one of your startup files (page 329). Just as you can make user-created variables environment variables, so you can make keyword variables environment variables—a task usually done automatically in startup files. You can also make a keyword variable readonly. See page 358 for a discussion of keyword variables.

The names of positional and special parameters do not resemble variable names. Most of these parameters have one-character names (for example, 1, ?, and #) and are referenced (as are all variables) by preceding the name with a dollar sign ($1, $2, and $#). The values of these parameters reflect different aspects of your ongoing interaction with the shell.

Whenever you run a command, each argument on the command line becomes the value of a positional parameter (page 1022). Positional parameters enable you to access command-line arguments, a capability you will often require when you write shell scripts. The set builtin (page 1024) enables you to assign values to positional parameters.

Other frequently needed shell script values, such as the name of the last command executed, the number of positional parameters, and the status of the most recently executed command, are available as special parameters (page 1027). You cannot assign values to special parameters.

# ## USER-CREATED VARIABLES

The first line in the following example declares the variable named person and initializes it with the value max:

```
$ person=max
$ echo person
person
$ echo $person
max
```

Because the echo builtin copies its arguments to standard output, you can use it to display the values of variables. The second line of the preceding example shows that person does not represent max. Instead, the string person is echoed as person. The shell substitutes the value of a variable only when you precede the name of the variable with a dollar sign ($). Thus the command echo $person displays the value of the variable