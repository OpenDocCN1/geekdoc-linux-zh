The expression i++ in the second line is mere shorthand for the longer addition and assignment in the first. The expression i++ adds one to the current value of integer i, and stores the result in i. The following two expressions also have identical effects:

```
i = i + 1; // Subtracts one from i
i--; // Same as the preceding statement
```

The expression i-- subtracts one from the value stored in i. You may use the ++ and -- operators only on integers, not on floating point variables. (However, ++ and -- may also be used with pointers. See Chapter 11, “Managing Memory with Pointers.”)

In addition to incrementing and decrementing their operands, expressions such as i++ and i-- also have values, as do all expressions. But the value of increment and decrement expressions depends on the position of the operators. This is a subtle, but critical, rule to understand. When ++ or -- follow their operands, the values of the expressions i++ and i-- equal the unmodified values. In other words, the statement

```
j = i++;
```

assigns to j the unmodified value of i. If i equals 7, after executing that statement, j equals 7 and i equals 8. C++ increments i after assigning the evaluated expression to j. A different result occurs when increment and decrement operators precede their operands. In that case, the expressions equal the modified operand values. The statement

```
j = ++i;
```

increments i and then assigns that incremented value to j. If i equals 7, after executing the preceding statement, j and i both equal 8. Another way to visualize these effects is to write increment and decrement expressions in long form. The statement

```
j = i++;
```

operates as though it were the two statements:

```
j = i;
i = i + 1;
```

And the statement

```
j = ++i;
```

operates as though it were written as:

```
i = i + 1;
j = i;
```

> Note
> The same rules for ++ apply to --. The expression i-- equals the value of i before it is decremented by one. The expression --i equals the decremented value of i.

# BITWISE OPERATORS

C and C++ provide several bitwise operators that you can use to perform Boolean logic operations on the individual bits of binary values. Table 7.3 summarizes the C and C++ bitwise operators.