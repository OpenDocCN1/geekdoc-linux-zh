# Default Value Assignment

The second form of advanced variable substitution assigns a value to a variable when the variable's value is null. The syntax is as follows:

```
${param:-word}
```

Here param is the name of the variable and word is the value to assign if the variable's value is null. The following example illustrates the behavior:

```
$ unset FRUIT
$ echo FRUIT is $FRUIT
FRUIT is
$ echo FRUIT is ${FRUIT:-APPLE}
FRUIT is APPLE
```

# Null Value Error

Sometimes substituting or assigning default values can hide problems in a shell script. In order to spot such problems in critical parts of a shell script, you can use the third form of variable substitution that outputs a message to STDERR when a variable is unset. The syntax is as follows:

```
${param:?msg}
```

Here, param is the name of the variable and msg is the message to be printed to STDERR.

If a shell script or shell function requires a certain variable to be set for proper execution, this form of variable substitution can be used. For example, the following expression causes the shell to exit if the variable $HOME is unset:

```
: ${HOME:? 'Your home directory is undefined.'}
```

In addition to using the variable substitution form described previously, this example makes use of the no-op (short for no operation) command, :. This command performs no work; it just evaluates the arguments passed to it.

# Substitute When Set

The final form of variable substitution is used to substitute a value when a variable is set. The syntax is as follows:

```
${param:+word}
```

Here param is the name of the variable and word is the value to substitute if the variable is set. If param is unset, then nothing is substituted. This form does not alter the value of the variable. It is commonly used by scripts to indicate that the script is running in debug mode:

```
echo ${DEBUG:+'Debug is active.'}
```