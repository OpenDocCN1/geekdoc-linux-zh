If you want to alter the order of evaluation of terms inside an expression, you can use parentheses. In fact, the expression listed previously is a perfectly valid C expression. Thus, the statement

r

could have been substituted in Program 3.2 to achieve identical results. However, if the expression

r

were used instead, the value assigned to r would be 2550 because the value of a (1 ) would be added to the value of b (2 ) before multiplication by the value of c (2 ) would take place. Parentheses can also be nested, in which case evaluation of the expression proceeds outward from the innermost set of parentheses. Just be certain you have as many closed parentheses as you have open ones.

You will notice from the last statement in Program 3.2 that it is perfectly valid to give an expression as an argument to p without having to first assign the result of the expression evaluation to a variable. The expression

a

is evaluated according to the rules stated previously as

(

or

(

The result of 3 is handed to the p routine.

# Integer Arithmetic and the Unary Minus Operator

Program 3.3 reinforces what you just learned and introduces the concept of integer arithmetic.

Program 3.3 More Examples with Arithmetic Operators

Click here to view code image

```
/
#
i
{

}
```

Program 3.3 Output

```
6
a
```