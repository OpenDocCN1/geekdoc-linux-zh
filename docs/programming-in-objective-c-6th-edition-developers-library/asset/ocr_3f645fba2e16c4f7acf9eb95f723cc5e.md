It is when the increment and decrement operators are used in more complex expressions that the distinction between the pre- and post- nature of these operators is realized.

Suppose you have two integers called i and j. If you set the value of i to 0 and then write the statement
j

the value that gets assigned to j is 1, and not 0 as you might expect. In the case of the preincrement operator, the variable is incremented before its value is used in the expression. So, in the preceding expression, the value of i is first incremented from 0 to 1 and then its value is assigned to j, as if the following two statements had been written instead:
+
j

If you instead use the postincrement operator in the statement
j

then i is incremented after its value has been assigned to j. So, if i is 0 before the preceding statement is executed, 0 is assigned to j and then i is incremented by 1, as if the statements
j+
j

were used instead. As another example, if i is equal to 1, then the statement

×
has the effect of assigning the value of a

to × because the variable i is decremented before its value is used to index into a. The statement

×
used instead has the effect of assigning the value of a

to × because i is decremented after its value has been used to index into a.

As a third example of the distinction between the pre- and post- increment and decrement operators, the function call
P
increments i and then sends its value to the p

function, whereas the call
P
increments i after its value has been sent to the function. So, if i is equal to 100, the first P

call displays 101, whereas the second P

call displays 100. In either case, the value of i is equal to 101 after the statement has executed.

As a final example on this topic before presenting Program 10.14, if t is a character pointer, the expression

*
first increments t

and then fetches the character it points to, whereas the expression

*
fetches the character pointed to by t

before its value is incremented. In either case, the