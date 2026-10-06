```
$ print -f "This %s value is %d\n" $test $test2
This testing value is 10
$
```

The %s and %d control codes determine the format of the output for the associated variables in the print command list.

The printf command uses only the C-style printf format to display arguments by default.
The format of the printf command is:

```
printf format [ arg ... ]
```

The format parameter is a text string that uses the standard symbols to denote specific data types and formats to use in the print (see Chapter 19). Each data symbol matches an argument supplied on the command line:

```
$ printf "This %s value is %d\n" $test $test2
This testing value is 10
$
```

The printf command provides a few formatting tricks until all of the listed variables are displayed.

+   - Reuses control codes until all of the listed variables are displayed.
- Can print time and date values using the same format as the date command.

If you supply more variables on the printf command line than control codes the printf command automatically goes back to the first control code and repeats using the additional variables. This is useful if you're trying to print a table of values. You only have to define the control codes for the first row, then list all of the variables on the same line:

```
$ test1=10
$test2=15
$test3=20
$test4=25
$ printf "%%d - %%d\n" $test1 $test2 $test3 $test4
10 - 15
20 - 25
$
```

The printf command also allows you to easily reformat a date and time value into any format using the date command format:

```
$ value='1/31/08'
$ print $value
1/31/08
$ printf "%%(%Y)T\n" $value
2008
```