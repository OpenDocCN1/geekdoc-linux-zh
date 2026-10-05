
# Chapter 11 • Creating Scripts

(described shortly), variables become even more powerful, because then your script can perform one action when one is met and another in some other case. For instance, a script that installs software can check free disk space and abort the installation if insufficient disk space is available.

In addition assigning variables with the assignment operator (=), you can read variables from standard input by using read, as in response to input for subsequent access as $variable. This method of variable assignment is useful for scripts that must interact with users. For instance, instead of reading the username from the command line. Listing 11.2 shows the result. To use this script, you type its name without typing a username on the command line. The script will then prompt for a username and, after you enter one, the script will attempt to create an account with that name.

### Certification Objective

LISTING 11.4: Modified version of Listing 11.2 that employs user interaction

```
#!/bin/bash
echo -n "Enter a username:"
read name
useradd -m $name
mkdir -p /shared/$name
chown $name:users /shared/$name
chmod 775 /shared/$name
ln -s /shared/$name /home/$name/shared
chown $name:users /home/$name/shared
```

One special type of variable is an environment variable, which is assigned and accessed just like a shell variable. The difference is that the script or command sets an environment variable uses Bash's export command to make the value of the variable accessible to programs launched from the shell or shell script that made the assignment. In other words, you can set an environment variable in one script and use it in another script the first script launches. Environment variables are often set in shell startup scripts, but the scripts you use access for. If your script calls X programs, it might check for the presence of a valid $DISPLAY environment variable and abort if it finds that this variable isn't set. By convention, environment variable names are all uppercase, whereas nonenvironment shell script variables are all lowercase or mixed case.

One special variable deserves mention: $?. This holds the exit status (or return value) of the most recently executed command. Most programs return a value of 0 when they terminate normally and return another value to specify errors. You can display this value with echo or use it in a conditional expression (described next) to have your script perform special handling.

Consult a program's man page to learn the meanings of its return values.

![](img/77662199428609b7662c8dc9c0e45c10_239_0.png)

# Using Conditional Expressions

Scripting languages support several types of conditional expressions. These enable a script to perform one of several actions contingent on a particular condition—typically the value of a variable. One common command that uses conditional expressions is if, which allows the system to take one of two actions depending on whether a certain condition is true. The if keyword's conditional expression appears in brackets after the if and can take many forms. For instance, -f file is true if file exists and is a regular file; -s file is true if file exists and has a size greater than 0; string1 == string2 is true if the two strings have the same values.

Conditionals may be combined together with the logical and (&&) or logical or (||) operators. When conditionals are combined with && both sides of the operator must be true for the condition as a whole to be true. When || is used, if either side of the operator is true, the condition as a whole is true.

To understand the use of conditionals, consider the following code fragment:

```
if [ -s /tmp/tempstuff ]
then
  echo "/tmp/tempstuff found, aborting"
  exit
fi
```

This fragment causes the script to exit if the file /tmp/tempstuff is present. The then keyword marks the beginning of a series of lines that execute only if the conditional is true, and fi (if backward) marks the end of the block. Such code may be useful if the script creates and then deletes this file, because its presence indicates that a previous run of the script didn't succeed or is still underway.

An alternative form for a conditional expression uses the test keyword rather than square brackets around the condition:

```
if test -s /tmp/tempstuff
```

You can also test a command's return value by using the command as the condition:

```
if [ command ]
then
  additional-commands
fi
```

In this example, the additional-commands will be run only if command completes successfully. If command returns an error code, the additional-commands won't be run.

# Chapter 11 - Creating Scripts

Conditional expressions may be expanded by use of the else clause:

```
if [ conditional-expression ]
then
    commands
else
    other-commands
```

Code of this form uses either commands or other-commands to execute, depending on the evaluation of conditional-expression. This is useful if something should happen in a part of the program, but precisely what should happen on a certain condition. For instance, you might want to launch one of two file-archiving programs depending on a user's input.

What do you do if more than two outcomes are possible—for instance, if a user may provide any one of four possible inputs? You can nest if/then/else clauses, but this gets awkward quickly. A cleaner approach is to use case:

```
case word in
    pattern1 command(s);
    pattern2 command(s);
    ...
esac
```

For a statement, a word is likely to be a variable, and each pattern is a possible value of that variable. The patterns can be expanded like filenames, using the wildcards and expansion rules (* to stand for any string, instance). You can match an arbitrary number of patterns in this way. Each set of commands must end with a double semicolon (;;), and the case statement as a whole ends in the string esac (case backward).

Upon execution, bash executes the commands associated with the first pattern to match the word. Execution then jumps to the line following the esac statement; any intervening commands don't execute. If no patterns match the word, no code the case statement executes. If you want to have a default condition, use * as the final pattern; this pattern matches any word, so its commands will execute if no other pattern matches.

# Using Loops

Conditional expressions are sometimes used in loops. Loops are structures that tell the script to perform the same task repeatedly until a particular condition is met (or until some condition is no longer met). For instance, Listing 11.5 shows a loop that plays all the .wav audio files in a directory.

LISTING 11.5: A script that executes a command on every matching file in a directory

```
#!/bin/bash
for d in `ls *.wav`; do
 aplay $d
done
```

The for loop used as here executes once for every item in the list generated by ls *.wav. Each of those items (filenames) is assigned in turn to the $d variable and is passed to the aplay command.

The seq command can be useful in creating loops (and in other ways too). This command generates a list of numbers starting from its first argument and continuing to its last one. For instance, typing `seq 1 10` generates 10 lines, each with a number between 1 and 10. You can use a for loop beginning for x `seq 1 10` to have the loop execute 10 times, with the value of x incrementing with each iteration. If you pass just one parameter to seq, it interprets that as an ending point, with the starting point being 1. If you pass three values to seq, it interprets them as a starting value, an increment amount, and an ending value.

Another type of loop is the while loop, which executes for long as its condition is true. The basic form of this loop type is as follows:

```
while [ condition ]
do
 commands
done
```

The until loop is similar in form, but it continues execution as long as its condition is false—that is, until the condition becomes true.

# Using Functions

A function is a part of a script that performs a specific subtask and that can be called by name from other parts of the script. Parenting parentheses after the function name and enclosing the lines that make up the function with curly braces is how functions are defined:

```
myfn() {
 commands
}
```
