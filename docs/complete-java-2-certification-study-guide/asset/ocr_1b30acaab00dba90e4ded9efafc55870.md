# The Short-Circuit Logical Operators 59

If the String reference s is null, calling the s.length() method would raise a NullPointerException. In both of these examples, the situation never arises. The second example, avoiding execution of the s.length() method is a direct consequence of the short-circuit behavior of the && operator. If the test (s != null) returns false (if s is in fact null), then the whole test is guaranteed to be false. Where the first operand is false, the && operator does not evaluate the second operand;so, in this case, the expression (s.length() > 20) is not evaluated.

Although these shortcuts do not affect the result of the operation, side effects might be changed. If the evaluation of the right operand involves a side effect, then omitting the evaluation will change the overall meaning of the expression in some way. This behavior distinguishes these operators from the bitwise operators applied to boolean types. Consider these fragments:

//first example:

+   1. int val = (int)(2 * Math.random());
2. boolean test = (val == 0) || ((val == 2);
3. System.out.println('test = ' + test + '\nval = ' + val);

//second example:

+   1. int val = (int)(2 * Math.random());
2. boolean test = (val == 0) | ((val == 2);
3. System.out.println('test = ' + test + '\nval = ' + val);

The first example will print

```
test = true
val = 0
```

and sometimes it will print

```
test = true
val = 2
```

The second example will sometimes print

```
test = true
val = 1
```

and sometimes it will print

```
test = true
val = 2
```

The point is that in the case of the short-circuit operator, if val starts at 0, then the second part of the expression (++val) is never executed, and val remains at 0. Alternatively, val starts at 1 and is incremented to 2. In the second case, the non-short-circuit version, the increment