FALSE, where TRUE is a nonzero number and FALSE is a zero. For simplicity, the words TRUE and FALSE will be used. A programmer can use define directives for these values in a program.

# For Loops

*For* loops are used to control definite looping, when we know how many times we want to loop. The syntax for this statement is:

```
for ( initialize expression; loop condition; update expression )
    statement;
```

The three expressions, initialize expression, loop condition, and update expression, set up and control the environment for the loop. The statement that immediately follows is the body of the loop consisting of any valid C statement.

If the body of the loop consists of more than one statement, curly braces ( { } ) are used to define the body.

```
for ( initialize expression; loop condition; update expression )
{
    statement;
    statement;
}
```

The first component of the *for* loop is labeled *initialize expression*. This is used to set the initial value of the control variable before the loop begins. An example of a valid expression is x = 0; The variable x is assigned the value of zero before the loop begins. The initialize expression is performed once, at the start of the loop.

The second component, *loop condition*, specifies the condition or set of conditions that are necessary for the loop to continue. After the loop condition is satisfied, the looping stops. The loop condition is specified with a relational expression. A *relational expression* compares variables using relational operators.

Relational operators provide a means to compare variables, constants and expressions. There are six operators in C that can test the relationships between two values, as shown in Table 14-5: