# Arithmetic evaluation versus arithmetic expansion

**Tip** Arithmetic evaluation differs from arithmetic expansion. As explained on page 408, arithmetic expansion uses the syntax `$(expression)`, evaluates *expression*, and replaces `$(expression)` with the result. You can use arithmetic expansion to display the value of an expression or to assign that value to a variable.

Arithmetic evaluation uses the *let expression* or `((expression))` syntax, evaluates *expression*, and returns a status code. You can use arithmetic evaluation to perform a logical comparison or an assignment.

You can use the `((expression))` syntax for logical expressions, although that task is frequently left to `[expression]` (next). The next example expands the *age_check* script (page 408) to include logical arithmetic evaluation in addition to arithmetic expansion:

```
`$ cat age2
#!/bin/bash
read -p "How old are you? " age
if ((30 < age && age < 60)); then
    echo "Wow, in $((60-age)) years, you'll be 60!"
else
    echo "You are too young or too old to play."
fi

$ ./age2
How old are you? 25
You are too young or too old to play.`
```

The *test-statement* for the *if* structure evaluates two logical comparisons joined by a Boolean AND and returns 0 (*true*) if they are both *true* or 1 (*false*) otherwise.

# LOGICAL EVALUATION (CONDITIONAL EXPRESSIONS)

The syntax of a conditional expression is

`[[ expression ]]`

where *expression* is a Boolean (logical) expression. You must precede a variable name with a dollar sign ($) within *expression*. The result of executing this built-in, as with the *test* built-in, is a return status. The *conditions* allowed within the brackets are almost a superset of those accepted by *test* (page 983). Where the *test* built-in uses `-a` as a Boolean AND operator, `[[ expression ]]` uses `&&`. Similarly, where *test* uses `-o` as a Boolean OR operator, `[[ expression ]]` uses `||`.

To see how conditional expressions work, replace the line that tests *age* in the *age2* script with the following conditional expression. You must surround the `[` and `]]` tokens with whitespace or a command terminator, and place dollar signs before the variables:

```
`if [[ 30 < $age && $age < 60 ]]; then`
```

You can also use *test*'s relational operators `-gt`, `-ge`, `-lt`, `-le`, `-eq`, and `-ne:`

```
`if [[ 30 -lt $age && $age -lt 60 ]]; then`
```