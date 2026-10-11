+   If the function is called in a floating-point context or all its arguments are floating-point values, the arguments are compared as floating-point values.

+   If neither of the preceding two rules apply, the arguments are compared as strings. String comparison rules are as described at the beginning of Section C.1.4,“Comparison Operators.”

```
GREATEST(2,3,1) → 3
GREATEST(38.5,94.2,-1) → 94.2
GREATEST('a','ab','abc') → 'abc'
GREATEST(1,3,5) → 5
GREATEST('A','b','C') → 'C'
GREATEST(BINARY 'A','b','C') → 'b'
```

+   **IF(**`expr1`, `expr2`, `expr3`**)**
+   If `expr1` is true (non-zero, non-NULL), returns `expr2`; otherwise, it returns `expr3`.
+   The return type for `IF()` is determined using the following tests, in order: A string, if `expr2` or `expr3` is a string; a floating-point value if either of them is a floating-point value; or an integer if either of them is an integer.

```
IF(1, 'true', 'false') → 'true'
IF(0, 'true', 'false') → 'false'
IF(NULL, 'true', 'false') → 'false'
IF(1,3, 'non-zero', 'zero') → 'non-zero'
IF(0.3 <> 0, 'non-zero', 'zero') → 'non-zero'
```

Note that the `IF()` function differs from the `IF` statement described in Section E.2.1,“Control Structure Statements.”

+   **IFNULL(**`expr1`, `expr2`**)**
+   Returns `expr2` if the value of the expression `expr1` is NULL; otherwise, it returns `expr1`. `IFNULL()` returns a number or string according to the context in which it is used.

```
IFNULL(NULL, 'null') → 'null'
IFNULL('not null', 'null') → 'not null'
```

+   **INTERVAL(**`n`, `n1`, `n2`, ...**)**
+   Returns `0` if `n` < `n1`, `1` if `n` < `n2`, and so on, or -1 if `n` is NULL. That is, `INTERVAL()` finds the position of the first argument within the intervals defined by the remaining arguments. All arguments must be integers. The values `n1`, `n2`, ... must be in strictly increasing order (`n1` < `n2` < ...) because a fast binary search is used. `INTERVAL()` behaves unpredictably otherwise.

```
INTERVAL(2,0,1,3) → 2
INTERVAL(7,1,3,5,7,9) → 4
```