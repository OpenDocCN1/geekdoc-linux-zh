Rabbits take one month to reach maturity. A mature pair of rabbits produces another pair of rabbits each month. If you start with one pair of newly born rabbits, how many pairs will you have after $n$ months?

We let $f_n$, for $n\geq 1$, be the number of pairs of rabbits alive after $n$ months. Thus $f_n$ is the number of pairs of rabbits, $f_{n-2}$, born to the rabbits who have reached maturity, plus the number, $f_{n-1}$, who were alive the previous month. Thus, for $n\geq 1$,

```
$$f_{n}=f_{n-2}+f_{n-1}.\tag{7.18}$$
```

We obtain the *Fibonacci numbers* when we solve this recurrence relation subject to the initial conditions

```
$$f_{1}=1 \text{ and } f_{2}=1.\tag{7.19}$$
```

Note that, except for a change of notation, the recurrence relation in Equation 7.18 is the same as in Equation 7.14. The only difference is that the initial conditions given by Equation 7.19 are different from those given by Equation 7.13.

The numbers in the sequence defined by Equations 7.18 and 7.19 are the Fibonacci numbers. It is easy to calculate the first few terms in the sequence:

+   $$\begin{gather*}1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, 1597, \dots, \end{gather*}$$

but can we find a simple formula for the numbers in this sequence? This was Problem 7 of Chapter 1. We now show how we can answer this question by finding the generating function for the sequence.

We let $F$ be the generating function for this sequence. Thus, $F(x)=\sum_{n\geq 1}f_{n}x^{n}$. If we multiply both sides of the recurrence relation in Equation 7.18 by $x^{n}$ and sum for all integers $n\geq 3$, we obtain

```
$$\sum_{n=3}^{\infty}f_{n}x^{n}=\sum_{n=3}^{\infty}f_{n-1}x^{n}+\sum_{n=3}^{\infty}f_{n-2}x^{n}.\tag{7.20}$$
```

The sum on the left-hand side of Equation 7.20 is just the series for $F(x)$ without the first two terms, that is, $\sum_{n=3}^{\infty}f_{n}x^{n}=F(x)-f_{1}x-f_{2}x^{2}=F(x)-x-x^{2}$. In a similar way, $\sum_{n=3}^{\infty}f_{n-1}x^{n}=x\sum_{n=3}^{\infty}f_{n-1}x^{n-1}=x(F(x)-x)$ and $\sum_{n=3}^{\infty}f_{n-2}x^{n}=x^{2}\sum_{n=3}^{\infty}f_{n-2}x^{n-2}=x^{2}F(x)$. Therefore, it follows from Equation 7.20 that

```
$$F(x)-x-x^{2}=x(F(x)-x)+x^{2} F(x).\tag{7.21}$$
```

Equation 7.21 can be rearranged to give

```
$$F(x)=\frac{x}{1-x-x^{2}}.\tag{7.22}$$
```