gawk scripts directly from the command line, using the multiline feature of the shell. When you use gawk in a shell script, you should place different gawk commands on separate lines. This'll make it much easier to read and follow, rather than trying to cram it all onto one line in the shell script.

# User-defined variables

Just like any other self-respecting programming language, gawk allows you to define your own variables for use within the program code. A gawk user-defined variable name can be any number of letters, digits, and underscores, but it can't begin with a digit. It's also important to remember that gawk variable names are case sensitive.

# Assigning variables in scripts

Assigning values to variables in gawk programs is similar to doing so in a shell script, using an assignment statement:

```
$ gawk
> BEGIN(
>   testing="This is a test"
>   print testing
> )\'
This is a test
```

The output of the print statement is the current value of the testing variable. Like shell script, gawk variables can hold either numeric or text values:

```
$ gawk
> BEGIN(
>   testing="This is a test"
>   print testing
>   testing=45
>   print testing
> )\'
This is a test
```

In this example, the value of the testing variable is changed from a text value to a numeric value.

Assignment statements can also include mathematical algorithms to handle numeric values:

```
$ gawk BEGIN(x=4; x = x * 2 + 3; print x)
11
```

As you can see from this example, the gawk programming language includes the standard mathematical operators for processing numerical values. These can include the remainder symbol (%) and the exponentiation symbol (using either ^ or **).