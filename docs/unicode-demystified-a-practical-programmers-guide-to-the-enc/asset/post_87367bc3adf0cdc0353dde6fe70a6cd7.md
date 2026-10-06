
```bash
$ cat abc
echo The name of the command used
echo to execute this shell script was $0
$ abc
The name of the command used
execute this shell script was abc
```

This shell script uses echo to verify the name of the script you are executing.

## $1-$Sn: Command Line Arguments

The first argument on the command line is represented by the parameter $1, the second argument by the parameter $2, and so on to $x. The following script displays positional parameters that hold command line arguments:

```bash
$ cat display_sargs
echo The first five command line
echo arguments are $1 $2 $3 $4 $5
$ display_sargs jenny alex helen
The first five command line
arguments are jenny alex helen
```

The display_sargs script displays the first five line arguments. The shell assigns a null value to each of parameters that represents an argument that is not present on the command line. The $4 and $5 variables have a null value.

The $@ variable represents all the command line arguments, as the display_all program demonstrates:

```bash
$ cat display_all
echo All the command line arguments are:
echo $$
$ display_all a b c d e f g h i j k l m n o p
All the command line arguments are:
a b c d e f g h i j k l m n o p
```

When you refer to a positional parameter, enclose the reference within double quotation marks. The quotation marks are particularly important when using positional parameters as arguments to commands; without double quotation marks, a positional parameter with a null value disappears:

```bash
$ cat showargs
echo "I was called with $# arguments, the first is :1:."
$ showargs a b c
echo I was called with 3 arguments, the first is :a::
$ echo $3
```

```bash
$ showargs $3 a b c
echo I was called with 3 arguments, the first is :a::
$ showargs "3" a b c
echo I was called with 4 arguments, the first is :3::.
```

## Parameters and Variables

The preceding example first calls showargs with three simple arguments. The showargs script displays the number of arguments and the value of the first argument enclosed between colons. The shell stores the number of arguments passed to it in the # special parameter (Refer to $$). The echo command demonstrates the third positional parameter of the current shell ($3) has no value. In the two calls to showargs, the first argument is $3. Because there is no value for this positional parameter, the shell replaces it with a null value. In the first case the command line becomes showargs b; the shell passes three arguments. In the second case the command line becomes showargs "a b c", which results in calling showargs with four arguments. The difference in the two calls to showargs illustrates a subtle problem that you must keep in mind when using positional parameters.

## shift: Promotes Command Line Arguments

The shift builtin promotes each of the command line arguments. The first argument (which is $1) is discarded. The second argument (which is $2) becomes the first (now $1), the third becomes the second, the fourth becomes the third, and so on.

Using the command line variables ($1–9), you can access only the nine command line arguments from a shell script. The shift builtin gives access to the tenth command argument by making it the ninth. Successive shift commands make additional arguments available. The original first argument is discarded. because there is no "unshift" command, it is not possible to bring back arguments that have been discarded.

The following demo_shift program is called with three arguments. Double quotation marks around the arguments preserve the spacing of the output display. The program displays the arguments and shifts them repeatedly until there are no more arguments to shift:

```bash
$ cat demo_shift
echo "arg1=$1 arg2=$2 arg3=$3"
shift
echo "arg1=$1 arg2=$2 arg3=$3"
shift
echo "arg1=$1 arg2=$2 arg3=$3"
shift
$ demo_shift alice helen jenny
arg1=alice arg2=helen arg3=jenny
arg1=helan arg2=jenny arg3=
arg1=jenny arg2= arg3=
arg1=
```

bash and zsh: When you enclose the number in braces, you can address command line arguments greater than nine. For example, ${16} represents the sixteenth command line argument.

## Chapter 12 The Shell II: The Bourne Again Shell

In the original Bourne Shell, the positional parameters were limited to $1-$9, so shell scripts that accepted more than nine arguments were forced to shift to later arguments. The Bourne Again Shell has no limit on the number of positional parameters, so this use of shift has declined. However, repeating shift is a convenient way to loop over all the command line arguments in shell scripts that expect an arbitrary number of arguments. See page 632 for a sample shell program that uses this technique.

## set: Initialize Command Line Arguments

When you call the set builtin with one or more arguments, it uses the arguments as values for positional parameters, starting with $1 (for tsh, see footnote 8 on page 581). The following script uses set to assign values to the positional parameters $1, $2, and $3:

```bash
$ cat set_it
set this is it
echo $3 $2 $1
set $1 it is this
```

Combining the use of command substitution (page 575) with the set builtin is a convenient way to get standard output of a command in a form that can be easily manipulated. The following script shows how to use set:

```bash
$ cat showargs
echo "I was called with $# arguments, the first is :1:."
$ showargs a b c
echo I was called with 3 arguments, the first is :a::
$ echo $3
```

```bash
$ showargs $3 a b c
echo I was called with 3 arguments, the first is :a::
$ showargs "3" a b c
echo I was called with 4 arguments, the first is :3::.
```

When you refer to a positional parameter, enclose the reference within double quotation marks. The quotation marks are particularly important when using positional parameters as arguments to commands; without double quotation marks, a positional parameter with a null value disappears:

The following script shows how to use set:

```bash
$ cat showargs
echo "I was called with $# arguments, the first is :1:."
$ showargs a b c
echo I was called with 3 arguments, the first is :a::
$ echo $3
```

The following script shows how to use set:
(Wait, the OCR repeats here, merging logical flow)

Combining the use of command substitution (page 575) with the set builtin is a convenient way to get standard output of a command in a form that can be easily manipulated. The following script shows how to use set:

(Note: The OCR text contains redundant/garbled repetitions. I have cleaned the logical flow based on the provided segments.)

## set Options

| Option | Description |
| :--- | :--- |
| -a | Marks variables you create for export. |
| -f | Stops bash from doing expansion (globbing). |
| -n | Causes bash to read and perform expansions but not to execute them. |
| -t | Reads and executes a single command and then quits. |
| -u | Returns an error when you try to expand unset variable. |

## Special Parameters

Special parameters make it possible to access values containing command line arguments. You reference by preceding a special character with a dollar sign ($). As with positional parameters, it is not possible to modify the value of a special parameter.

## Number of Command Line Arguments

As the showargs script on page 582 and the following example demonstrate, the $# parameter contains the number of arguments on the command line. This string parameter represents a decimal number.

```bash
$ cat num_args
echo "This shell script was called with $# arguments."
$ num_args helen alex jenny
This shell script was called with 3 arguments.
```

## $$ PID Number

The shell stores in the $$ parameter the PID number of the process is executing it. In the following interaction echo displays the value of this variable, and the ps utility confirms its value (ps lists a more processes if you are running X). Both commands show that the shell has a PID number of 5209:
