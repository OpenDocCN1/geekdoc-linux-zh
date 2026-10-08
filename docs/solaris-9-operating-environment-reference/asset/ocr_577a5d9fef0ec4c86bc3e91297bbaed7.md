# test 1401

(condition) true if condition is true. You can use the parentheses to alter the normal precedence and associativity. Notice also that parentheses are meaningful to the shell and therefore must be quoted.

The algorithm for determining the precedence of the operators and the return value is based on the number of arguments presented to test. (However, when you use the [...] form, the right-bracket final argument is not counted in this algorithm.) In the following list, $1, $2, $3, and $4 the arguments presented to test as a condition,ororcondition2.

+   0 arguments Exit false(1).
1 argument Exit true(0) if $1 is not null; otherwise, exit false.
2 arguments If $1 is !, exit true if $2 is not null, false if $2 is not null.
If $1 is a unary primary, exit true if the unary test is true, false if the unary test is false.
Otherwise, produce unspecified results.
3 arguments If $2 is a binary primary, perform the binary test of $1 and $3.
If $1 is !, negate the two-argument test of $2 and $3.
Otherwise, produce unspecified results.
4 arguments If $1 is !, negate the three-argument test of $2, $3, and $4.
Otherwise, the results are unspecified.

# Usage

Be careful when you write scripts that deal with user-supplied input that could be confused with primaries and operators. Unless you, the application writer, know all the cases that produce input to the script, write invocations like
test "$1" -a "$2"

as follows to avoid problems if a user supplied values such as $1 set to ! and $2 set to the null string.
test "$1" && test "$2"

```
In cases where maximal portability is of concern, replace
test expr1 -a expr2
```

```
with
test expr1 && test expr2
```

```
replace
test expr1 -o expr2
```

```
with
test expr1 || test expr2
```