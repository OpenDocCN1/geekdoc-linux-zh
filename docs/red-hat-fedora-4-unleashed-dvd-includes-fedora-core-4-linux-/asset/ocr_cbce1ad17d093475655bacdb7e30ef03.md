# The repeat Statement (t csh)

The repeat statement is used to execute only one command a fixed number of times.

If you want to print a hyphen (-) 80 times with one hyphen per line on the screen, you can use the following command:

```
`repeat 80 echo '-'`
```

# The select Statement (pdksh)

The select statement is used to generate a menu list if you are writing a shell program that expects input from the user online. The format of the select statement is as follows:

```
```
select item in itemlist
do
    Statements
done
```
```

itemlist is optional. If it isn't provided, the system iterates through the item entries one at a time. If itemlist is provided, however, the system iterates for each entry in itemlist and the current value of itemlist is assigned to item for each iteration, which then can be used as part of the statements being executed.

If you want to write a menu that gives the user a choice of picking a Continue or a Finish, you can write the following shell program:

```
```bash
#!/bin/ksh
select item in Continue Finish
do
    if [ $item = "Finish" ]; then
        break
    fi
done
```
```

When the select command is executed, the system displays a menu with numeric choices to the user—in this case, 1 for Continue and 2 for Finish. If the user chooses 1, the variable item contains a value of Continue; if the user chooses 2, the variable item contains a value of Finish. When the user chooses 2, the if statement is executed and the loop terminates.

# The shift Statement

The shift statement is used to process the positional parameters, one at a time, from left to right. As you'll remember, the positional parameters are identified as $1, $2, $3, and so on. The effect of the shift command is that each positional parameter is moved one position to the left and the current $1 parameter is lost.