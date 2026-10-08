You can initialize variables with values at the time they are declared by placing an equal sign after the variable name and then a constant value. Here is an example:

```
int days = 5, months = 2, years = 10;
```

# Understanding the Scope of Variables

The **scope** of a variable is the part of the program in which the variable is defined and therefore accessible. You can declare a variable either inside a function or any place that is not inside a function.

Variables that are declared inside a function are called **automatic variables**. These variables are local to the function in which they are declared. Here is an example:

```
/* This program declares a local variable
    in function main. The program does nothing
    else. */
int main()
{
int days;
}
```

Here, the variable days is an automatic variable and is local to the function main. You can also declare a variable outside of any function, as in the following example:

```
/* This program declares a global variable
    The program does nothing else. */

int days;
int main()
{
}
```

In the program above, the variable is external, or global. The scope of a global variable is the entire program, beginning at the point where the declaration was made. The scope of an automatic, or local, variable is the body of the function in which it is declared.

The only place inside a function where local variables may be declared is at the beginning of the body of the function—after the opening brace and before any statement. You can declare global variables anywhere in a program except inside a function.

# Using Math Operators

Table 10-4 lists the C arithmetic operators.