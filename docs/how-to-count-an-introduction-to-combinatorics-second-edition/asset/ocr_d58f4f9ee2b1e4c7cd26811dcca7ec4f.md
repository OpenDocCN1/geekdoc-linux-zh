of finding the coefficients $b_{n,k}$ arising when $x^n$ is expressed in terms of the falling factorial polynomials, so that

```
$x^{n}=b_{n,n} x(x-1).. (x-[n-1])+b_{n,n-1} x(x-1) .. (x-[n-2])+... +b_{n,2} x(x-1)+b_{n,1} x.$
```

The definition of falling factorial polynomials given above is fairly easy to grasp, but clearly a succinct notation would be a help. So for each integer $k>0$ we use $[x]_k$ for the falling factorial polynomial $x(x-1).. (x-[k-1])$. Note that the suffix $k$ indicates the degree of the polynomial.

# PROBLEM 5.1

Calculate the values of the numbers $a_{n,k}$ for $1 \leq n \leq 5$ and $1 \leq k \leq n$.

# Solution

```
[x]$_1$ = x
[x]$_2$ = x(x-1) = $x^{2}-x$
[x]$_3$ = $x(x-1)(x-2) = x^{3}-3x^{2} + 2x$
[x]$_4$ = $x(x-1)(x-2)(x-3) = x^{4}-6x^{3} + 11x^{2}-6x$
[x]$_5$ = $x(x-1)(x-2)(x-3)(x-4) = x^{5}-10x^{4} + 35x^{3}-50x^{2} + 24x$
```

Therefore we have Table 5.1 giving the numbers $a_{n,k}$ for $1 \leq n \leq 5$ and $1 \leq k \leq n$.

# PROBLEM 5.2

Calculate the numbers $b_{n,k}$, for $1 \leq n \leq 4$ and $1 \leq k \leq n$.

# Solution

```
[x]$_1$ = x, and hence $b_{1,1} = 1$.
[x]$_2$ = $x^{2}-x$, and hence $x^{2}=[x]_2 + x = [x]_2 + [x]_1$, Therefore $b_{2,2} = 1$ and $b_{2,1} = 1$.
[x]$_3$ = $x^{3}-3x^{2} + 2x$, and hence $x^{3}=[x]_3 + 3x^{2}-2x = [x]_3 + 3([x]_2 + [x]_1)-2[x]_1 = [x]_3 + 3[x]_2 + [x]_1$. Therefore $b_{3,3} = 1, b_{3,2} = 3$, and $b_{3,1} = 1$.
[x]$_4$ = $x^{4}-6x^{3} + 11x^{2}-6x$, and hence $x^{4}=[x]_4 + 6x^{3}-11x^{2} + 6x = [x]_4 + 6([x]_3 + 3[x]_2 + [x]_1)-11([x]_2 + [x]_1) + 6[x]_1 = [x]_4 + 6[x]_3 + 7[x]_2 + [x]_1$. Therefore $b_{4,4} = 1, b_{4,3} = 6, b_{4,2} = 7$, and $b_{4,1} = 1$.
```

TABLE 5.1

| | $k$ | | | | |
| --- | :---: | :---: | :---: | :---: | :---: |
| $a_{n,k}$ | 1 | 2 | 3 | 4 | 5 |
| $n$ | | | | | |
| 1 | 1 | | | | |
| 2 | 1 | 1 | | | |
| 3 | 2 | 3 | 1 | | |
| 4 | 6 | 11 | 6 | 1 | |
| 5 | 24 | 50 | 35 | 10 | 1 |