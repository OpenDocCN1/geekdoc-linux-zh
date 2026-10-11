The two-argument form returns the logarithm of $x$ to the base $b$.

```
LOG(10,100) → 2
LOG(2,256) → 8
```

You can also compute the logarithm of $x$ to the base $b$ using LOG ($x$) /LOG($b$) .

```
LOG(100)/LOG(10) → 2
LOG10(100) → 2
```

+   LOG10 ($x$)

Returns the logarithm of $x$ to the base 10.

```
LOG10(0) → NULL
LOG10(10) → 1
LOG10(100) → 2
```

+   LOG2 ($x$)

Returns the logarithm of $x$ to the base 2.

```
LOG2(0) → NULL
LOG2(255) → 7.99435434368589
LOG2(32767) → 14.999955597177
```

LOG2 ( ) tells you the “width” of a value in bits. One use for this is to assess the amount of storage required for the value.

+   MOD ($m, n$)

MOD ( ) performs a modulo operation. MOD ($m, n$ ) function syntax is the same as $m \% n$ or $m \text{ MOD } n$ operator syntax (see Section C.1.3, “Arithmetic Operators”).

+   PI ()

Returns the value of $\pi$ .

```
PI() → 3.141593
```

+   POW ($x, y$)

Returns $x^{y}$, that is, $x$ raised to the power $y$ .

```
POW (2,3) → 8
POW (2,-3) → 0.125
POW (4,-5) → 2
POW (16, ,25) → 2
```

+   RADIANS ($x$)

Returns the value of $x$, converted from degrees to radians.

```
RADIANS(0) → 0
RADIANS(360) → 6.2831853071796
RADIANS(-360) → -6.2831853071796
```