When working with multiple compound operators you must be careful of the operator order. You can group them together using parentheses to establish the proper operations.
An example of this is:

```
if ($test -- 0 || ($test -- 1 && $test2 -- 0))
```

The condition evaluates to a TRUE value if the $test variable value is either 0, or the value of $test is 1 and the value of $test2 is 0.

# Arithmetic Operators

Arithmetic operators can be used to perform the standard mathematical operations on variables. The available operators are listed in Table 26-3.

Table 26-3: Perl Arithmetic Operators
| Operation | Operator |
|---|---|
| Raise x to the y power | x**y |
| Calculate the remainder of x/y | x%y |
| Add x to y | x+y |
| Subtract y from x | x-y |
| Multiply x times y | x*y |
| Divide x by y | x/y |
| Negate y | -y |
| Increment y by 1 and uses value | ++y |
| Use value of y and then increments by 1 | y++ |
| Decrement y by 1 then uses value | --y |
| Use value of y and then decrements by 1 | y-- |
| Assign value of y to x | x=y |

These operators are mostly used in assignment statements when performing mathematical calculations:

```
$area = $pi * $radius ** 2;
```

The standard order of operators applies when using multiple operators in a statement. You can use parentheses to alter the order of the operators.

# Regular Expressions

Regular expressions are templates that you use to help simplify searching for data. The regular expression template is compared against a pool of data. Any data that matches the template passes the test, while any data not matching the template is rejected. This is a great way to quickly sort through various types of data.