
functions, and sophisticated condition testing. Shell scripts are capable of handling everything from simple one-line commands to something as complex as starting up your Fedora system.

In fact, as you will read in this chapter, Fedora does just that. It uses shell scripts (/etc/rc.d/rc.sysinit and /etc/rc) to check and mount all your filesystems, set up your consoles, configure your network, launch all your system services, and eventually provide you with your login screen. While there are nearly a dozen different shells available in Fedora, the default shell is called bash, the Bourne-Again Shell.

### Executing and debugging shell scripts

One of the primary advantages of shell scripts is that they can be opened in any text editor to see what they do. A big disadvantage is that shell scripts often execute more slowly than compiled programs. There are two basic ways to execute a shell script:

-   The filename is used as an argument to the shell (as in `bash myscript`). In this method, the file does not need to be executable; it just contains a list of shell commands. The shell specified on the command line is used to interpret the commands in the script file. This is most common for quick, simple tasks.

-   The shell script may also have the name of the interpreter placed in the first line of the script preceded by `#!` (as in `#!/bin/bash`), and have its execute bit set (using `chmod +x`). You can then run your script just like any other program in your path simply by typing the name of the script on the command line.

> **CROSS-REFERENCE:** See Chapter 4 for more details on `chmod` and read/write/execute permissions.

When scripts are executed in either manner, options to the program may be specified on the command line. Anything following the name of the script is referred to as a command-line argument.

As with writing any software, there is no substitute to clear and thoughtful design and lots of comments. The pound sign (`#`) prefaxes comments and can take up an entire line or exist on the same line as script code. It’s best to implement more complex shell scripts in stages, making sure the logic is sound at each step before continuing. Here are a few good, concise tips to make sure things are working as expected during testing:

-   Place an `echo` statement at the beginning of lines within the body of a loop. That way, rather than executing the code, you can see what will be executed without making any permanent changes.

-   To achieve the same goal, you could place dummy `echo` statements throughout the code. If these lines get printed, you know the correct logic branch is being taken.

-   You could use `set -x` near the beginning of the script to display each command that is executed or launch your scripts using `bash -x myscript`.

## Understanding shell variables

Often within a shell script, you want to reuse certain items of information. During the course of processing the shell script, the name or number representing this information may change. To store information used by a shell script in such a way that it can be easily reused, you can set variables. Variable names within shell scripts are case-sensitive and can be defined in the following manner:

```
NAME=value
```

The first part of a variable is the variable name, and the second part is the value set for that name. Variables can be assigned from constants, like text or numbers. This is useful for initializing values or saving lots of typing for long constants. Here are examples where variables are set to a string of characters (`CITY`) and a numeric value (`PI`):

```
CITY="Springfield"
PI=3.14159265
```

Variables can contain the output of a command or command sequence. You can accomplish this by enclosing the command in backticks (`` ` ``).

This is a great way to get information that can change from computer to computer or from day to day. Here we set the output of the `uname -n` command to the `MACHINE` variable. Then we use parentheses to set `NUM_FILES` to the number of files in the current directory by piping (`|`) the output of the `ls` command to the word count command (`wc -l`).

```
MACHINE=`uname -n`
NUM_FILES=`/bin/ls | wc -l`
```

Variables can also contain the value of other variables. This is useful when you have to preserve a value that will change so you can use it later in the script. Here `BALANCE` is set to the value of the `CurBalance` variable.

```
BALANCE="$CurBalance"
```

> **NOTE:** When assigning variables, use only the variable name (for example, `BALANCE`). When referenced, meaning you want the *value* of the variable, precede it with a dollar sign (as in `$CurBalance`).

## Special Shell Variables

There are special variables that the shell assigns for you. The most commonly used variables are called the *positional parameters* or *command line arguments* and are referenced as `$0`, `$1`, `$2`, `$3` ... `$n`. `$0` is special and is assigned the name used to invoke your script; the remainder are assigned the values of the parameters passed on the command line. For instance, if the shell script named `myscript` were called as:

```
myscript foo bar
```

the positional parameter `$0` would be `myscript`, `$1` would be `foo`, and `$2` would be `bar`. Another variable, `$#`, tells you how many parameters your script was given. In our example, `$#` would be `2`. Another particularly useful special shell variable is `$?`, which receives the exit status of the last command executed. Typically, a value of zero means everything is okay, and anything other than zero indicates an error of some kind. For a complete list of special shell variables, refer to the bash man page.

## Parameter expansion in bash

As mentioned earlier, if you want the value of a variable, you precede it with a `$` (for example, `$CITY`). This is really just a shorthand for the notation `${CITY}`; curly braces are used when the name of the parameter needs to be placed next to other text without a space. Bash has special rules that allow you to expand the value of a variable in different ways. Going into all the rules is probably a little overkill for a quick introduction to shell scripts, but Table 12-1 presents some common constructs that you’re likely to see in bash scripts you find on your Fedora box.

### Table 12-1: Examples of bash Parameter Expansion

| Construction | Meaning |
| :--- | :--- |
| `${var:-value}` | If variable is unset or empty, expand this to value |
| `${var?pattern}` | Chop the shortest match for pattern from the front of var's value |
| `${var#pattern}` | Chop the longest match for pattern from the front of var's value |
| `${var%pattern}` | Chop the shortest match for pattern from the end of var's value |
| `${var%pattern}` | Chop the longest match for pattern from the end of var's value |

Try typing the following commands from a shell to test out how parameter expansion works:

```
$ THIS="Example"
$ THIS=${THIS:- "Not Set"}
$ THAT=${THAT:- "Not Set"}
$ echo $THIS
Example
$ echo $THAT
Not Set
```

In the examples here, the `THIS` variable is initially set to the word `Example`. In the next two lines, the `THIS` and `THAT` variables are set to their current values or to `Not Set`, if they are not currently set. Notice that because we just set `THIS` to the string `Example`, when we `echo` the value of `THIS` it appears as `Example`. However, since `THAT` was not set, it appears as `Not Set`.

> **NOTE:** For the rest of this section, I show how variables and commands may appear in a shell script. To try out any of those examples, however, you can simply type them into a shell as shown in the previous example.

In the following example, set `MYFILENAME` to `/home/digby/myFile.txt`. Next, the `FILE` variable is set to `myFile.txt` and `DIR` is set to `/home/digby`. In the `NAME` variable, the file name is cut down to simply `myFile`, then in the `EXTENSION` variable the file extension is set to `txt`. (To try these out, you can type them at a shell prompt as we did with the previous example, then `echo` the value of each variable to see how it is set.)

```
MYFILENAME="/home/digby/myFile.txt"
FILE=$( ${MYFILENAME##*/ } )    #FILE becomes  "myFile.txt"
DIR=$( ${MYFILENAME%/*} )        #DIR becomes "/home/digby"
NAME=$( ${FILE%.*} )             #NAME becomes "myFile"
EXTENSION=$( ${FILE#.*} )        #EXTENSION becomes "txt"
```

## Performing arithmetic in shell scripts

Bash used *untyped* variables, meaning it normally treats variables as strings or text, but can change them on the fly if you want to do. Unless you tell it otherwise with `declare`, your variables are just a bunch of letters to bash. But when you start trying to do arithmetic with them, bash will convert them to integers if it can. This makes it possible to do some fairly complex arithmetic in bash.

Integer arithmetic can be performed using the built-in `let` command or through the external `expr` or `bc` commands. After setting the variable `BIGNUM` value to 1024, the three commands that follow would all store the value 64 in the `RESULT` variable:

```
BIGNUM=1024
let RESULT=$BIGNUM / 16
RESULT=`expr $BIGNUM / 16`
RESULT=`echo "$BIGNUM / 16" | bc -l`
```

> **NOTE:** While most elements of shell scripts are relatively freeform (where whitespace, such as spaces or tabs, is insignificant), both `let` and `expr` are particular about spacing. The `let` command insists on no spaces between each operand and the mathematical operator, whereas the syntax of the `expr` command requires whitespace between each operand and its operator. In contrast to those, `bc` isn't picky about spaces, but can be trickier to use because it does floating-point arithmetic.

To see a complete list of the kinds of arithmetic you can perform using the `let` command, type `help let` at the bash prompt.

## Using programming constructs in shell scripts

One of the features that make shell scripts so powerful is that their implementation of looping and conditional execution constructs is similar to those found in more *complex* scripting and
