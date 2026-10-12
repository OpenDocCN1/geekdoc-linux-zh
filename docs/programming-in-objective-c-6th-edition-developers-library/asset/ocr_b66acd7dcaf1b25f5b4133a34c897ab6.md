```
t
{

}
```

You can now proceed to develop your graphics library, taking advantage of this P       type. For example, the declaration

```
Click here to view code image

P
defines o      and c               to be of type P      and sets the x and y members of o       to 0.0.

Here’s a function called d             that calculates the distance between two points.
```

```
Click here to view code image
# 
d
{


}
```

As previously noted, s      is the square root function from the standard library. It is declared in the system header file m   , thus the reason for the #            .
Remember, the t         statement does not actually define a new type—only a new type name. So the C      variables j and n, as defined in the beginning of this section, would in all respects be treated as normal i     variables by the C compiler.

# Data Type Conversions

Chapter 3, “Variables, Data Types, and Arithmetic Expressions,” briefly addressed the fact that sometimes, conversions are implicitly made by the system when expressions are evaluated. The case you examined was with the data types f       and i    . You saw how an operation that involved a f       and an i    was carried out as a floating-point operation, the integer data item being automatically converted to floating point.

You have also seen how the type cast operator can be used to explicitly dictate a conversion. So in the statement

```
a
```

the value of the variable t       is converted to type f        before the operation is performed, thereby guaranteeing that the division will be carried out as a floating-point operation.

The C compiler adheres to strict rules when it comes to evaluating expressions that consist of different data types.

The following summarizes the order in which conversions take place in the evaluation of two operands in an expression:

+   1. If either operand is of type l              , the other is converted to l             , and that is the type of the result.