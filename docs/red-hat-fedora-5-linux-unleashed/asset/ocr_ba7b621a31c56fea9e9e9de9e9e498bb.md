The double quotes resolve all variables within the string. Here is an example for pdksh and bash:

```
var="test string"
newvar="Value of var is $var"
echo $newvar
```

Here is the same example for tsh:

```
set var="test string"
set newvar="Value of var is $var"
echo $newvar
```

If you execute a shell program containing the preceding three lines, you get the following result:

```
Value of var is test string
```

# Using Single Quotes to Maintain Unexpanded Variables

You can surround a string with single quotes (') to stop the shell from expanding variables and interpreting special characters. When used for the latter purpose, the single quote is an escape character, similar to the backslash, which you learn about in the next section. Here, you learn how to use the single quote to avoid expanding a variable in a shell script. An unexpanded variable maintains its original form in the output.

In the following examples, the double quotes in the preceding examples have been changed to single quotes.

+   pdksh and bash:

```
var='test string'
newvar='Value of var is $var'
echo $newvar
```

+   tsh:

```
set var = 'test string'
set newvar = 'Value of var is $var'
echo $newvar
```

If you execute a shell program containing these three lines, you get the following result:

```
Value of var is $var
```

As you can see, the variable var maintains its original format in the results, rather than having been expanded.