Because `||` and `&&` have equal precedence, the parentheses in the two preceding pairs of examples do not change the order of operations.

Because the expression on the right side of a short-circuiting operator may never be executed, you must be careful when placing assignment statements in that location. The following example demonstrates what can happen:

```
$ ((N=10,Z=0))
$ echo $((N || (Z+=1)))
1
$ echo $Z
0
```

Because the value of N is nonzero, the result of the `||` (OR) operation is 1 (*true*), no matter what the value of the right side is. As a consequence, `(Z+=1)` is never evaluated and Z is not incremented.

The ternary operator, `?:`, decides which of two expressions should be evaluated, based on the value returned by a third expression:

```
*expression*1 ? *expression*2 : *expression*3
```

If *expression*1 produces a *false* (0) value, *expression*3 is evaluated; otherwise, *expression*2 is evaluated. The value of the entire expression is the value of *expression*2 or *expression*3, depending on which is evaluated. If *expression*1 is *true*, *expression*3 is not evaluated. If *expression*1 is *false*, *expression*2 is not evaluated.

```
$ ((N=10,Z=0,COUNT=1))
$ ((T=N>COUNT?++Z:--Z))
$ echo $T
1
$ echo $Z
1
```

The assignment operators, such as `+=`, are shorthand notations. For example, `N+=3` is the same as `((N=N+3))`.

The following commands use the syntax *base*#n to assign base 2 (binary) values. First v1 is assigned a value of 0101 (5 decimal) and then v2 is assigned a value of 0110 (6 decimal). The `echo` utility verifies the decimal values.

```
$ ((v1=2#0101))
$ ((v2=2#0110))
$ echo "$v1 and $v2"
5 and 6
```

Next the bitwise AND operator (&c;) selects the bits that are on in both 5 (0101 binary) and 6 (0110 binary). The result is binary 0100, which is 4 decimal.

```
$ echo $((v1 & v2))
4
```