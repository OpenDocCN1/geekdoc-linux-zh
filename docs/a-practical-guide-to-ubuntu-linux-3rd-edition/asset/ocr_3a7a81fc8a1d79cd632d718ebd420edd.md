present on the command line. Thus the $4 and $5 parameters have null values in this example.

# shift: PROMOTES COMMAND-LINE ARGUMENTS

The shift builtin promotes each command-line argument. The first argument (which was $1) is discarded. The second argument (which was $2) becomes the first argument (now $1), the third becomes the second, and so on. Because no “unshift” command exists, you cannot bring back arguments that have been discarded. An optional argument to shift specifies the number of positions to shift (and the number of arguments to discard); the default is 1.

The following demo_shift script is called with three arguments. Double quotation marks around the arguments to echo preserve the spacing of the output. The program displays the arguments and shifts them repeatedly until no more arguments are left to shift:

```
$ cat demo_shift
echo "arg1= $1\targ2= $2\targ3= $3"
shift
echo "arg1= $1\targ2= $2\targ3= $3"
shift
echo "arg1= $1\targ2= $2\targ3= $3"
shift
echo "arg1= $1\targ2= $2\targ3= $3"
shift
$ ./demo_shift alice helen zach
arg1= alice\targ2= helen\targ3= zach
arg1= helen\targ2= zach
arg1= zach\targ2=\targ3=
arg1=\targ2=\targ3=
```

Repeatedly using shift is a convenient way to loop over all command-line arguments in shell scripts that expect an arbitrary number of arguments. See page 959 for a shell script that uses shift.

# set: INITIALIZES COMMAND-LINE ARGUMENTS

When you call the set builtin with one or more arguments, it assigns the values of the arguments to the positional parameters, starting with $1. The following script uses set to assign values to the positional parameters $1, $2, and $3:

```
$ cat set_it
set this is it
echo $3 $2 $1
$ ./set_it
it is this
```

Combining command substitution (page 362) with the set builtin is a convenient way to get standard output of a command in a form that can be easily manipulated in a shell script. The following script shows how to use date and set to provide the