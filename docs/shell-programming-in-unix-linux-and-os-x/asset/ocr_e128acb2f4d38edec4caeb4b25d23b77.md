The exit status is that of the last command in the pipeline. Placing a `! ` at the beginning of the pipeline causes the exit status of the pipeline to be the logical negation of the last command in the pipeline.

If the command sequence is terminated by an ampersand &, it is run asynchronously in the background. The shell displays the process ID and job number of the command at the terminal and prompts for the next interactive command to be entered.

Typing of a command can continue to the next line if the last character on the line is a backslash character \.

The characters & && cause the command that follows to be executed only if the preceding command returns a zero exit status. The characters || cause the command that follows to be executed only if the preceding command returns a non-zero exit status. As an example,

```
grep "fred" /dev/null && echo "fred's logged on"
```

the echo is executed only if the grep returns a zero exit status.

# Comments

If the character # appears on a line, the shell treats the remainder of the line as a comment and ignores it for interpretation, substitution and execution.

# Parameters and Variables

There are three different types of parameters: shell variables, special parameters, and positional parameters.

# Shell Variables

A shell variable name must start with an alphabetic or underscore character, and can be followed by any number of alphanumeric or underscore characters. Shell variables can be assigned values on the command line by:

```
variable=value variable=value
```

Filename assignment is not performed on value.

# Positional Parameters

Whenever a shell program is executed, the name of the program is assigned to the variable $0 and the arguments typed on the command line to $1, $2, ..., respectively. Positional parameters can also be assigned values with the set command. Parameters 1 through 9 can be explicitly referenced. Parameters greater than 9 must be enclosed inside braces, as in ${10}.