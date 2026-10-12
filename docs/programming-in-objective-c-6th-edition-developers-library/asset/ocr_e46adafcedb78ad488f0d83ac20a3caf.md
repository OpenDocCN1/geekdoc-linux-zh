operation is carried out and the results are displayed. Pay careful attention to the nesting of the \xi statements and the associated \xi clauses in this case.

The \xe clause at the end of the program catches any “fall throughs.” Therefore, any value of \x0 that does not match any of the four characters tested causes this \xe clause to be executed, resulting in the display of “Unknown operator.”

# # The switch Statement

The type of \xi statement chain that you encountered in the last program example—in which the value of a variable is successively compared against different values—is so commonly used when developing programs that a special program statement exists in the C language for performing precisely this function. The name of the statement is the \x5 statement, and its general format is

```
Click here to view code image

```
s expression
{
        value1:
            program statement
            program statement

        value2:
            program statement
            program statement

        valuen:
            program statement
            program statement

            program statement
            program statement
}
```
```

The expression enclosed within parentheses is successively compared against the values value1, value2, ..., valuen, which must be simple constants or constant expressions. If a case is found whose value is equal to the value of expression, the program statements that follow the case are executed. Note that when more than one such program statement is included, they do not have to be enclosed within braces.

The \xb statement signals the end of a particular case and causes execution of the \x5 statement to be terminated. Remember to include the \xb statement at the end of every case. Forgetting to do so for a particular case causes program execution to continue into the next case whenever that case gets executed.

The special optional case called \xd is executed if the value of expression does not match any of the case values. This is conceptually equivalent to the “fall through” \xe that you used in the previous example. In fact, the general form of the \x5 statement can be equivalently expressed as an \xi statement as follows:

```
Click here to view code image
```