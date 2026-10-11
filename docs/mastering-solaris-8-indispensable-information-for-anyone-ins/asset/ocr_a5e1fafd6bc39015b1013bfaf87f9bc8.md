```
$ echo 'dept*' $wordproc
dept* currirr
$ echo 'dept*' $wordproc
dept* $wordproc
```

# ## Parameters and Variables

Shell parameters are values that are accessible to the owner. Shell parameters may consist of letters, digits, and underscores. Variables may not start with a number or contain hyphens. User-created variables are shell variables that you name and assign values to. To set a variable in sh or ksh, you would not precede or follow the equal sign with a space or tab, as shown in the following example:

```
$ car=van
$ echo car
car
```

To bring the value of the variable to output, you must place another dollar sign in front of the value:

```
$ echo $car
van
```

This dollar sign causes the shell to pass the value of the variable to echo, which displays it on the screen. You may also use quotation marks to deal with variables. For example, you may place double or single quotes around a variable to control the output. The following example shows what the output will be if you use double or single quotes:

```
$ echo $car
van
$ echo '$car'
van
$ echo '$car'
$car
$ echo \$car
$car
```

Quotation marks are good to use if you need to maintain spacing in the output. The following example shows what the output will look like if you need a literal space or tab:

```
$ car="Dodge Van Sport Model"
$ echo $car
Dodge Van Sport Model
```