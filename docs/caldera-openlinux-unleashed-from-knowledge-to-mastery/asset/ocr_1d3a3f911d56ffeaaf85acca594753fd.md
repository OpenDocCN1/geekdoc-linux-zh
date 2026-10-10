The variable `fudgeFactor` must be defined in some other source file; the linker will resolve the reference to it during linking (or linking will fail).

We could also have written the example like this:

```
```c
double mySin(double x)
{
    /* Someone else defines this... */
    extern double fudgeFactor;

    return sin(x + fudgeFactor);
}
```
```

The variable `fudgeFactor` is still external, but the scope of the declaration is limited to the body of mySin.

# Statements

A C program consists of a sequence of statements. A statement comes in various flavors:

+   * Declarations declare functions or variables. We’ve seen examples of declarations before. Declaration statements are terminated with a semicolon.
+   * Definitions define functions. The “Hello, World!” program consists of some preprocessing information and a definition of main.
+   * Expression statements evaluate expressions. These are the most common C statements. Expression statements are terminated with a semicolon.
+   * if and switch statements control program flow.
+   * for, do, and while statements create loop structures.
+   * The return statement causes termination of a function.
+   * The break and continue statements alter the behavior of a loop statement.
+   * A compound statement consists of a group of statements enclosed in curly brackets.

# Declarations

A variable declaration declares the type of a variable or function. Consider this example:

```
```c
extern double foo;
extern int defenestrate(int window, double force);
```
```

These statements declare a variable `foo` of type `double`, and a function `defenestrate`, which returns a value of type `int`. The function expects two arguments, the first of type `int` and the second of type `double`. Note that the declarations do not define the function