The operands are of different types (number and string), so MySQL converts one of them to make them the same type. But which one should it change? In this case, + is a numeric operator, so MySQL wants the operands to be numbers thus and converts the string ‘2’ to the number 2. Then it evaluates the expression to produce the result 3.

Here's another example. The CONCAT( ) function concatenates strings to produce a longer string as a result. To do this, it interprets its arguments as strings, no matter what type they are. If you pass it a bunch of numbers, CONCAT( ) converts them to strings, and then returns their concatenation:

```
CONCAT(1,23,456)
→ '123456'
```

If the call to CONCAT( ) is part of a larger expression, further type conversion may take place. Consider the following expression and its result:

```
REPEAT('X',CONCAT(1,2,3)/10)
→ 'XXXXXXXXXXXX'
```

CONCAT(1,2,3) produces the string ‘123’. The expression ‘123’/10 is converted to 123/10 because division is an arithmetic operator. The result of this expression is 12.3, but REPEAT( ) expects an integer repeat count, so the count is rounded to produce 12. Then REPEAT('X', 12) produces a string result of 12 ‘X’ characters.

If all arguments to CONCAT( ) are non-binary strings, the result is a non-binary string. If any argument is a binary string, the result is a binary string. The latter principle includes the case of numeric arguments, which are converted to binary strings. These examples both appear to produce the same result:

```
CONCAT('1',',','23')
→ '123'
CONCAT(1, '23')
→ '123'
```

But if you check the result with CHARSET( ), you can see that the expressions return a non-binary and binary string, respectively:

```
CHARSET(CONCAT('1',',','23'))
→ 'latin1'
CHARSET(CONCAT(1, '23'))
→ 'binary'
```

A general principle to keep in mind is that, by default, MySQL attempts to convert values to the type required by an expression rather than generating an error. Depending on the context, it converts values of each of the three general categories (numbers, strings, or dates and times) to values in any of the other categories. However, values can't always be converted from one type to another. If a value to be converted to a given type doesn't look like a legal value for that type, the conversion fails. Conversion to numbers of things like 'abc' that don't look like numbers results in a value of 0. Conversion to date or time types of things that don't look like a date or time result in the 'zero' value for the type. For example, converting the string 'abc' to a date results in the 'zero' date '0000-00-00'. On the other hand, any value can be treated as a string, so generally it's not a problem to convert a value to a string.