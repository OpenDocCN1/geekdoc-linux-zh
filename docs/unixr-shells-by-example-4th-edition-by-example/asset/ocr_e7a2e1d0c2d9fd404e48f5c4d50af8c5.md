# EXPLANATION

+   1. If using the compound test command, shell metacharacters can be used in string tests. In this example, the expression is tested for string equality where name can match either Tom, tom, tommy, and so forth. If the expression is true, the exit status (?) is 0.
+   2. The logical operators && (AND) and || (OR) can be used with the compound test. If && is used, both expressions must be true, and if the first expression evaluates as false, no further checking is done. With the || logical operator, only one of the expressions must be true. If the first expression evaluates true, no further checking is done. Note that "Jose" is quoted. If not quoted, the friend variable would be checked to see if it contained the pattern Jose. Jose would match, and so would Joseph. The expression evaluates to false because the second condition is not true. The exit status is 1.
+   3. Extended pattern matching is turned on with the built-in shopt command.
+   4. The variable is assigned the value Tommy.
+   5. In this test, the expression is tested for string equality using the new pattern-matching metacharacters. It tests if name matches a string starting with T or t, followed by an o, one or more # characters, and a y.

The following examples illustrate how the exit status is tested with the built-in test command and the alternate form of test, a set of single brackets [ ]; the compound command, a set of double brackets [[ ]].

# The let Command and Arithmetic with Double Parentheses.

Although the test command can evaluate arithmetic expressions, you may prefer to use the let command with its rich set of C-like operators (bash 2.x). The let command can be represented alternatively by enclosing its expression in a set of double parentheses.

Whether you are using the test command, compound command, or let command, the result of an expression is tested, with zero status indicating success and nonzero status indicating failure. (See Table 14.4.)
Example 14.18 illustrates how the let command uses double parentheses (( )).

# Table 14.4 The let Command Operators

| Operator | Meaning |
|---|---|
| - | Unary minus |
| + | Unary plus |
| ! | Logical NOT |
| ~ | Bitwise NOT (negation) |