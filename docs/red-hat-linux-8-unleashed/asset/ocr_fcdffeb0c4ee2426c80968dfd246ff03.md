If you want to write a menu that gives the user a choice of picking a Continue or a Finish, you can write the following shell program:

```
#!/bin/ksh
select item in Continue Finish
do
if [ $item = "Finish" ]; then
  break
fi
```

When the select command is executed, the system displays a menu with numeric choices to the user—in this case, 1 for Continue and 2 for Finish. If the user chooses 1, the variable item contains a value of Continue; if the user chooses 2, the variable item contains a value of Finish. When the user chooses 2, the if statement is executed and the loop terminates.

# The Shift Statement

The shift statement is used to process the positional parameters, one at a time, from left to right. As you'll remember, the positional parameters are identified as $1, $2, $3, and so on. The effect of the shift command is that each positional parameter is moved one position to the left and the current $1 parameter is lost.

The shift statement is useful when you are writing shell programs in which a user can pass various options. Depending on the specified option, the parameters that follow may mean different things or might not be there at all.

The format of the shift command is as follows:

```
shift number
```

The parameter number is the number of places to be shifted and is optional. If not specified, the default is 1; that is, the parameters are shifted one position to the left. If specified, the parameters are shifted number positions to the left.

# Conditional Statements

Conditional statements are used in shell programs to decide which part of the program to execute depending on specified conditions.

# The if Statement

The if statement evaluates a logical expression to make a decision. If an if condition has the following format in pdksh and bash: