them by their position on the command line. Only the set builtin (page 998) allows you to change the values of positional parameters. However, you cannot change the value of the command name from within a script.

# $#: NUMBER OF COMMAND-LINE ARGUMENTS

The $# parameter holds the number of arguments on the command line (positional parameters), not counting the command itself:

```
```
$ cat num_args
echo "This script was called with $# arguments."
$ ./num_args sam max zach
This script was called with 3 arguments.
```
```

# $0: NAME OF THE CALLING PROGRAM

The shell stores the name of the command you used to call a program in parameter $0. This parameter is numbered zero because it appears before the first argument on the command line:

```
```
$ cat abc
echo "The command used to run this script is $0"
$ ./abc
The command used to run this script is ./abc
$ /home/sam/abc
The command used to run this script is /home/sam/abc
```
```

The preceding shell script uses echo to verify the name of the script you are executing. You can use the basenname utility and command substitution to extract and display the simple filename of the command:

```
```
$ cat abc2
echo "The command used to run this script is $(basename $0)"
$ /home/sam/abc2
The command used to run this script is abc2
```
```

# $1–$n: COMMAND-LINE ARGUMENTS

The first argument on the command line is represented by parameter $1, the second argument by $2, and so on up to $n. For values of n greater than 9, the number must be enclosed within braces. For example, the twelfth command-line argument is represented by ${12}. The following script displays positional parameters that hold command-line arguments:

```
```
$ cat display_5args
echo First 5 arguments are $1 $2 $3 $4 $5

$ ./display_5args zach max helen
First 5 arguments are zach max helen
```
```

The display_5args script displays the first five command-line arguments. The shell assigns a null value to each parameter that represents an argument that is not