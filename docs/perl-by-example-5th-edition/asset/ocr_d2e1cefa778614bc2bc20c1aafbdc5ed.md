# EXPLANATION

+   1. The *scalar* `$_` is set to the current hour. The *localtime* built-in function returns the hour, the third element of the array of time values.
+   2. The `if` statement tests whether the value of `$_` is greater than or equal to `0` and less than `12`. The result of the evaluation is true, so the block following the control expression is executed (that is, the `print` statement is executed).
+   3. If the first `if` test is false, this expression is tested. If the value of `$_` is equal to `12`, the `print` statement is executed.
+   4. If the previous `elsif` test failed, and this `elsif` expression evaluates to true, the `print` statement will be executed.
+   5. If none of the above statements is true, the `else` statement, the default action, is executed.

# The *unless* Construct

The `unless` statement is similar to the `if` statement, except that the control expression after the `unless` is tested for the reverse condition; that is, if the conditional expression following the `unless` is false, the statement block is executed.

The `unless/else` and `unless/elsif` behave in the same way as the `if/else` and `if/elsif` statements with the same reversed test as previously stated.

# FORMAT

```
unless (Expression) {Block}
unless (Expression) {Block}	else (Block)
unless (Expression) {Block}	elsif (Expression)
	(Block),... else (Block)
```

# EXAMPLE 7.4

```
(The Script)

use warnings;
print "How old are you? ";
chomp($age = <STDIN>);
unless ($age <= 21) { # If false, enter the block
	print "Let's party!\n";
}
print "You said you were $age.\n";

(Output)

How old are you? 32
Let's party!
You said you were 32.
---Run the program again---

(Output)

How old are you? 10
You said you were 10.
```