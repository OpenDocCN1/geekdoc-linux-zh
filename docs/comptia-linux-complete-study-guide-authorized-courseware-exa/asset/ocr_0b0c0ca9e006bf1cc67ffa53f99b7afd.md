1 and 10. You can use a `for` loop beginning `for x in `seq 10`` to have the loop execute 10 times, with the value of x incrementing with each iteration. If you pass just one parameter to seq, it interprets that number as an ending point, with the starting point being 1. If you pass three values to seq, it interprets them as a starting value, an increment amount, and an ending value.

Another type of loop is the `while` loop, which executes for as long as its condition is true. The basic form of this loop type is like this:

```
while [ condition ]
do
    commands
done
```

The `until` loop is similar in form, but it continues execution for as long as its condition is *false*—that is, until the condition becomes true.

# ## Using Functions

A *function* is a part of a script that performs a specific sub-task and that can be called by name from other parts of the script. Functions are defined by placing parentheses after the function name and enclosing the lines that make up the function within curly braces:

```
myfn() {
    commands
}
```

The keyword *function* may optionally precede the function name. In either event, the function is called by name as if it were an ordinary internal or external command.

Functions are very useful in helping to create modular scripts. For instance, if your script needs to perform half a dozen distinct computations, you may place each computation in a function and then call them all in sequence. Listing 9.6 demonstrates the use of functions in a simple program that copies a file but aborts with an error message if the target file already exists. This script accepts a target and a destination filename and must pass those filenames to the functions.

# **Listing 9.6: A Script Demonstrating the Use of Functions**

```
#!/bin/bash

doit() {
    cp $1 $2
}

function check() {
```