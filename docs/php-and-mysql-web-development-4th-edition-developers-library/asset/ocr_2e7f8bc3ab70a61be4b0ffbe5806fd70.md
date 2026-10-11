+   * `<=`
+   
+     Evaluates to 1 if the left operand is less than or equal to the right operand, 0 otherwise.
+     ```
+     'abc' <= 'a'                   → 0
+     'a' <= 'abc'                   → 1
+     13.5 <= 14                    → 1
+     (3 * 4) - (6 * 2) <= 0        → 1
+     ```

+   * `>`
+   
+     Evaluates to 1 if the left operand is greater than the right operand, 0 otherwise.
+     ```
+     PI() > 3                       → 1
+     'abc' > 'a'                   → 1
+     SIN(0) > COS(0)               → 0
+     ```

+   * `>=`
+   
+     Evaluates to 1 if the left operand is greater than or equal to the right operand, 0 otherwise.
+     ```
+     'abc' >= 'a'                   → 1
+     'a' >= 'abc'                  → 0
+     13.5 >= 14                    → 0
+     (3 * 4) - (6 * 2) >= 0        → 1
+     ```

+   * `expr BETWEEN min AND max`
+     `expr NOT BETWEEN min AND max`
+   
+     BETWEEN evaluates to 1 if `expr` lies within the range of values spanned by `min` and `max` (inclusive), 0 otherwise. For `NOT BETWEEN`, the opposite is true. If the operands `expr`, `min`, and `max` are all of the same type, these expressions are equivalent:
+   
+     ```
+     expr BETWEEN min AND max
+     (min <= expr AND expr <= max)
+     ```
+   
+     If the operands are not of the same type, type conversion occurs and the two expressions may not be equivalent. BETWEEN is evaluated using comparisons determined according to the type of `expr`:

+   * If `expr` is a string, the operands are compared lexically as strings, using the rules given at the beginning of this section.
+   * If `expr` is an integer, the operands are compared numerically as integers.
+   * If neither of the preceding rules is true, the operands are compared numerically as floating-point numbers.
+   
+   ```
+   'def' BETWEEN 'abc' AND 'ghi'   → 1
+   'def' BETWEEN 'abc' AND 'def'   → 1
+   13.3 BETWEEN 10 AND 20         → 1
+   ```