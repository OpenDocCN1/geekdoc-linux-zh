# The suspend Command

The suspend command is used to suspend the execution of the shell script until it receives a SIGCONT signal. Here is the syntax for the command:

```
suspend [-f]
```

You can pass the -f option to suspend, which tells suspend to complain if if the calling shell is not a login shell and just to suspend the shell anyway. suspend will return a value of 0 if it executes successfully, or a non-zero error code otherwise. suspend can fail if called from a login shell and the -f option is not passed.

# Parsing Command-Line Parameters

You can pass command-line parameters to shell scripts. The arguments will come into your shell script as a number of variables. The variable name of each argument will simply be the number of the argument. The name of your shell script is actually the first argument, so it will be passed in the variable $0. Any other arguments will be passed in the variables $1, $2, and so on. There is also a special variable called $#, which contains the number of command-line parameters passed to your script.

Here is a sample program that outputs any parameters that have been passed to your script:

```
#!/bin/bash

echo The first argument you passed was $1
echo The total number of arguments you passed was $#
echo All of the arguments you passed were:
for param in $*
do
    echo $param
done
```

When you run the program, you should get output similar to the following:

```
$ ./arg how are you doing today?
The first argument you passed was how
The total number of arguments you passed was 5
All of the arguments you passed were:
how
are
you
doing
today?
```