command-line parameters in your Bash shell scripts.

# # Reading parameters

The Bash shell assigns special variables, called *positional parameters*, to all of the command-line parameters entered. This includes the name of the script the shell is executing. The positional parameter variables are standard numbers, with $0 being the script’s name, $1 being the first parameter, $2 being the second parameter, and so on, up to $9 for the ninth parameter.

Here’s a simple example of using one command-line parameter in a shell script:

```
```
$ cat positional1.sh
#!/bin/bash
# Using one command-line parameter
#
factorial=1
for (( number = 1; number <= $1; number++ ))
do
        factorial=$[ $factorial * $number ]
done
echo The factorial of $1 is $factorial
exit
$
./positional1.sh 5
The factorial of 5 is 120
$
```
```

You can use the $1 variable just like any other variable in the shell script. The shell script automatically assigns the value from the command-line parameter to the variable, so you don’t need to do anything special.

If you want to enter more command-line parameters for your script, each parameter must be separated by a space on the command line. And the shell assigns each parameter to the appropriate variable:

```
```
$ cat positional2.sh
#!/bin/bash
# Using two command-line parameters
#
product=$[ $1 * $2 ]
```
```