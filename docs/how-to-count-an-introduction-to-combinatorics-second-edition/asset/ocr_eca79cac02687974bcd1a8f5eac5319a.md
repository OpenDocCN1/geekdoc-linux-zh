real numbers, so it also covers the case where some or all of the roots of the polynomial equation in Equation 7.61 are complex numbers.

We now come to the theory of nonhomogeneous linear recurrence relations, namely, recurrence relations of the form

$c_{0}a_{n} + c_{1}a_{n-1} + \ldots + c_{k} \, a_{n-k} = f(n)$, (7.67)

where $c_{0}$,$c_{1}$,$\ldots$,$c_{k}$ are constants, with $c_{k} \neq 0$, and where $f$ is some function. The *associated homogeneous recurrence relation* is

$c_{0}a_{n} + c_{1}a_{n-1} + \ldots + c_{k} \, a_{n-k} = 0$. (7.68)

The method we described and used in Section 7.6 can now be justified.

# THEOREM 7.3

The general solution of the nonhomogeneous linear recurrence relation in Equation 7.67 has the form

$\{a_{n} + b_{n}^{[i]}\}$,

where $\{b_{n}^{[i]}\}$ is one particular solution of Equation 7.67 and $\{a_{n}\}$ is any solution of the associated homogeneous recurrence relation in Equation 7.68.

**Proof**

Let $\{b_{n}^{[i]}\}$ be one particular solution of Equation 7.67, and let $\{a_{n}\}$ be any solution of Equation 7.68. Thus,

$c_{0}b_{n}^{[i]} + c_{1}b_{n-1}^{[i]} + ... + c_{k}b_{n-k}^{[i]} = f(n)$ (7.69)

and

$c_{0}a_{n} + c_{1}a_{n-1} + \ldots + c_{k} \, a_{n-k} = 0$. (7.70)

Adding Equations 7.69 and 7.70 gives