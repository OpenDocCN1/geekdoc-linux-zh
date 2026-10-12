# ## Use Double Quotes to Resolve Variables in Strings with Embedded Spaces

If a string contains embedded spaces, you can enclose the string in double quotes (") so that the shell interprets the whole string as one entity instead of more than one.

For example, if you assigned the value of abc def (abc followed by one space, followed by def) to a variable called x in a shell program as follows, you would get an error because the shell would try to execute def as a separate command:

| Command | Environment |
| --- | --- |
| x=abc def | pdksh and bash |
| set x=abc def | tcsh |

The shell will execute the string as a single command if you surround the string in double quotes as follows:

| Command | Environment |
| --- | --- |
| x="abc def" | pdksh and bash |
| set x="abc def" | tcsh |

The double quotes resolve all variables within the string. Here is an example for pdksh and bash:

```
```
var="test string"
newvar="Value of var is $var"
echo $newvar
```
```

Here is the same example for tcsh:

```
```
set var="test string"
set newvar="Value of var is $var"
echo $newvar
```
```

If you execute a shell program containing the preceding three lines, you get the following result:

Value of var is test string

# ## Using Single Quotes to Maintain Unexpanded Variables

You can surround a string with single quotes (') to stop the shell from expanding variables and interpreting special characters. When used for the latter purpose, the single quote is an *escape character*, similar to the backslash, which you learn about in the next section. Here, you learn how to use the single quote to avoid expanding a variable in a shell script. An unexpanded variable maintains its original form in the output.