# Part II Shell Scripting Basics

# The more advanced getopts

The getopts command (notice that it's plural) is built into the bash shell. It looks a lot like its cousin, but has some expanded features.

Unlike getopt, which produces one output for all of the processed options and parameters found in the command line, the getopts command works on the existing shell parameter variables sequentially.

It processes the parameters it detects in the command line one at a time it is called. When it runs out of parameters, it exits with an exit status greater than zero. This makes it great for using in loops to parse all of the parameters on the command line.

The format of the getopts command is:

```
getopts string variable
```

The optstring value is similar to the one used in the getopt command. Valid list options in the optstring, along with a colon if the option requires a parameter value. To suppress error messages, start the optstring with a colon. The getopts command places the current parameter in the variable defined in the command line.

There are two environment variables that the getopts command uses. The OPTARG environment variable contains the value to be used if an option requires a parameter value. The OPTIND environment variable contains the value of the current location within the parameter list where getopts left off. This allows you to continue processing other command line parameters after finishing the options.

Let's take a look at a simple example that uses the getopts command:

```
$ cat test19
#!/bin/bash
# simple demonstration of the getopts command
while getopts :abc opt; do
  case "$opt" in
    a) echo "Found the -a option":
    b) echo "Found the -b option, with value $OPTARG":
    c) echo "Found the -c option":
    *) echo "Unknown option: $opt"
  esac
done
$ ./test19 -ab test1 -c
Found the -a option
```