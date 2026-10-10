# Processor-Independent Formulas for DCFT for NAUX1 and NAUX2

# NAUX1 Formulas::

If $n \leq 2048$, use $naux1 = 20000$.

If $n > 2048$, use $naux1 = 20000+2.28n$.

# NAUX2 Formulas::

If $n \leq 2048$, use $naux2 = 20000$.

If $n > 2048$, use $naux2 = 20000+2.28n$.

For the transposed case, where $inc2x = 1$ or $inc2y = 1$, and where $n \geq 252$, add the following to the above storage requirements: $(2n+256)(\min(64, m))$.

# Function

The set of $m$ complex discrete n-point Fourier transforms of complex data in array X, with results going into array Y, is expressed as follows:

```
$y_{ki} = scale \sum_{j=0}^{n-1} x_{j}W_{n}^{A(isgn)jk}$
```

for:

```
$k = 0, 1, ..., n-1$
$i = 1, 2, ..., m$
```

where:

```
$W_{n} = e^{-2\pi(\sqrt{-1})n}$
```

and where:

$x_{j}$ are elements of the sequences in array X.

$y_{ki}$ are elements of the sequences in array Y.

$isgn$ is + or – (determined by argument $isgn$),

$scale$ is a scalar value.

For $scale = 1.0$ and $isgn$ being positive, you obtain the discrete Fourier transform, a function of frequency. The inverse Fourier transform is obtained with $scale = 1.0/n$ and $isgn$ being negative. See references [1], [3], [4], [21], and [22].

Two invocations of this subroutine are necessary:

+   1. With $init \neq 0$, the subroutine tests and initializes arguments of the program, setting up the $aux1$ working storage.

+   2. With $init = 0$, the subroutine checks that the initialization arguments in the $aux1$ working storage correspond to the present arguments, and if so, performs the calculation of the Fourier transforms.

# Error Conditions

**Resource Errors:** Error 2015 is unrecoverable, $naux2 = 0$, and unable to allocate work area.

**Computational Errors:** None