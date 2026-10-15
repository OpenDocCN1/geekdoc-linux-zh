# EXAMPLE 14.73 (CONTINUED)

```
(The Command Line)
$ opts4 -xyz foo
You entered -x as an option.
You entered -y as an option.
You entered -z as an option.
$OPTARG is foo.
The number of arguments passed was 2.
```

```
$ opts4 -x -y -z boo
You entered -x as an option.
You entered -y as an option.
You entered -z as an option.
$OPTARG is boo.
The number of arguments passed was 4.
```

```
$ opts4 -d
Usage: opts4 [-xy] [-z argument]
```

# EXPLANATION

+   1. The while command tests the exit status of getopts; if getopts can successfully process an argument, it returns 0 exit status, and the body of the while loop is entered. The colon appended to the z option tells getopts that an argument must follow the -z option. If the option takes an argument, the argument is stored in the getopts built-in variable OPTARG.
+   2. If x is given as an option, it is stored in the variable arguments.
+   3. If z is given as an option with an argument, the argument is stored in the built-in variable OPTARG.
+   4. If an invalid option is entered, the question mark is stored in the variable arguments and an error message is displayed.
+   5. The special getopts variable OPTIND holds the number of the next option to be processed. Its value is always one more than the actual number of command-line arguments.

# 14.10.2 The eval Command and Parsing the Command Line

The eval command evaluates a command line, performs all shell substitutions, and then executes the command line. It is used when normal parsing of the command line is not flexible enough for what we want to do.