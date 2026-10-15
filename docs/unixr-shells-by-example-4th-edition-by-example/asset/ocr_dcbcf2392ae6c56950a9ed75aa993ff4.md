# EXPLANATION

+   1. The while command tests the exit status of getopts. If getopts can successfully process an argument, it returns 0 exit status, and the body of the while loop is entered. The colon appended to the z option tells getopts that an argument must follow the -z option. If the option takes an argument, the argument is stored in the getopts built-in variable OPTARG.
+   2. If x is given as an option, it is stored in the variable arguments.
+   3. If z is given as an option with an argument, the argument is stored in the built-in variable OPTARG.
+   4. If an invalid option is entered, the question mark is stored in the variable arguments, and an error message is displayed.
+   5. The special getopts variable, OPTIND, holds the number of the next option to be processed. Its value is always one more than the actual number of command-line arguments.

# 8.9.2 The eval Command and Parsing the Command Line

The eval command evaluates a command line, performs all shell substitutions, and then executes the command line. Essentially, it parses the command line twice. It is used when normal parsing of the command line is not enough.

# EXAMPLE 8.63

```
1 $ set a b c d
2 $ echo The last argument is \$#
   The last argument is $4
3 $ echo The last argument is $4
   The last argument is d
4 $ eval echo The last argument is \$#
   The last argument is d
5 $ set -x
$ echo The last argument is \$#
+ eval echo the last argument is $4
+ echo the last argument is d
   The last argument is d
```

# EXPLANATION

+   1. Four positional parameters are set.
+   2. The desired result is to print the value of the last positional parameter. The \$ will print a literal dollar sign. The $# evaluates to 4, the number of positional parameters. After the shell evaluates the $4, it does not parse the line again to get the value of $4.
+   3. $4 is printed instead of the last argument.
+   4. After the shell performs variable substitution, the eval command performs the variable substitution and then executes the echo command.
+   5. Turn on the echoing to watch the order of parsing.