
## Table 2-3 (continued)

| Operator Group | Operator Name | Notation | Associativity |
|---|---|---|---|
| Unary | Postincrement | x++ | Right to left |
| Unary | Postdecrement | x-- |  |
| Unary | Preincrement | ++x |  |
| Unary | Predecrement | --x |  |
| Unary | Address of | &x |  |
| Unary | Indirection | *x |  |
| Unary | Plus | +x |  |
| Unary | Minus | -x |  |
| Unary | Bitwise NOT | ~x |  |
| Unary | Logical NOT | !x |  |
| Unary | Sizeof | sizeof x |  |
| Unary | Type cast | (type)x |  |
| Multiplicative | Multiply | x*y | Left to right |
| Multiplicative | Divide | x/y |  |
| Multiplicative | Remainder | x%y |  |
| Additive | Add | x+y | Left to right |
| Additive | Subtract | x-y |  |
| Shift | Left shift | x<<y | Left to right |
| Shift | Right shift | x>>y |  |
| Relational | Greater than | x>y | Left to right |
| Relational | Greater than or equal to | x>=y |  |
| Relational | Less than | x<y |  |
| Relational | Less than or equal to | x<=y |  |
| Equality | Equal to | x==y | Left to right |
| Equality | Not equal to | x!=y |  |
| Bitwise | Bitwise AND | x&y | Left to right |
| Bitwise | Bitwise exclusive OR | x^y |  |
| Bitwise | Bitwise OR | x|y |  |
| Logical | Logical AND | x&&y | Left to right |
| Logical | Logical OR | x||y |  |
| Conditional | Conditional | z?x:y | Right to left |
| Assignment | Assignment | x=y | Right to left |
| Assignment | Multiply assign | x *= y |  |
| Assignment | Divide assign | x /= y |  |
| Assignment | Remainder assign | x %= y |  |
|  | Add assign | x += y |  |
|  | Subtract assign | x -= y |  |
|  | Left shift assign | x <<= y |  |
|  | Right shift assign | x >>= y |  |
|  | Bitwise AND assign | x &= y |  |
|  | Bitwise XOR assign | x ^= y |  |
|  | Bitwise OR assign | x |= y |  |
| Comma | Comma | x , y | Left to right |

Getting back to the question of interpreting *iptr[4], a quick look at Table 2-3 tells you that the [] operator has precedence over the * operator. Thus, when the compiler processes the expression *iptr[4], it evaluates iptr[4] first, and then it applies the indirection operator, resulting in the value of the int with the address in iptr[4].

## Statements

You use statements to represent the actions C functions will perform and to control the flow of execution in the C program. A statement consists of keywords, expressions, and other statements. Each statement ends with a semicolon (;).

A special type of statement — the compound statement — is a group of statements enclosed in a pair of braces ({ ... }). The body of a function is a compound statement. Such compound statements (also known as blocks) can contain local variables.

In the following sections — which are alphabetically arranged — I briefly describe the types of statements available in C.

### The break statement

You use the break statement to jump to the statement following the innermost do, for, switch, or while statement. It is also used to exit from a switch statement. Here is an example that uses break to exit a for loop:

```c
for(i = 0; i < ncommands; i++)
{
    if(strcmp(input, commands[i]) == 0) break;
}
```

### The case statement

The case statement marks labels in a switch statement. Here is an example (here interrupt_id is an integer variable):

```c
switch (interrupt_id)
{
    case XMIT_RDY:
        transmit();
        break;
    case RCV_RDY:
        receive();
        break;
}
```

### A compound statement or block

A compound statement or block is a group of declarations followed by statements, all enclosed in a pair of braces ({ ... }). Typical compound statements are the body of a function and the block of code following an if statement. In the following example, everything that appears within the braces — the declarations and the statements — constitute a compound statement:

```c
if(theEvent.xexpose.count == 0)
{
    int i;
    /* Clear the window and draw the figures
     * in the "figures" array
     */
    XClearWindow(theDisplay, dWin);
    if(numfigures > 0)
        for(i=0; i<numfigures; i++)
            draw_figure(theDisplay, dWin, theGC, i);
}
```

### The continue statement

The continue statement begins the next iteration of the innermost do, for, or while statement in which it appears. You can use continue when you want to skip the execution of the loop. For example, to add the numbers from 1 to 10, excluding 5, you can use a for loop that skips the body when the loop index (i) is 5:

```c
for(i=0, sum=0; i <= 10; i++)
{
    if(i == 5) continue;  /* Exclude 5 */
    sum += i;
}
```

### The default label

You use default as the label in a switch statement to mark code that will execute when none of the case labels match the switch expression.

### The do statement

The do statement, together with while, forms iterative loops with the following structure:

```
do
  statement
  while(expression);
```

where statement (usually a compound statement) executes until the expression in the while statement evaluates to 0. The expression is evaluated after each execution of the statement — thus a do-while block always executes at least once. For example, to add the numbers from 1 to 10, you can use the following do statement:

```c
sum = 0;
do
{
    sum += i;
    i++;
}
while(i <= 10);
```

### Expression statements

Expression statements are evaluated for their side effects. Some typical uses of expression statements include calling a function, incrementing a variable, and assigning a value to a variable. Here are some examples:

```c
printf("Hello, World!\n");
i++;
num_bytes = length * sizeof(char);
```

### The for statement

Use the for statement to execute a statement any number of times (basing that number on the value of an expression). The syntax is as follows:

```
for (expr_1; expr_2; expr_3) statement
```

where the expr_1 is evaluated once at the beginning of the loop, and the statement is executed until the expression expr_2 evaluates to 0. The third expression, expr_3, is evaluated after each execution of the statement. All three expressions are optional, and the value of expr_2 is assumed to be 1 if it is omitted. Here is an example that uses a for loop to add the numbers from 1 to 10:

```c
for(i=0, sum=0; i <= 10; sum += i, i++);
```

In this example, the actual work of adding the numbers is done in the third expression, and the statement controlled by the for loop is a null statement (a single ;).

### The goto statement

The goto statement transfers control to a statement label. Here is an example that prompts the user for a value and repeats the request if the value is not acceptable:

```c
ReEnter;
printf("Enter offset: ");
scanf("%d", &offset);
if(offset < 0 || offset > MAX_OFFSET)
{
    printf("Bad offset: %d Please reenter:\n", offset);
    goto ReEnter;
}
```

### The if statement

You can use the if statement to test an expression and execute a statement only when the expression is not zero. An if statement takes the following form:

```
if ( expression ) statement
```

The statement following the if is executed only if the expression in parentheses evaluates to a non-zero value. That statement is usually a compound statement. Here is an example:

```c
if(mem_left < threshold)
{
    Message("Low on memory! Close some windows.\n");
}
```

### The if-else statement

The if-else statement is a form of the if statement coupled with an else clause. The statement has the syntax

```
if ( expression )
    statement_1
else
    statement_2
```

where statement_1 is executed if the expression within the parentheses is not zero. Otherwise, statement_2 is executed. Here is an example that uses if and else to pick the smaller of two variables:

```c
if ( a <= b)
    smaller = a;
else
    smaller = b;
```

### The null statement

The null statement, represented by a solitary semicolon, does nothing. You use null statements in loops when all processing is done in the loop expressions rather than in the body of the loop. For example, to locate the zero byte marking the end of a string, you may use the following:

```c
char str[80] = "Test";
int i;

for (i=0; str[i] != '\0'; i++)
    ; /* Null statement */
```

### The return statement

The return statement stops executing the current function and returns control to the calling function. The syntax is

```
return expression;
```

where the value of the expression is returned as the value of the function. For a function that does not return a value, use the return statement without the expression as follows:

```
return;
```

### The switch statement

The switch statement performs a multiple branch, depending on the value of an expression. It has the following syntax:

```
switch (expression)
{
    case value1:
        statement_1
        break;
    case value2:
```
