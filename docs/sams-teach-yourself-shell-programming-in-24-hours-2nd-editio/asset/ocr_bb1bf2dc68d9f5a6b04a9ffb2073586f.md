This process, known as variable substitution, is covered in greater detail in Chapter 9, "Substitution." The following example demonstrates this process:

```
$ FRUIT=peach
$ echo $FRUIT
peach
```

In this example, the shell first determines that the variable FRUIT has been referenced. Next it looks up the value for FRUIT. Finally the string $FRUIT is replaced with peach, the value of FRUIT, which is what the echo command prints.

If you do not use the dollar sign ($), variable substitution is not performed and the name of the variable is used directly. For example,

```
$ echo FRUIT
FRUIT
```

simply prints out FRUIT, not the value of the variable FRUIT.

The dollar sign ($) is used only when accessing a variable's value. It should not be used to define a variable or assign a value to a variable. For example, the assignment

```
$ SFUIT=apple
```

generates the following error message

```
sh: peach-apple: not found
```

assuming that the value of FRUIT was peach. If the variable FRUIT did not have a value, the error would have been

```
sh: =apple: not found
```

# Array Variables

Arrays are a method for grouping a set of variables together using a single name. Instead of creating a new name for each variable you need, you can use a single array variable to stores all the variables.

To understand how arrays work, consider the following example. Say that we are trying to represent the chapters in this book using a set of scalar variables. We could choose the following variable names to represent some of the chapters:

+   CH01
+   CH02
+   CH15
+   CH07