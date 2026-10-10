# SCOSF and DCOSF

# NAUX2 Formulas:

If $n \le 16384$, use $naux2 = 20000$.
If $n > 16384$, use $naux2 = 20000+64n$.
For the transposed case, where $inc2x = 1$ or $inc2y = 1$, and where $n \ge 252$, add the following to the above storage requirements:
$(n/2+252)(\min(128, m))$.

# Function

The set of $m$ real even discrete $n$-point Fourier transforms of the cosine sequences of real data in array $X$, with results going into array $Y$, is expressed as follows:

```
$$y_{ki} = scale \left( .5x_{0j} + .5(-1)^{k}x_{n/2,j} + \sum_{j=1}^{n/2-1}x_{ji}\cos(jk(2\pi/n)) \right)$$
```

for:

$k = 0, 1, ..., n/2$
$i = 1, 2, ..., m$

where:

- $x_{ji}$ are elements of the sequences in array $X$, where each sequence contains the $n/2+1$ real nonredundant data $x_{j0}, j = 0, 1, ..., n/2$.
- $y_{ki}$ are elements of the sequences in array $Y$, where each sequence contains the $n/2+1$ real nonredundant data $y_{k0}, k = 0, 1, ..., n/2$.
- $scale$ is a scalar value.

You can obtain the inverse cosine transform by specifying $scale = 4.0/n$. Thus, if an $X$ input is used with $scale = 1.0$, and its output is used as input on a subsequent call with $scale = 4.0/n$, the original $X$ is obtained. See references [1], [4], [21], and [22].

Two invocations of this subroutine are necessary:

1. With $init \ne 0$, the subroutine tests and initializes arguments of the program, setting up the $aux1$ working storage.
2. With $init = 0$, the subroutine checks that the initialization arguments in the $aux1$ working storage correspond to the present arguments, and if so, performs the calculation of the Fourier transforms.

These subroutines use a Fourier transform method with a mixed-radix capability. This provides maximum performance for your application.

# Error Conditions

**Resource Errors:** Error 2015 is unrecoverable, $naux2 = 0$, and unable to allocate work area.

**Computational Errors:** None

**Input-Argument Errors:**

1. $n > 37748736$
2. $inc1x$ or $inc1y \le 0$
3. $inc2x$ or $inc2y \le 0$
4. $m \le 0$
5. $scale = 0.0$
6. The subroutine has not been initialized with the present arguments.