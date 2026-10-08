+   5 You can specify the name of the executable file with the `-o` option. Type `gcc -o inches inches.c`, and press `Enter`. The command compiles the Inches.c file and stores the executable code in a file named Inches.

+   6 Run the inches program by typing `./inches` and pressing `Enter`.

# Using the if Statement

The if statement allows your program to make decisions depending upon whether a condition is true or false. The general form of the if statement is:

**Syntax**  `if (condition) statement;`

If the condition is true, statement will be performed. Here is an example:

```
if (weight > 1000) printf("You have exceeded the limit.");
```

If the variable `weight` contains a value greater than 1000, the `printf` statement executes.

Sometimes you may need to execute more than one line of code if a condition is true. C allows you to substitute a block of code for the single statement, when necessary. Here is an example:

```
if (weight > 1000)
{
    printf("Warning!\n");
    printf("You have exceeded the limit.\n");
    printf("Just thought you\'d like to know.");
}
```

The program segment above causes the three `printf` statements to execute if `weight` is greater than 1000.

The if-else construct allows your program to do one thing if a condition is true and another if it is false. Here is an example:

```
if (hours > 40)
    printf("You can go home now");
else printf("Keep working.");
```