# # Using Pointers in Expressions

In **Program 10.3**, two integer pointers, p    and p    , are defined. Notice how the value referenced by a pointer can be used in an arithmetic expression. If p    is defined to be of type “pointer to integer,” what conclusion do you think can be made about the use of *      in an expression?

**Program 10.3 Using Pointers in Expressions**

[Click here to view code image]

```
```
/
#
i
{

}
```

```

**Program 10.3 Output**

[Click here to view code image]

```
```
i
```

```

After defining the integer variables i    and i    and the integer pointer variables p    and p    , the program then assigns the value 5 to i    and stores a pointer to i    inside p    . Next, the value of i    is calculated with the following expression:

```
```
i
```

```

As implied from the discussions of **Program 10.2**, if a pointer p    points to a variable x, and p    has been defined to be a pointer to the same data type as is x, then use of *      in an expression is, in all respects, identical to the use of x in the same expression.

Because in **Program 10.3** the variable p    is defined to be an integer pointer, the preceding expression is evaluated using the rules of integer arithmetic. And because the value of *      is 5 (p    points to i    ), the final result of the evaluation of the preceding expression is 1    , which is the value that is assigned to i    . (The pointer reference operator * has higher precedence than the arithmetic operation of division. In fact, this operator, as well as the address operator &, has higher precedence than *all* binary operators in C.)

In the next statement, the value of the pointer p    is assigned to p    . This assignment is perfectly valid and has the effect of setting p    to point to the same data item to which p    points. Because p    points to i    , after the assignment statement has been executed, p    *also* points to i    (and you can have as many pointers to the same item as you want in C).

The p            call verifies that the values of i  , *     , and *      are all the same (5) and that the