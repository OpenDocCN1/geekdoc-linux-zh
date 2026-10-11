Table 28-2 Comparison operators

| Numeric operators | String operators | Value returned based on the relationship between the values preceding and following the operator |
|:---|:---|:---|
| `==` | `eq` | True if equal |
| `!=` | `ne` | True if not equal |
| `<` | `lt` | True if less than |
| `>` | `gt` | True if greater than |
| `<=` | `le` | True if less than or equal |
| `>=` | `ge` | True if greater than or equal |
| `<=>` | `cmp` | 0 if equal, 1 if greater than, –1 if less than |

The next program is similar to the preceding one, except it tests for equality between two strings. The `chomp` function (page 1001) removes the trailing NEWLINE from the user's entry—without this function the strings in the comparison would never match. The `eq` comparison operator compares strings. In this example the result of the string comparison is *true* when the user enters the string five. Leading or trailing whitespace will yield a result of *false*, as would the string 5, although none of these entries would generate a warning because they are legitimate strings.

```
`$ cat if2a.pl`
`#!/usr/bin/perl –w`
`print "Enter the word 'five': ";`
`$entry = <>;`
`chomp ($entry);`
`if ($entry eq "five") { # use eq for a string comparison`
`    print "Thank you for entering 'five'.\n";`
`}`
`print "End.\n";`
`$ ./if2a.pl`
`Enter the word 'five': five`
`Thank you for entering 'five'.`
`End.`
```

# if...else

The if...else control structure is a compound statement that is similar to the bash if...then...else control structure (page 892). It implements a two-way branch using the following syntax:
*if* (*expr*) {…} else {…}

The next program prompts the user for two different numbers and stores those numbers in $num1 and $num2. If the user enters the same number twice, an if structure executes a *die* function, which sends its argument to standard error and aborts program execution.