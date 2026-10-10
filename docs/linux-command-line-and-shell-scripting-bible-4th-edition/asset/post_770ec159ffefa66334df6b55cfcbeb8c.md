
variable returns the script name used on the command line.

## Grabbing all the data

In some situations you want to grab all the parameters provided on the command line. Instead of having to mess with using the $# variable to determine how many parameters are on the command line and having to loop through them all, you can use a couple of other special variables.

The $* and $@ variables provide easy access to all your parameters. Both of these variables include all the command-line parameters within a single variable.

The $* variable takes all the parameters supplied on the command line as a single word. The word contains each of the values as they appear on the command line. Basically, instead of treating the parameters as multiple objects, the $* variable treats them all as one parameter.

The $@ variable, on the other hand, takes all the parameters supplied on the command line as separate words in the same string. It allows you to iterate through the values, separating out each parameter supplied. This is most often accomplished using a *for* loop.

It can easily get confusing trying to figure out how these two variables operate. Let's look at the difference between the two:

```bash
$ cat grabbingallparams.sh
#!/bin/bash
# Testing different methods for grabbing all the parameters
#
echo
echo "Using the \$* method: $*"
echo
echo "Using the \$@ method: $@"
echo
exit

$ ./grabbingallparams.sh alpha beta charlie delta

Using the $* method: alpha beta charlie delta

Using the $@ method: alpha beta charlie delta
```

Notice that on the surface, both variables produce the same output, showing all the command-line parameters provided at once. The following example demonstrates where the differences are:

```bash
#!/bin/bash
# Exploring different methods for grabbing all the parameters
#
echo
echo "Using the \$* method: \$*"
count=1
for param in "\$*"
do
	echo "\$* Parameter #\$count = \$param"
	count=\$[ \$count + 1 ]
done
#
echo
echo "Using the \$@ method: \$@"
count=1
for param in "\$@"
do
	echo "\$@ Parameter #\$count = \$param"
	count=\$[ \$count + 1 ]
done
echo
exit
```

```bash
$ ./grabdisplllparams.sh alpha beta charlie delta
Using the \$* method: alpha beta charlie delta
\$* Parameter #1 = alpha
Using the \$@ method: alpha beta charlie delta
\$@ Parameter #1 = alpha
\$@ Parameter #2 = beta
\$@ Parameter #3 = charlie
\$@ Parameter #4 = delta
$
```

Now we're getting somewhere. By using the for command to iterate through the special variables, you can see how they each treat the command-line parameters differently. The $* variable treated all the parameters as a single parameter, whereas the $@ variable treated each parameter separately. This is a great way to iterate through command-line parameters.

## Being Shifty

Another tool you have in your Bash shell tool belt is the shift command. The Bash shell provides the shift command to help you manipulate command-line parameters. The shift command literally shifts the command-line parameters in their relative positions.

When you use the shift command, it moves each parameter variable one position to the left by default. Thus, the value for variable $3 is moved to $2, the value for variable $2 is moved to $1, and the value for variable $1 is discarded (note that the value for variable $0, the program name, remains unchanged).

This is another great way to iterate through command-line parameters. You can just operate on the first parameter, shift the parameters over, and then operate on the first parameter again.

Here’s a short demonstration of how this works:

```bash
$ cat shiftparams.sh
#!/bin/bash
# Shifting through the parameters
#
echo
echo "Using the shift method:"
count=1
while [ -n "$1" ]
do
    echo "Parameter #$count = $1"
    count=$((count + 1))
    shift
done
echo
exit

$ ./shiftparams.sh alpha bravo charlie delta

Using the shift method:
Parameter #1 = alpha
Parameter #2 = bravo
Parameter #3 = charlie
Parameter #4 = delta

$
```

The script performs a while loop, testing the length of the first parameter's value. When the first parameter's length is 0, the loop ends. After testing the first parameter, the shift command is used to shift all the parameters one position.

> **NOTE**
>
> **Be careful when working with the shift command. When a parameter is shifted out, its value is lost and can't be recovered.**

Alternatively, you can perform a multiple location shift by providing a parameter to the shift command. Just provide the number of places you want to shift:

```bash
$ cat bigshiftparams.sh
#!/bin/bash
# Shifting multiple positions through the parameters
#
echo
echo "The original parameters: $*"
echo "Now shifting 2 ..."
shift 2
echo "Here's the new first parameter: $1"
echo
exit

$ ./bigshiftparams.sh alpha bravo charlie delta

The original parameters: alpha bravo charlie delta
Now shifting 2 ...
Here's the new first parameter: charlie
$
```

By using values in the shift command, you can easily skip over parameters you don't need in certain situations.

## Working with Options

If you've been following along in the book, you've seen several Bash commands that provide both parameters and options. *Options* are single letters preceded by a dash that alter the behavior of a command. This section shows three methods for working with options in your shell scripts.

### Finding your options

On the surface, there's nothing all that special about command-line options. They appear on the command line immediately after the script name, just the same as command-line parameters. In fact, if you want, you can process command-line options the same way you process command-line parameters.

### Processing simple options

In the shiftparams.sh script earlier, you saw how to use the `shift` command to work your way down the command-line parameters provided with the script program. You can use the same technique to process command-line options.

As you extract each individual parameter, use the `case` statement (see Chapter 12, “Using Structured Commands”) to determine when a parameter is formatted as an option:

```bash
$ cat extractoptions.sh
#!/bin/bash
# Extract command-line options
#
echo
while [ -n "$1" ]
do
	case "$1" in
	-a) echo "Found the -a option" ;;
	-b) echo "Found the -b option" ;;
	-c) echo "Found the -c option" ;;
	*) echo "$1 is not an option" ;;
	esac
	shift
done
echo
exit
```

```bash
$ ./extractoptions.sh -a -b -c -d

Found the -a option
Found the -b option
Found the -c option
-d is not an option

$
```

The case statement checks each parameter for valid options. When one is found, the appropriate commands are run in the case statement. This method works, no matter in what order the options are presented on the command line:

```bash
$ ./extractoptions.sh -d -c -a

-d is not an option
Found the -c option
Found the -a option

$
```

The case statement processes each option as it finds it in the command-line parameters. If any other parameters are included on the command line, you can include commands in the catch-all part of the case statement to process them.

### Separating options from parameters

Often you'll run into situations where you'll want to use both options and parameters for a shell script. The standard way to do this in Linux is to separate the two with a special character code that tells the script when the options are finished and when the normal parameters start.

For Linux, this special character is the double dash ( - - ). The shell uses the double dash to indicate the end of the option list. After seeing the double dash, your script can safely process the remaining command-line parameters as parameters and not options.

To check for the double dash, simply add another entry in the case statement:

```bash
$ cat extractoptionparams.sh
#!/bin/bash
# Extract command-line options and parameters
#
echo
while [ -n "$1" ]
do
	case "$1" in
	-a) echo "Found the -a option" ;;
	-b) echo "Found the -b option" ;;
	-c) echo "Found the -c option" ;;
	--) shift
		break;;
	*) echo "$1 is not an option" ;;
	esac
	shift
done
#
echo
count=1
for param in $@
do
	echo "Parameter #$count: $param"
	count=$[ $count + 1 ]
done
echo
exit
$
```

This script uses the **break** command to break out of the **while** loop when it encounters the double dash. Because we're breaking out prematurely, we need to ensure that we stick in another **shift** command to get the double dash out of the parameter variables.

For the first test, try running the script using a normal set of options and parameters:

```bash
$ ./extractoptionparams.sh -a -b -c test1 test2 test3

Found the -a option
Found the -b option
Found the -c option
test1 is not an option
test2 is not an option
test3 is not an option

$
```
