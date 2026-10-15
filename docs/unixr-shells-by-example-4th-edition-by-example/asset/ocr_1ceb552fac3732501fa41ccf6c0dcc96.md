# EXAMPLE 7.27

```
*(Assigning temporary alternate values)

1  $ foo=grapes
2  $ echo ${foo:+pears}
   pears
3  $ echo $foo
   grapes
   $
```

# EXPLANATION

+   1. The variable foo has been assigned the value grapes.
+   2. The special modifier `+` will check to see if the variable has been set. If it has been set, pears will temporarily be substituted for foo; if not, null is returned.
+   3. The variable foo now has its original value.

# EXAMPLE 7.28

```
*(Creating error messages based on default values)

1  $ echo ${name:?"name is undefined"}
   name: name is undefined
2  $ echo ${y:?}
   y: parameter null or not set
```

# EXPLANATION

+   1. The `?` modifier will check to see if the variable has been set. If not, the string to the right of the `?` is printed to standard error, after the name of the variable. If in a script, the script exits.
+   2. If a message is not provided after the `?`, the shell sends a default message to standard error.

# 7.6.7  Positional Parameters

Normally, the special built-in variables, often called positional parameters, are used in shell scripts when passing arguments from the command line, or used in functions to hold the value of arguments passed to the function. See Table 7.6. The variables are called positional parameters because they are denoted by their position on the command line. The Bourne shell allows up to nine positional parameters. The name of the shell script is stored in the $0 variable. The positional parameters can be set and reset with the set command.