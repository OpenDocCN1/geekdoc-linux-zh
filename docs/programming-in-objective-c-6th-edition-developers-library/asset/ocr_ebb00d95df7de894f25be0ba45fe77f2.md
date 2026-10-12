# Omitting Fields

Just as the need might arise to include more than one expression in a particular field of the $\mathrm{f}$ statement, the need might arise to omit one or more fields from the statement. This can be done simply by omitting the desired field and marking its place with a semicolon. The most common application for the omission of a field in the $\mathrm{f}$ statement occurs when there is no initial expression that needs to be evaluated. The init_expression field can simply be "left blank" in such a case, as long as the semicolon is still included:

```
``` 
 f
```
```

This statement might be used if j were already set to some initial value before the loop was entered. A f loop that has its looping_condition field omitted effectively sets up an infinite loop; that is, a loop that is theoretically executed forever. Such a loop can be used provided there is some other means used to exit from the loop (such as executing a r , b , or g statement as discussed elsewhere in this book).

# Declaring Variables

You can also declare variables as part of your initial expression inside a f loop. This is done using the normal ways you've defined variables in the past. For example, the following can be used to set up a f loop with an integer variable c both defined and initialized to the value 1:

Click here to view code image

```
```
 f
```
```

The variable c is only known throughout the execution of the f loop and cannot be accessed outside the loop. As another example, the following f loop

Click here to view code image

```
```
 f
```
```

defines two integer variables and sets their values accordingly.

# The while Statement

The w statement further extends the C language's repertoire of looping capabilities. The syntax of this frequently used construct is as follows:

Click here to view code image

```
```
 w       expression
       program statement (or statements)
```
```

The expression specified inside the parentheses is evaluated. If the result of the evaluation is TRUE, the program statement that immediately follows is executed. After execution of this statement (or statements if enclosed in braces), the expression is once again evaluated. If the result of the evaluation is TRUE, the program statement is once again executed. This process continues until the expression finally evaluates as FALSE, at which point the loop is terminated. Execution of the program then continues with the statement that follows the program statement.

As an example of its use, Program 4.6 sets up a w loop, which merely counts from 1 to 5.