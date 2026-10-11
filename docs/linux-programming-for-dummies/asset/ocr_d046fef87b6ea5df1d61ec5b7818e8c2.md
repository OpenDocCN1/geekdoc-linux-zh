information that tells your computer information about you and about the computer. A common environment variable, for example, is EDITOR. The value that you assign to this variable is the name of the text editor that’s on your computer.

# Declaring variables

You can create a variable by using the reserved words declare and export, following them with the variable’s name. Here’s an example:

```
declare FirstName
export editor
```

In this example, you can see the creation of the following variable:

+   - The reserved word declare declares an environment variable.
+   - The reserved word export makes the variable available to the environment.

# Placing variables

Although you find no special place in your Linux program to declare a variable, you can, in fact, declare a variable anywhere in your program. Placing a variable just anywhere, however, isn’t what most programmers consider a good programming practice. If you do, you’re likely to end up hunting for those variables the next time you read your program.

A preferred programming practice is to declare all the variables at the beginning of your program. That way, they’re all in the same place whenever you need to find them.

# Combining your variables

You can declare variables of the same kind (such as two string variables) on the same line at the beginning of your program. The following example shows you how to do so:

```
declare FirstName LastName
```

You can type as many variable names as you can fit on the line. Notice that a space separates each variable.