# The # and @ Commands (Execute a DOS Program)

The external program execution commands (# and @) are used to load and run an .exe or .com program without exiting Novell Client. The # command stops the login script from processing until the specified program has finished running, but the @ command starts an executable program and then continues processing login script commands while the executable program runs in the background. The @ command is useful if you want to load continuously running programs, such as virus detection software, into the computer’s memory. Using the # command causes the login script to “hang” because the background program runs continuously in memory and doesn’t exit back to the login script processor.

# IF... THEN... ELSE Statements

You can use the IF statement to customize a login script for users or groups and to perform special processing when a certain condition exists (such as a specific day or time). Here’s the syntax for an IF statement:

```
IF condition THEN command
```

The condition parameter is replaced with a conditional statement that has a value of true or false. Conditional statements usually consist of an identifier variable and a value enclosed in quotation marks. Table 9-8 shows some common conditional statements.

**Table 9-8** Common conditional statements

| Condition | Description |
| :--- | :--- |
| MEMBER OF “group” | This statement is true if the user is a member of the specified group. |
| DAY_OF_WEEK=“Monday” | This statement is true if the day is Monday. Possible values range from Sunday through Saturday. Uppercase or lowercase letters can be used. |
| DAY=“05” | This statement is true on the fifth day of the month; valid values range from 01 to 31. Include the leading zero for day numbers lower than 9. |
| MONTH=“June” | This statement is true for the month of June. You can replace “June” with any valid month name from January to December. Uppercase or lowercase letters are accepted. |
| NDAY_OF_Week=“1” | This statement is true on Sunday, which is the first day of the week. Valid weekday numbers range from 1 to 7. |

The command parameter can be replaced with any valid login script command. For example, a simple IF statement with a single condition can be written as follows:

```
IF DAY_OF_WEEK=“FRIDAY” THEN WRITE “Hurrah it’s Friday!”
```

More complex IF statements consist of multiple commands followed by the END statement. For these statements, use the BEGIN command after THEN, and then place commands after the IF statement, as shown:

```
IF condition THEN BEGIN

    command 1

    command 2

    command n

END
```

All commands between IF and END are performed when the condition is true. For example, to set up drive mappings for members of the Design group, you can use this IF statement in the Engineering container login script:

```
IF MEMBER OF “Design” THEN BEGIN

    MAP ROOT P:=UASHOST_CORP:\Engineer\CAD
```