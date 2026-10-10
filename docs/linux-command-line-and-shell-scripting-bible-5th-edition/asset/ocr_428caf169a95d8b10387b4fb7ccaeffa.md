# Part II: Shell Scripting Basics

As you extract each individual parameter, use the case statement (see Chapter 12, "Using Structured Commands") to determine when a parameter is formatted as an option:

```
```
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
$ ./extractoptions.sh -a -b -c -d

Found the -a option
Found the -b option
Found the -c option
-d is not an option

$ ```
```

The case statement checks each parameter for valid options. When one is found, the appropriate commands are run in the case statement.

This method works, no matter which order the options are presented on the command line:

```
```
$ ./extractoptions.sh -d -c -a
-d is not an option
Found the -c option
Found the -a option
```
```

The case statement processes each option as it finds it in the command-line parameters. If any other parameters are included on the command line, you can include commands in the catch all part of the case statement to process them.

# Separating options from parameters

Often you'll run into situations where you'll want to use both options and parameters for a shell script. The standard way to do this in Linux is to separate the two with a special character code that tells the script when the options are finished and when the normal parameters start.