you can save the gawk script in a separate file and reference it using the -f parameter (see Chapter 19).

# User-defined variables

Just like any other self respecting programming language, gawk allows you to define your own variables for use within the program code. A gawk user defined variable name can be any number of letters, digits, and underscores, but it can't begin with a digit. It is also important to remember that gawk variable names are case sensitive.

# Assigning variables in scripts

Assigning values to variables in gawk programs is similar to doing so in a shell script, using an assignment statement:

```
$ gawk '
> BEGIN{
> testing="This is a test"
> print testing
> }'
This is a test
$
```

The output of the print statement is the current value of the testing variable. Like shell script variables, gawk variables can hold either numeric or text values:

```
$ gawk '
> BEGIN{
> testing="This is a test"
> print testing
> testing=45
> print testing
> }'
This is a test
45
$
```

In this example, the value of the testing variable is changed from a text value to a numeric value.

Assignment statements can also include mathematical algorithms to