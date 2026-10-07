# Chapter 6: ADVANCED VARIABLE USAGE 281

with a new value that is computed using the arithmetic expression on the right side of the equal sign. Because of the timing (first compute the value on the right side, *then* assign it to the variable on the left side) it's perfectly legitimate to reference the original value of the variable to do the computation.

+   d) What do you observe about the use of spaces inside the double parentheses command?
Answer: It's all right to put spaces around the various parts of an arithmetic expression inside double parentheses.

The rule about no spaces in an assignment applies to let commands not inside double parentheses. Because spaces make code easy to read, it's a good idea to use double parentheses instead of the let command. You can also use spaces in the expression part of a let command by putting the expression to the right of the equal sign in quotes, but by the time you type the *word* let and the quotes, you as well type the double parentheses.

> You can make multiple arithmetic assignments in one let command line, just as you can do for nonarithmetic assignments. If you want to do the same thing inside double parentheses, separate the assignments with commas (, ).The following three command lines are equivalent:

```
let i=i+j j=j+k
(( i = i + j )) (( j = j + k ))
(( i = i + j, j = j + k ))
```

Run the following commands:
i=3 j=5
(( k = i++ )); ; print $i k=$k
(( k = ++j )) ; print $j k=$k

+   e) What does the double plus do, and what difference does it make whether it comes before or after the name of a variable?
Answer: Your interaction should look like the following:
[6037]: i=3 j=5
[6038]: (( k = i++ )); ; print $i k=$k
i=4 k=3
[6039]: (( k = ++j )) ; print $j k=$k