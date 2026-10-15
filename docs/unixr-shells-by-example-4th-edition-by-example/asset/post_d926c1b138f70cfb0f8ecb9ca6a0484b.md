
## 6.17 Conditional Statements

The conditional statements in awk were borrowed from the C language. They are used to control the flow of the program in making decisions.

### 6.17.1 if Statements

Statements beginning with the if construct are action statements. With conditional patterns, the if is implied; with a conditional action statement, the if is explicitly stated, and followed by an expression enclosed in parentheses. If the expression evaluates true (nonzero or non-null), the statement or block of statements following the expression is executed. If there is more than one statement following the conditional expression, the statements are separated either by semicolons or a newline, and the group of statements must be enclosed in curly braces so that the statements are executed as a block.

Write a nawk script to produce the following output:

```
% nawk -f nawk.sc db
```

***CAMPAIGN 2006 CONTRIBUTIONS***

| NAME | PHONE | Jan | Feb | Mar | Total Donated |
|---|---|---|---|---|---|
| Mike Harrington | (510) 548-1278 | 250.00 | 100.00 | 175.00 | 525.00 |
| Christian Dobbins | (408) 538-3558 | 155.00 | 90.00 | 201.00 | 446.00 |
| Susan Dalsass | (206) 654-6279 | 250.00 | 60.00 | 50.00 | 360.00 |
| Archie McNichol | (206) 548-1348 | 250.00 | 100.00 | 175.00 | 525.00 |
| Jody Savage | (206) 548-1278 | 15.00 | 188.00 | 150.00 | 353.00 |
| Guy Quigley | (916) 343-6410 | 250.00 | 100.00 | 175.00 | 525.00 |
| Dan Savage | (406) 299-7744 | 450.00 | 300.00 | 275.00 | 1025.00 |
| Nancy McNeil | (206) 548-1278 | 250.00 | 80.00 | 75.00 | 405.00 |
| John Goldenrod | (916) 345-4278 | 250.00 | 100.00 | 175.00 | 525.00 |
| Chet Main | (510) 548-5258 | 50.00 | 95.00 | 135.00 | 280.00 |
| Tom Savage | (408) 926-3456 | 250.00 | 68.00 | 200.00 | 518.00 |
| Elizabeth Stachelin | (916) 440-1763 | 175.00 | 75.00 | 300.00 | 550.00 |

SUMMARY

The campaign received a total of $6137.00 for this quarter.
The average donation for the 12 contributors was $511.42.
The highest contribution was $450.00.
The lowest contribution was $15.00.

### FORMAT

```
if (expression) {
    statement; statement; ...
}
```

### EXAMPLE 6.127

```
1 % awk '{if ( $6 > 50 ) print $1 "Too high"}' filename
2 % awk '{if ($6 > 20 && $6 <= 50){safe++; print "OK"}}' filename
```

### EXPLANATION

1 In the if action block, the expression is tested. If the value of the sixth field ($6) is greater than 50, the print statement is executed. Because the statement following the expression is a single statement, curly braces are not required. (filename represents the input file.)

2 In the if action block, the expression is tested. If the sixth field ($6) is greater than 20 and the sixth field is less than or equal to 50, the statements following the expression are executed as a block and must be enclosed in curly braces.

### 6.17.2 if/else Statements

The if/else statement allows a two-way decision. If the expression after the if keyword is true, the block of statements associated with that expression are executed. If the first expression evaluates to false or 0, the block of statements after the else keyword is executed. If multiple statements are to be included with the if or else, they must be blocked with curly braces.

### FORMAT

```
{if (expression) {
    statement; statement; ...
}
else{
    statement; statement; ...
}
}
```

### EXAMPLE 6.128

```
1 % awk '{if ($6 > 50) print $1 "Too high"; \ else print "Range is OK"}' filename
2 % awk '{if ( $6 > 50 ) { count++; print $3 } \ else { x+=5; print $2 } }' filename
```

### EXPLANATION

- 1 If the first expression is true, that is, the sixth field ($6) is greater than 50, the print function prints the first field and Too high; otherwise, the statement after the else, Range is OK, is printed.
- 2 If the first expression is true, that is, the sixth field ($6) is greater than 50, the block of statements is executed; otherwise, the block of statements after the else is executed. Note that the blocks are enclosed in curly braces.

### 6.17.3 if/else and else if Statements

The if/else and else if statements allow a multiway decision. If the expression following the keyword if is true, the block of statements associated with that expression is executed and control starts again after the last closing curly brace associated with the final else. Otherwise, control goes to the else if and that expression is tested. When the first else if condition is true, the statements following the expression are executed. If none of the conditional expressions test true, control goes to the else statements. The else is called the default action because if none of the other statements are true, the else block is executed.

### FORMAT

```
{if (expression) {
    statement; statement; ...
}
else if (expression){
    statement; statement; ...
}
else if (expression){
    statement; statement; ...
}
else{
    statement
}
}
```

### EXAMPLE 6.129

```
(In the Script)
1 {if ( $3 > 89 && $3 < 101 ) Agrade++
2 else if ( $3 > 79 ) Bgrade++
3 else if ( $3 > 69 ) Cgrade++
4 else if ( $3 > 59 ) Dgrade++
5 else Fgrade++
}
END{print "The number of failures is" Fgrade }
```
