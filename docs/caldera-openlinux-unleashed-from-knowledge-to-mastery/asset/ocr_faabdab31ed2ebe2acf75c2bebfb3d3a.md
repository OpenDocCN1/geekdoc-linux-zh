Test the script by typing the following:

```
$ awk -f countwords.awk
I like awk and awk likes me
Do I like awk?
^D
awk occurred 1 time(s)
me occurred 1 time(s)
likes occurred 1 time(s)
and occurred 1 time(s)
I occurred 2 time(s)
awk occurred 2 time(s)
Do occurred 1 time(s)
like occurred 2 time(s)
```

In the previous example, the notation ^D means to enter **Control+D**, your terminal's end-of-file character.

As you see, awk counts the words you enter. Note that it treats awk and awk? as different words. Also note that the words come out in an unpredictable order—the second for loop iterates over the array in an unspecified order. This is because of the low-level implementation details of associative arrays.

# ## awk Expressions

Many awk statements use expressions to control their behavior. For example, the first form of the for statement uses three expressions to control the looping.

An awk expression is similar to a C expression. It consists of a sequence of values and operators. The awk operators in order of decreasing precedence are given in Table 30.3.

TABLE 30.3  awk Operators
| Operator | Meaning |
|:---------|:---------|
| ( ... ) | Grouping. Parentheses alter the normal precedence rules. |
| $ | Field reference. |
| ++ and - | Pre- and post-increment and decrement. The pre operators increment or decrement a variable and return the new value; the post operators increment or decrement a variable and return the old value. |
| ^ or ** | Exponentiation. |
| * , / , and % | Multiplication, division, and modulus. |
| + and - | Addition and subtraction. |
| space | String concatenation. |