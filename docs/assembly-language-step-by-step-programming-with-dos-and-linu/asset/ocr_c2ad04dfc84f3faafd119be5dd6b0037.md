# Bits, Flags, Branches, and Tables

Bits are numbered from right to left, starting from 0:

Byte value:

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|

Word value:

| 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

Most significant bit (MSB) Least-significant bit (LSB)

**Figure 10.1** Bit numbering.

write a check you don't have, and a check without money behind it will bounce. People who live out of their checkbooks (and they always end up ahead of me in the checkout line at Safeway) must use the AND operator frequently.

When mathematicians speak of Boolean logic, they manipulate abstract values called True and False. The AND operator works like this. Condition1 AND Condition2 will be considered True if both Condition1 and Condition2 are True. If either condition is False, the result will be False.

There are in fact four different combinations of the two input values, so logical operations between two values are usually summarized in a form called a *truth table*. The truth table for the AND operator is shown in Table 10.1.

There's nothing mysterious about the truth table. It's just a summary of all possibilities of the AND operator as applied to two input conditions. The important thing to remember is that *only* when both input values are True the result will also be True.

**Table 10.1** The AND Table for Formal Logic

| CONDITION1 | OPERATOR | CONDITION2 | RESULT |
|---|---|---|-|
| False | AND | False = | False |
| False | AND | True = | False |
| True | AND | False = | False |
| True | AND | True = | True |