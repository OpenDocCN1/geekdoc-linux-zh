
## Shell Scripting: Parameters and Special Variables

In the preceding example, the command-line parameters used were both numerical values. You can also use text strings as parameters:

```bash
$ cat stringparam.sh
#!/bin/bash
# Using one command-line string parameter
#
echo Hello $1, glad to meet you.
exit
$
$ ./stringparam.sh world
Hello world, glad to meet you.
$
```

The shell passes the string value entered into the command line to the script. However, you'll have a problem if you try to do this with a text string that contains spaces:

```bash
$ ./stringparam.sh big world
Hello big, glad to meet you.
$
```

Remember that the parameters are separated by spaces, so the shell interpreted the space as just separating the two values. To include a space as a parameter value, you must use quotation marks (either single or double quotation marks):

```bash
$ ./stringparam.sh 'big world'
Hello big world, glad to meet you.
$
$ ./stringparam.sh "big world"
Hello big world, glad to meet you.
$
```

> **NOTE**
> 
> **The quotation marks used when you pass text strings as parameters are not part of the data. They just delineate the beginning and the end of the data.**

If your script needs more than nine command-line parameters, you can continue, but the variable names change slightly. After the ninth variable, you must use braces around the variable number, such as `${10}`. Here's an example of doing that:

```bash
$ cat positional10.sh
#!/bin/bash
# Handling lots of command-line parameters
#
product=$((${10} * ${11}))
echo The tenth parameter is ${10}.
echo The eleventh parameter is ${11}.
echo The product value is $product.
exit
$
$ ./positional10.sh 1 2 3 4 5 6 7 8 9 10 11 12
The tenth parameter is 10.
The eleventh parameter is 11.
The product value is 110.
```

This technique allows you to add as many command-line parameters to your scripts as you could possibly need.

### Reading the script name

You can use the `$0` parameter to determine the script name the shell started from the command line. This can come in handy if you're writing a utility that has multiple functions or that produces log messages.

```bash
$ cat positional0.sh
#!/bin/bash
# Handling the $0 command-line parameter
#
echo This script name is $0.
exit
$ bash positional0.sh
This script name is positional0.sh.
$
```

However, there is a potential problem. When using a different command to run the shell script, the command becomes entangled with the script name in the `$0` parameter:

```bash
$ ./positional0.sh
This script name is ./positional0.sh.
$
```

An additional issue occurs when the actual string passed is the full script path, and not just the script's name. In this case, the `$0` variable gets set to the full script path and name:

```bash
$ /home/christine/scripts/positional0.sh
This script name is /home/christine/scripts/positional0.sh.
$
```

If you want to write a script that only uses the script's name, you'll have to do a little work in order to strip off whatever path is used to run the script or any entangled commands. Fortunately, there's a handy little command available that does just that. The `basename` command returns just the script's name without the path:

```bash
$ cat posbasename.sh
#!/bin/bash
# Using basename with the $0 command-line parameter
# 
name=$(basename $0)
# 
echo This script name is $name.
exit
$ ./posbasename.sh
This script name is posbasename.sh.
$
```

Now that's much better. You can use this technique to write a script that produces log messages identifying when it ran:

```bash
$ cat checksystem.sh
#!/bin/bash
# Using the $0 command-line parameter in messages
scriptname=$(basename $0)
#
echo The $scriptname ran at $(date)>> $HOME/scripttrack.log
exit
$
$ ./checksystem.sh
$ cat $HOME/scripttrack.log
The checksystem.sh ran at Thu 04 Jun 2020 10:01:53 AM EDT
$
```

Having a script that identifies itself is useful for tracking down script problems, auditing the system, and producing log messages.

### Testing parameters

Be careful when using command-line parameters in your shell scripts. If the script is run without the needed parameters, bad things can happen:

```bash
$ ./positional1.sh
./positional1.sh: line 5: ((: number <= : syntax error:
operand expected (error token is "<= ")
The factorial of is 1
$
```

When the script assumes there is data in a parameter variable and no data is present, most likely you'll get an error message from your script. This is a poor way to write scripts. Always check your parameters to make sure the data is there before using it:

```bash
$ cat checkpositional1.sh
#!/bin/bash
# Using one command-line parameter
#
if [ -n "$1" ]
then
    factorial=1
    for (( number = 1; number <= $1; number++ ))
    do
        factorial=$(($factorial * $number))
    done
    echo The factorial of $1 is $factorial
else
        echo "You did not provide a parameter."
fi
exit
$ ./checkpositional1.sh
You did not provide a parameter.
$ ./checkpositional1.sh 3
The factorial of 3 is 6
$
```

In this example, the `-n` test evaluation was used to check for data in the `$1` command-line parameter. In the next section, you'll learn another way to check command-line parameters.

### Using Special Parameter Variables

A few special Bash shell variables track command-line parameters. This section describes what they are and how to use them.

#### Counting parameters

As you saw in the last section, you should verify command-line parameters before using them in your script. For scripts that use multiple command-line parameters, this checking can get tedious.

Instead of testing each parameter, you can count how many parameters were entered on the command line. The Bash shell provides a special variable for this purpose.

The `$#` variable contains the number of command-line parameters included when the script was run. You can use this special variable anywhere in the script, just like a normal variable:

```bash
$ cat countparameters.sh
#!/bin/bash
# Counting command-line parameters
#
if [ $# -eq 1 ]
then
    fragment="parameter was"
else
    fragment="parameters were"
fi
echo $# $fragment supplied.
exit
$ ./countparameters.sh
0 parameters were supplied.
$ ./countparameters.sh Hello
1 parameter was supplied.
$ ./countparameters.sh Hello World
2 parameters were supplied.
$ ./countparameters.sh "Hello World"
1 parameter was supplied.
$
```

Now you have the ability to test the number of parameters present before trying to use them:

```bash
$ cat addem.sh
#!/bin/bash
# Adding command-line parameters
#
if [ $# -ne 2 ]
then
    echo Usage: $(basename $0) parameter1 parameter2
else
    total=$[ $1 + $2 ]
    echo $1 + $2 is $total
fi
exit
$
$ ./addem.sh
Usage: addem.sh parameter1 parameter2
$ ./addem.sh 17
Usage: addem.sh parameter1 parameter2
$ ./addem.sh 17 25
17 + 25 is 42
$
```

The `if-then` statement uses the `-ne` evaluation to perform a numeric test of the command-line parameters supplied. If the correct number of parameters isn't present, an error message displays showing the correct usage of the script.

This variable also provides a cool way of grabbing the last parameter on the command line without having to know how many parameters were used. However, you need to use a little trick to get there.

If you think this through, you might think that because the `$#` variable contains the value of the number of parameters, using the variable `${$#}` would represent the last command-line parameter variable. Try that and see what happens:

```bash
$ cat badlastparamtest.sh
#!/bin/bash
# Testing grabbing the last parameter
#
echo The number of parameters is $#
echo The last parameter is ${$#}
exit
$ ./badlastparamtest.sh one two three four
The number of parameters is 4
The last parameter is 2648
$
```

Obviously, something went wrong. It turns out that you can't use the dollar sign within the braces. Instead, you must replace the dollar sign with an exclamation mark. Odd, but it works:

```bash
$ cat goodlastparamtest.sh
#!/bin/bash
# Testing grabbing the last parameter
#
echo The number of parameters is $#
echo The last parameter is ${!#}
exit
$ ./goodlastparamtest.sh one two three four
The number of parameters is 4
The last parameter is four
$ ./goodlastparamtest.sh
The number of parameters is 0
The last parameter is ./goodlastparamtest.sh
$
```

Perfect. It's important to notice that, when there weren't any parameters on the command line, the `$#` value was 0, but the `${!#}` value was the command used to run the script.
