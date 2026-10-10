
The `list` command ensures that we always get a well-formed three-element list, which is therefore guaranteed to be a well-formed script with `set` followed by exactly two arguments.

## Control Structures

Tcl has the usual control structures found in modern languages. The implementation of the control structures is unusual in that Tcl control structures are normal commands, some of whose arguments happen to be Tcl scripts.

### if

The `if` command looks something like the following:

```
if test1 body1 ?elseif test2 body2...? ?else bodyn?
```

Each `test` is evaluated in turn as an expression. If the result is non-zero, Tcl executes the corresponding `body` and skips the remaining `tests` and `bodies`. If all `tests` are `false` and the `else` clause is present, Tcl executes the final `body`.

The result of an `if` command is the result of whichever body was executed or the empty string if no body was executed.

Consider the following example:

```
if { $a > 0 } {
  set answer Positive
  set b $a
} elseif { $a == 0 } {
  set answer Zero
  set b $a
} else {
  set answer Negative
  set b [expr -1 * $a]
}
```

In the example, `answer` is set to `Positive`, `Zero`, or `Negative`, depending on the value of `a`. In addition, `b` is set to the absolute value of `a`.

### while

The `while` command looks like the following:

```
while test body
```

The `while` command evaluates `test` as an expression. If the result is non-zero, the `while` command evaluates `body` as a Tcl script. This repeats until `test` becomes `false`.

```
set i 0
set total 0

while { $i < 10 } {
incr i
incr total $i
}
set total
```

This adds all the numbers from 1 to 10, leaving the result in *total*.

The *while* command returns the empty string.

### for

The *for* command looks a bit like its C counterpart:

```
for init test update body
```

First, Tcl evaluates *init* as a script. Next, Tcl evaluates *test* as an expression. If it returns *true*, Tcl evaluates *body* as a script. After that, Tcl evaluates *update* as a script. The process repeats from the evaluation of *test* until *test* returns *false*.

The following is the previous example written as a *for* loop:

```
for {set i 1; set total 0} {$i <= 10} {incr i} {
incr total $i
}
set total
```

### foreach

The *foreach* command iterates over a list. In its simplest form, it looks like the following:

```
foreach var list body
```

It assigns *var* successive elements of *list*, executing *body* after each assignment. The following example adds the numbers 22, 75, 41, and 3:

```
set total 0
foreach number { 22 75 41 3 } {
incr total $number
}
set total
```

You can make the first argument a list of variables. In this case, *foreach* consumes as many elements from the list as there are variables for each iteration, assigning them to matching variables. For example, the following code computes the value of 22*75* + 41*3*:

```
set total 0
foreach {x y} { 22 75 41 3 } {
incr total [expr $x * $y]
}
set total
```

Finally, you can supply several lists and variable lists, and they are stepped in parallel. The following example computes 22*75*4 + 41*3*8:

```tcl
set total 0
foreach {x y} { 22 75 41 3} z {4 8} {
    incr total [expr $x * $y * $z]
}
set total
```

See the manual page foreach(n) for more details.

### break and continue

Within the body of a loop, you can use the **break** and **continue** commands. The **break** command stops execution of the loop body and terminates the loop completely. Execution continues with the command following the loop.

The **continue** statement terminates execution of the loop body and starts a new iteration. For **while** loops, this means that **test** is re-evaluated. For **for** loops, **update** is executed and **test** re-evaluated. For **foreach**, the next loop iteration is performed.

### switch

The **switch** command is a more compact way of encoding a series of **if...** **else if...** **else** commands.

The following is an example of **switch**:

```tcl
switch $a {
    1 { incr t1 }
    2 { incr t2 }
    default {incr tx}
}
```

In this example, if a holds the value 1, t1 is incremented. If it is 2, t2 is incremented; otherwise, tx is incremented.

The **switch** command has other options and capabilities; see switch(n) for details. The return value of **switch** is the value of whichever script was executed or the empty string if no script was executed.

### source

The **source** command takes a single argument, which is the name of the file. The file is read and evaluated as a Tcl script. The return value is the value of the last-executed Tcl command from the file.

For example, to execute the Tcl commands in **file.tcl**, use
**source** **file.tcl**

### eval

The *eval* command concatenates all of its arguments (as if with *concat*) and executes the result as a Tcl script. This is used to build up an execute scripts, or force another round of substitution.

Consider the following example:

```
set a 1
set varName "a"
set b ${varName}
eval set c ${varName}
set c
```

In this example, the arguments to the *eval* command are *set*, *c*, and *$a*. The *eval* command forces another round of parsing, so *c* is set to 1. However, because we didn’t use *eval*, *b* is set to the string "*${a}*".

# Procedures

While most built-in Tcl commands are executed by C code in the Tcl interpreter, you can write your own commands in Tcl and have them executed just as if they were built-in commands.

### proc

The *proc* command defines a procedure:

```
proc pname args body
```

The *pname* is the name of the procedure. *args* is a list of arguments to the procedure, and *body* is a Tcl script that is the body of the procedure.

When Tcl invokes a procedure, actual arguments are stored in the variables named by *args*. The *body* is executed, and whatever it returns becomes the return value of the procedure.

Consider the following procedure, which returns the sum of the squares of its arguments:

```
proc sos { a b } {
  expr $a*$a + $b*$b
}
```

You can now use *sos* as a Tcl command:

```
% sos 3 4
25
% sos -3 8
73
% sos 7
no value given for parameter "b" to "sos"
```

You can use the return command to prematurely end execution of a procedure; the argument of the return command is returned as the procedure’s value. For example, you can create a recursive procedure to compute the factorial of a number:

```
proc factorial { n } {
    if {$n <= 1} {
        return 1
    }
    expr $n * [factorial [expr $n-1]]
}
```

In this example, if the argument is less than or equal to 1, 1 is returned. Otherwise, the expr command is executed and, because it is the last command in the procedure, its return value becomes the return value of the procedure. The following are some sample calls:

```
% factorial 10
3628800

% factorial 0
1

% factorial glup
syntax error in expression "glup-1"
```

### Local and Global Variables

All variables created in the body of a procedure, as well as the procedure’s formal arguments, are local variables. They are unique to that procedure (in fact, unique to a particular invocation of a procedure).

If you want to access global variables from a procedure body, use the global command to declare them as global.

```
set globVar 10
proc mult { a } {
    global globVar
    expr $a * $globVar
}
```

### Arguments

The proc command has additional syntax for declaring procedures with default values for missing arguments and for procedures that take an arbitrary number of arguments.

If an entry in the procedure’s argument list is a two-element list, the first element is the name of the formal argument and the second is the default value:

```
proc mult {a {b 10}} {
    expr $a * $b
}
% mult 5 6
30

% mult 5
50
```

As the example shows, if the second argument is omitted, it assumes the default value of 10.

You can declare a procedure taking an arbitrary number of arguments by using args as the final argument name. In this case, Tcl packs all remaining arguments into a list and assigns this list to args. The following procedure takes any number of arguments and returns the sum of their squares:

```
proc ssum { args } {
    set total 0
    foreach num $args {
        incr total [expr $num*$num]
    }
    return $total
}
% ssum 5 6
61
% ssum 1 2 3 4 5
55
% ssum
0
```

In the last case, args was assigned the empty list, so the foreach command did not iterate at all.

# Tk

Let us now look at some Tcl programs using the Tk widget set. You've already seen a simple example; let's write a useful Tcl/Tk program.

The following program creates a very simple color selector dialog box. It presents three sliders that you adjust to select various intensities of red, green, and blue. When you click OK, it prints the color value as a standard X color string on standard output.

> Note
> The line numbers are for reference; do not actually type them.

```
1 # Main program
2 frame .swatch -height 1i -width 1i
3 scale .red -length 4i -orient horizontal \\
4        -from 0 -to 255 -command setcolor -label Red
5 scale .green -length 4i -orient horizontal \\
6        -from 0 -to 255 -command setcolor -label Green
7 scale .blue -length 4i -orient horizontal \\
```
