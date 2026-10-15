# EXAMPLE 12.71 (CONTINUED)

```
(The Command Line)
4 $ opts3 -d
-d is the ON switch
5 $ opts3 +d
+d is the OFF switch
6 $ opts3 -e
e is not a valid option
7 $ opts3 e
```

# EXPLANATION

1 The while command tests the exit status of getopts; if getopts can successfully process an argument, it returns 0 exit status, and the body of the while loop is entered. The colon prepended to the d option tells getopts not to print an error message if the user enters an invalid option.

2 One of the legal options is -d. If -d is entered as an option, the d (without the dash) is stored in the options variable. (The -x option to the print command allows the first character in the print string to be a dash.)

3 One of the legal options is +d. If +d is entered as an option, the d (with the plus sign) is stored in the options variable.

4 The -d option is a legal option to opts3.

5 The +d option is also a legal option to opts3.

6 The -e option is invalid. A question mark is stored in options if the option is illegal. The illegal argument is stored in OPTARG.

7 The option is prepended with neither a dash nor a plus sign. The getopts command will not process it as an option and returns a nonzero exit status. The while loop is terminated.

# EXAMPLE 12.72

```
(The Script)
#!/bin/ksh
# Program opts4
# Using getopts -- Fourth try --
1 alias USAGE='print "usage: opts4 [-x] filename " >&2'
2 while getopts :x: arguments
do
case $arg in
3 x) print "$OPTARG is the name of the argument ";;
4 :) print "Please enter an argument after the -x option" >&2
USAGE ;;
```