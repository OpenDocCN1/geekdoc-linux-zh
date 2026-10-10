This example runs the date command and assigns its output to the variable `TodayDate`. You can then access the information in this variable just as you can access the information in any other variable.

# # Arithmetic in Shell Programs

Although the original Bourne shell has no built-in arithmetic handlers, arithmetic can still be done using command substitution along with the `expr` command. Here's an example:

```
var3=`expr var1 + var2`
```

This adds the values contained in var1 and var2 together and then stores the result in var3. Note that the arguments and the operator must be separated by whitespace. `expr var1+var2` will not have the intended result.

The `expr` command can do only very simple arithmetic—it can handle only integer arithmetic. Entering floating-point numbers will cause an error. In addition, changing the order of operations with parentheses is not supported. Division that does not return an integer value will have the decimal portion dropped. For example, `5 / 2` is 2 as far as `expr` is concerned. If you wish to retrieve the remainder of a division, you can use the modulus operator (%). For example, `expr 5 % 2` will return 1 (`5 / 2` = 4 remainder 1).

Characters that have special meaning to the shell must be escaped. For example, `expr 2 * 2` will not work because the shell interprets the * as a wildcard operator. For the operation to work, the multiplication operator (*) must be escaped like this: `expr 2 \* 2`. This protects it from the shell and prevents the shell from giving it special meaning.

`expr` can also evaluate true/false expressions. If the expression is true, `expr` returns a 1. If the expression is false, `expr` returns 0. Here's an example:

```
expr 2 + 2 = 4 + 1
```

This returns 0 (the equation is false).

This next example returns 1 (the equation is true):

```
expr 2 + 2 = 3 + 1
```

! = will reverse the equation. It means “is not equal to.” So, for example, the equation `expr 5 != 3` will return 1 (true).

`expr` can, of course, also evaluate less than/greater than expressions. Once again, because the < and > characters have special meaning to the shell, they must be escaped when used with `expr` to protect them from the shell. It is a true/false evaluation just like the “equal to” operator. If the expression is true, `expr` returns 1. If the expression is false, `expr` returns 0. For example, `expr 5 \> 4` returns 1 (the expression is true). In addition, greater than or equal to (\>=) and less than or equal to (\<=) evaluations are also supported.