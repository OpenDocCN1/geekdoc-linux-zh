# The Assignment Operators

Here are the points you should review for handling conditional operators in an exam question,
or to use them properly in a program. In an expression of the form a = x ? b : c;

+   - The types of the expressions b and c should be compatible and be made identical throughnconversion.

+   - The type of the expression x should be boolean.

+   - The types of the expressions b and c should be assignment-compatible with the type of a.
The value assigned to a must be b if x is true or c if x is false.

Now that we have discussed the conditional (ternary) operator, only one group of operatorsnremains: the assignment operators.

# The Assignment Operators

Assignment operators—= and— set the value of a variable or expression to a new value.
Assignments are supported by a battery of operators. Simple assignment uses =. Operators such
+= and *= provide "calculate and assign" functions. These compound operators
take a general form op= where op can be any of the binary non-boolean operators already
dis. For any compatible expressions x and y, the expression op= is a shorthand
for x = x op. However, there are two differences you must know. First, be aware that side effects
in the expression are evaluated exactly once, not twice, as the expanded view might suggest.
second issue is that the assignment operators include an implicit cast. Consider this situation:

+   1. byte x = 2;

+   2. x += 3;

If this had been written using the longhand approach

+   1. byte x = 2;

+   2. x = (byte)(x + 3);

the cast to would have been necessary because the result of an integer addition is at least
int. In the first case, using the assignment operator, this cast is implied. This is one of two situations
Java allows down-casting without explicit programmer intervention. The other situation is
in combined declaration and initialization.) We will to compare this with the general principles
of assignment and casting out in Chapter 4.

![](bbox=[0.125, 0.781, 0.198, 0.823])

The statement x += 2; involves two fewer characters but is otherwise
more effective than the longer version x = x + 2; and is neither nor
less readable. However, if x is a complex expression, such as target[temp
.calculateOffset(1.9F) + depth++].item, it is definitely more readable to
expressing this value by 2 using the += 2 form. This is because
operators define that the same thing will be read on the right side as writ-
on the left side. The maintainer does not have to struggle to decide whether
two complex expressions are actually the same, and the original programmer
avoids some of the risk of mistyping a copy of the expression.