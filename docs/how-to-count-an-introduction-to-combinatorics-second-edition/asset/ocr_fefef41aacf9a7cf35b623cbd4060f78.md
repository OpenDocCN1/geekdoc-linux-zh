We illustrate this idea by finding the formula for the generating function for the Catalan numbers, $C_{n}$, as described in Chapter 5. Recall that we have specified that $C_{0}=1$ and that, by Theorem 5.8, we have that for each integer $n \geq 1$, $C_{n+1} = \sum_{k=0}^{n} C_{k} C_{n-k}$. This formula should remind you of the formula in Equation 7.4 for multiplying power series. If we let $C$ be the generating function for the Catalan numbers, that is, $C(x) = \sum_{n=0}^{\infty} C_{n} x^{n}$, then, by Equation 7.4, $(C(x))^{2} = \sum_{n=0}^{\infty} d_{n} x^{n}$, where $d_{n} = \sum_{k=0}^{n} C_{k} C_{n-k}$, and thus $d_{n} = C_{n+1}$. Hence $(C(x))^{2} = \sum_{n=0}^{\infty} C_{n+1} x^{n}$. Therefore $x(C(x))^{2} \equiv \sum_{n=0}^{\infty} C_{n+1} x^{n+1} = C(x)-1$. Therefore, writing $C$ for $C(x)$ we have that

$x(C^{2}-C+1=0$,  (7.73)

Solving Equation 7.73 by the standard formula, we have that, for $x \neq 0$,

$C= \frac{1 \pm \sqrt{1-4x}}{2x}$,  (7.74)

Using the power series expansion for $\sqrt{1-4x}$, Equation 7.74 may be used to derive the formula $C_{n} = \frac{1}{(1/n+1)} C(2n,n)$ for the Catalan numbers. You are asked to do this in Exercise 7.8.1A. Another example of this type is given in Exercise 7.8.1B.

# **Exercises**

**7.8.1A** Deduce from Equation 7.73 that, for all positive integers $n$, $C_{n} = \frac{1}{(1/n+1)} C(2n,n)$.

*Hint: The power series expansion for $\sqrt{1-4x}$, that is, $(1-4x)^{1/2}$ may be derived either from the general binomial theorem

$(1+x)^{\alpha} = 1+\alpha x + \frac{\alpha(\alpha-1)}{2!}x^{2} + \frac{\alpha(\alpha-1)(\alpha-2)}{3!}x^{3} + ...$

in the case where $x$ is replaced by $-4x$ and $\alpha$ by $\frac{1}{2}$, or from Taylor's theorem, namely, that, for an infinitely differentiable function $f$,

$f(x) = f(0) + f'(0)x + \frac{f''(0)}{2!} x^{2} + \frac{f'''(0)}{3!} x^{3} + ...$

**7.8.1B** Find a formula for the generating function of the sequence $\{a_{n}\}$ defined by $a_{0}=a_{1}=1$, and for $n \geq 2$, $a_{n} = a_{n-1} + \sum_{i=0}^{n-2} a_{i}a_{n-1-i}$.