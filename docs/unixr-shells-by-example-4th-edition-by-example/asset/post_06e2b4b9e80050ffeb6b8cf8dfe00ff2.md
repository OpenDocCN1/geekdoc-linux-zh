
## Table 14.7 Debugging Options

| Command | Option | What It Does |
|---|---|---|
| `bash -x scriptname` | Echo option | Displays each line of script after variable substitutions and before execution. |
| `bash -v scriptname` | Verbose option | Displays each line of script before execution, just as you typed it. |
| `bash -n scriptname` | Noexec option | Interprets but does not execute commands. |
| `set -x` | Turns on echo | Traces execution in a script. |
| `set +x` | Turns off echo | Turns off tracing. |

**EXAMPLE 14.69**

```bash
(The Script)
#!/bin/bash
# Scriptname: todebug

name="Joe Shmoe"
if [ "$name" == "Joe Blow" ]
then
    printf "Hello $name\n"
fi

declare -i num=1
while (( num < 5 ))
do
    let num+=1
done
printf "The total is %d\n", $num

(The Output)
$ bash -x todebug
+ name=Joe Shmoe
+ [[ Joe Shmoe == \J\o\e\ \B\l\o\w ]]
+ declare -i num=1
+ (( num < 5 ))
+ let num+=1
+ (( num < 5 ))
+ let num+=1
+ (( num < 5 ))
+ let num+=1
```

### EXAMPLE 14.69 (CONTINUED)

```
+ (( num < 5 ))
+ let num+=1
+ (( num < 5 ))
+ printf 'The total is %d\n' 5
The total is 5
```

## EXPLANATION

- 1. The script is called todebug. You can watch the script run with the -x switch turned on. Each iteration of the loop is displayed and the values of variables are printed as they are set and when they change.
- 2. Bash is invoked with the -x option. Echoing is turned on. Each line of the script will be displayed to the screen prepended with a plus sign (+). Variable substitution is performed before the line is displayed. The result of the execution of the command appears after the line has been displayed.

## 14.10 The Command Line

### 14.10.1 Processing Command-Line Options with getopts

If you are writing scripts that require a number of command-line options, positional parameters are not always the most efficient. For example, the UNIX ls command takes a number of command-line options and arguments. (An option requires a leading dash; an argument does not.) Options can be passed to the program in several ways: ls -lafl, ls -i -a -l -f, ls -ia -f and so forth. If you have a script that requires arguments, positional parameters might be used to process the arguments individually, such as ls -l -i -f. Each dash option would be stored in $1, $2, and $3, respectively. But, what if the user listed all of the options as one dash option, as in ls -l1f? Now the -l1f would all be assigned to $1 in the script. The getopts function makes it possible to process command-line options and arguments in the same way they are processed by the ls program. The getopts function will allow the runt program to process its arguments using any variety of combinations.

## EXAMPLE 14.70

```
(The Command Line )
1 $ runt -x -n 200 filex
2 $ runt -xn200 filex
3 $ runt -xy
```

### EXAMPLE 14.70 (CONTINUED)

```
4  $ runit -yx -n 30
5  $ runit -n250 -xy filey
( any other combination of these arguments )
```

## EXPLANATION

- 1 The program runit takes four arguments: x is an option, n is an option requiring a number argument after it, and filex is an argument that stands alone.
- 2 The program runit combines the options x and n and the number argument 200; filex is also an argument.
- 3 The program runit is invoked with the x and y options combined.
- 4 The program runit is invoked with the y and x options combined; the n option is passed separately, as is the number argument, 30.
- 5 The program runit is invoked with the n option combined with the number argument, the x and y options are combined, and the filey is separate.

Before getting into all the details of the runit program, we examine the line from the program where getopts is used to see how it processes the arguments.

## EXAMPLE 14.71

(A line from the script called runit)

```
while getopts :xyn: name
```

## EXPLANATION

x, y, and n are the options. In this example the first option is preceded by a colon. This tells getopts to use silent error reporting. If there is a colon after one of the options, the option expects an argument separated from it by whitespace. An argument is a word that does not begin with a dash. -n requires an argument.

Any options typed at the command line must begin with a dash.

Any options that do not contain a dash tell getopts that the option list has ended.

Each time getopts is called, it places the next option value it finds in the variable name. (You can use any variable name here.) If an illegal argument is given, name is assigned a question mark.

# Sample getopts Scripts. The following examples illustrate how getopts processes arguments.
