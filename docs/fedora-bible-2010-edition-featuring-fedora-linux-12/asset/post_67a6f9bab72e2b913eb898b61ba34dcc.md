
# Understanding shell variables

Often within a shell script, you want to reuse certain items of information. During the course of processing the shell script, the name or number representing this information may change. To store information used by a shell script in such a way that it can be easily reused, you can set variables. Variable names within shell scripts are case-sensitive and can be defined in the following manner:

```
NAME=value
```

The first part of a variable is the variable name, and the second part is the value set for that name. Be sure that the `NAME` and `value` touch the equal sign, without any spaces. Variables can be assigned from constants, such as text or numbers. This is useful for initializing values or saving lots of typing for long constants. Here are examples where variables are set to a string of characters (`CITY`) and a numeric value (`PI`):

```
CITY="Springfield"
PI=3.14159265
```

In addition to constants holding things not likely to change (such as the mathematical definition of pi), you can also use variables as placeholders for the current items of interest, such as the filename to process, the directory you want to back up, and so on.

Variables can contain the output of a command or command sequence. You can accomplish this by preceding the command with a dollar sign and open parenthesis, and following it with a closing parenthesis. For example, `MYDATE=$(date)` assigns the output from the `date` command to the `MYDATE` variable. Enclosing the command in backticks (`` ` ``) can have the same effect.

> **NOTE:** Keep in mind that characters such as the dollar sign ($), backtick (` ` `), asterisk (*), exclamation point (!), and others have special meaning to the shell, as you will see as you proceed through this chapter. To use those characters in an option to a command, and not have the shell use its special meaning, you need to precede that character with a backslash (\) or surround it in quotes. One place you will encounter this is in files created by Windows users that might include spaces, exclamation points, or other characters. In Linux, to properly interpret a file named `my big! file`, you either need to surround it in double quotes or type: `my\ big\! file\!`

These are great ways to get information that can change from computer to computer or from day to day. The following example sets the output of the `uname -r` command to the `MACHINE` variable. Then I use parentheses to set `NUM_FILES` to the number of files in the current directory by piping ( `|` ) the output of the `ls` command to the word count command (`wc -l`).

```
MACHINE=`uname -n`
NUM_FILES=$( /bin/ls | wc -l )
```

Variables can also contain the value of other variables. This is useful when you have to preserve a value that will change so you can use it later in the script. Here, BALANCE is set to the value of the CurBalance variable.

```
BALANCE="$CurBalance"
```

The double quotes ("") tell bash to substitute the value of the variable CurBalance. If you used single quotes (''), the shell would merely display the text $CurBalance as shown below:

```
$ CurBalance=5.00
$ echo "$CurBalance"
5.00

$ echo '$CurBalance'
$CurBalance
```

> **NOTE:** When assigning variables, use only the variable name (for example, BALANCE). When referenced, meaning you want the value of the variable, precede it with a dollar sign (as in $CurBalance). The result of the latter is that you get the value of the variable and not the variable name itself.

# Special shell variables

There are special variables that the shell assigns for you. The most commonly used variables are called the *positional parameters or command line arguments* and are referenced as $0, $1, $2, $3 . . . $n. $0 is special and is assigned the name used to invoke your script; the others are assigned the values of the parameters passed on the command line. For instance, if the shell script named myscript were called as

```
myscript foo bar
```

the positional parameter $0 would be myscript, $1 would be foo, and $2 would be bar. The following script, myscript, shows this:

```
#!/bin/sh

echo "0: $0"
echo "1: $1"
echo "2: $2"

echo "You passed $# arguments to $0"
```

When you run this script with the command-line parameters of foo and bar shown above, you should see output like the following:

```
sh myscript foo bar
0: myscript
1: foo
2: bar
You passed 2 arguments to myscript
```

Another variable, $# , tells you how many parameters your script was given. In our example, $# would be 2. Another particularly useful special shell variable is $?, which receives the exit status of the last command executed. Typically, a value of zero means everything is okay, and anything other than zero indicates an error of some kind. For a complete list of special shell variables, refer to the bash man page.

# Parameter expansion in bash

As mentioned earlier, if you want the value of a variable, you precede it with a $ (for example, ${CITY}). This is really just shorthand for the notation ${CITY}; curly braces are used when the value of the parameter needs to be placed next to other text without a space. Bash has special rules that allow you to expand the value of a variable in different ways. Going into all the rules is probably a little overkill for a quick introduction to shell scripts, but Table 11-1 presents some common constructs that you're likely to see in bash scripts you find on your Fedora box.

## Table 11-1: Examples of bash Parameter Expansion

| Construction | Meaning |
|---|---|
| ${var:-value} | If variable is unset or empty, expand this to value. |
| ${var#pattern} | Chop the shortest match for pattern from the front of var's value. |
| ${var##pattern} | Chop the longest match for pattern from the front of var's value. |
| ${var%pattern} | Chop the shortest match for pattern from the end of var's value. |
| ${var%%pattern} | Chop the longest match for pattern from the end of var's value. |

Try typing the following commands from a shell to test how parameter expansion works:

```
$ FOOD="Pizza"
$ FOOD=${FOOD:-"Not Set"}
$ SNACK=${ SNACK:-"Not Set"}
$ echo $FOOD
Pizza
$ echo $ SNACK
Not Set
```

In the examples here, we set the FOOD variable to Pizza in the first line. In the second line, we give FOOD a default value, Not Set , if necessary. In this case the value of FOOD is still Pizza since it has a value. The third line sets a default value for the variable $SNACK. Because we never gave SNACK a value, it gets the default, Not Set in this case.

> **NOTE:** For the rest of this section, I show how variables and commands may appear in a shell script. To try out any of those examples, however, you can simply type them into a shell as shown in the previous example.

In the following example, MYFILENAME is set to `/home/digby/myfile.txt`. Next, the FILE variable is set to `myfile.txt` and DIR is set to `/home/digby`. In the NAME variable, the file name is cut down to simply `myfile`; then in the EXTENSION variable the file extension is set to `txt`. (To try these out, you can type them at a shell prompt as in the previous example, and then echo the value of each variable to see how it is set.)

```
MYFILENAME="/home/digby/myfile.txt"
FILE=${MYFILENAME##*/}             #FILE becomes "myfile.txt"
DIR=${MYFILENAME%/*}              #DIR becomes "/home/digby"
NAME=${FILE%.*}                   #NAME becomes "myfile"
EXTENSION=${FILE#*.}              #EXTENSION becomes "txt"
```

# Performing arithmetic in shell scripts

Bash uses untyped variables, meaning it normally treats variables as strings or text, but can change them on-the-fly if you want it to. Unless you tell it otherwise with declare, your variables are just a bunch of letters to bash. But when you start trying to do arithmetic with them, bash will convert them to integers if it can. This makes it possible to do some fairly complex arithmetic in bash.

Integer arithmetic can be performed using the built-in let command or through the external expr or bc commands. After setting the variable BIGNUM variable to 1024, the three commands that follow would all store the value 64 in the RESULT variable. (The command using bc will set the RESULT variable to 64.00000000000000000000.)

The last command gets a random number between 0 and 10 and echoes the results back to you.

```
BIGNUM=1024
let RESULT=$BIGNUM/16
RESULT=`expr $BIGNUM / 16` 
RESULT=`echo "$BIGNUM / 16" | bc -l` 
let foo=$RANDOM%10; echo $foo
```

You can also use arithmetic in line with the following double-parenthesis syntax:

```
$ RESULT=$( (10*20) )
$ echo $RESULT
200
```
