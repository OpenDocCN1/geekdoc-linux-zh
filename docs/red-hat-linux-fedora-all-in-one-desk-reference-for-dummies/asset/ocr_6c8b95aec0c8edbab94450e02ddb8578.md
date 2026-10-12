three expressions are optional, and the value of expr. 2 is assumed to be 1 if it is omitted. Here is an example that uses a for loop to add the numbers from 1 to 10:

```
for(i=0, sum=0; i <= 10; sum += i, i++);
```

In this example, the actual work of adding the numbers is done in the third expression, and the statement controlled by the for loop is a null statement (a single :).

# The goto statement

The goto statement transfers control to a statement label. Here is an example that prompts the user for a value and repeats the request if the value is not acceptable:

```
ReEnter;
printf("Enter offset: ");
scanf("%d", &offset);
if(offset < 0 || offset > MAX_OFFSET)
{
    printf("Bad offset: %d Please reenter:\n", offset);
    goto ReEnter;
}
```

# The if statement

You can use the if statement to test an expression and execute a statement only when the expression is not zero. An if statement takes the following form:

```
if ( expression ) statement
```

The statement following the if is executed only if the expression in parentheses evaluates to a non-zero value. That statement is usually a compound statement. Here is an example:

```
if(mem_left < threshold)
{
    Message("Low on memory! Close some windows.\n");
}
```

# The if-else statement

The if-else statement is a form of the if statement coupled with an else clause. The statement has the syntax

```
if ( expression )
    statement_1
```