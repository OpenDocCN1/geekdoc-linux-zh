# 432 BASH PROGRAMMING

```
printf format para1 para2 para3 ...
```

printf allows you to generate formatted output using the syntax of the C command printf. Detailed information on available formatting options can be obtained with man 3 printf.

# pushd directory

pushd stores the current directory and subsequently changes to the specified directory. With popd, you can switch back to the original directory. dirs displays a list of all directories stored.

```
read [var1 var2 var3 ...]
```

read reads a line of text into the specified variables. read expects its data from the standard input. When no variable is specified, read writes the input into the variable REPLY. When exactly one variable is specified, read writes the entire input into the first variable, the second word into the second variable ... and the remainder of the input into the last variable. Words are considered to be character strings separated by spaces or tabs.

The read command does not provide the possibility of outputting an info text as the input prompt. It might therefore be good idea to inform the user of the purpose of the input by means of echo -n, prior to execution of read commands.

# readonly

readonly displays the write-protected variables of the shell. Variables can be protected against modification with declare -r.

# setterm [option]

setterm modifies various settings of the terminal. When the command is executed without specifying an option, it displays a list of all available options. Some options have already been described on page 479. Useful options for shell programming are:

+   -bold on | off
activates/deactivates bold face. In text consoles, the text does not appear in bold face, but in a different color from other text.

+   -clear
clears the screen.

+   -default
restores colors and text attributes to their default settings.

+   -half-bright | off
highlighted type on/off.