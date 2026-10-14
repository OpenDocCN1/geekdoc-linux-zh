the equation of line 12. This SRFF works identically to the one described by

# Listing 6.3 ABEL code for a single macrocell or LUT SR flip-flop.

```
001- MODULE SRFF2
002- TITLE 'simple SR flip-flop'
003-
004- DECLARATIONS
005- SB PIN;                 "S input
006- RB PIN;                 "R input
007- Q PIN ISTYPE 'COM';     "Q output
008-
009- EQUATIONS
010- Q = !(SB & !(RB & Q));
011-
012- END SRFF2
```

The VHDL code for an SRFF with no QB output is shown in Listing 6.4. This SRFF consumes just 1 LUT or CLB, but it is expressed in a behavioral style rather than as Boolean equations. A behavioral logic description typically has one or more processes surrounded by PROCESS...END PROCESS statements. The PROCESS keyword is followed by a parenthesized sensitivity list. If any of the signals in the list changes its value, then the statements in the process block are evaluated.

The process starting on line 17 of Listing 6.4 is initiated if either the sb or qb inputs or the q output changes state. In general, the sensitivity list contains all the signals which appear as operands in conditional expressions or on the right-hand side of the <= assignment operator of statements in the process block.

The IF...ELSIF...ELSE conditional statement on lines 19 through 25 describes the actual operations of the S-R flip-flop. Line 20 sets the q output to 1 if the sb input is ever low. But if sb is not 0 and rb is, then line 22 will reset q to 0. Finally, line 24 states that q will not change its value if neither sb or rb is low. This is exactly the operation we want in an S-R flip-flop.

Note that we do not even need the statements on lines 23 and 24 and they could be removed without affecting the operation of the flip-flop. Consider the case when sb=0 and rb=1. The q output will be 1 after the process executes line 20 and the process terminates. Then if sb goes high, the change will initiate the process once more. But this time neither sb or rb is low, so neither of the assignment statements on lines 20 or 22 will be executed. With no explicit statement to set its value, the q output will retain its previous value which was 1. When an output retains its last value because none of the assignment statements are