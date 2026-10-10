
Our method for solving such nonhomogeneous recurrence relations is as follows. The theoretical justification for this method is given in Section 7.7.

## SOLVING NONHOMOGENEOUS RECURRENCE RELATIONS

To solve the nonhomogeneous recurrence relation

$c_{0}a_{n} + c_{1}a_{n-1} + \ldots + c_{k}a_{n-k} = f(n),$ (7.51)

1. Find the general solution, say $(y_{n})$, of the associated homogeneous recurrence relation
   $c_{0}y_{n} + c_{1}y_{n-1} + \ldots + c_{k}y_{n-k} = 0.$ (7.52)

2. Find any particular solution, say $(z_{n})$, of the nonhomogeneous recurrence relation in Equation 7.51.

3. Then the general solution of Equation 7.51 is given by
   $a_{n} = y_{n} + z_{n}$
   and the constants occurring in this solution can be found so as to satisfy any given initial conditions.

As we already know how to solve homogeneous recurrence relations, all we need to be able to solve nonhomogeneous equations is to find some way to come across a particular solution $(z_{n}).$ We illustrate one way this can be done by returning to the recurrence relation given in Equation 7.49, which we repeat for convenience:

$r_{n} - r_{n-1} = 2n^{2} - 3n + 2$ for $n \ge 2$ with $r_{1} = 0.$ [(7.49)]

We first need to solve the associated homogeneous recurrence relation

$r_{n} - r_{n-1} = 0.$ (7.53)

We couldn't ask for anything easier! By Equation 7.53 all the terms, $r_{n}$, are the same, so the general solution of Equation 7.53 is given by

$r_{n} = A,$ (7.54)

where $A$ is a constant.

Next, we seek a particular solution of Equation 7.49. The idea here is that if the difference between $r_{n}$ and $r_{n-1}$ is a polynomial of degree 2, we should look for a polynomial of degree 3 for $r_{n}$. The reason will emerge from the solution. (However, this is a special case because of the particular form of the left-hand side of Equation 7.49. In general, with a polynomial of degree $k$ on the right-hand side, we try to find a particular solution that is also a polynomial of degree $k$; see also Exercise 7.6.5A.) So we put

$r_{n} = \alpha n^{3} + \beta n^{2} + \gamma n + \delta.$ (7.55)

and aim to find values of $\alpha, \beta, \gamma$, and $\delta$ that satisfy Equation 7.49.

Substitution from Equation 7.55 into Equation 7.49 gives

$(\alpha n^3 + \beta n^2 + \gamma n + \delta) - (\alpha(n-1)^3 + \beta(n-1)^2 + \gamma(n-1) + \delta) = 2n^2 - 3n + 2$, that is,

$3\alpha n^2 + (-3\alpha + 2\beta)n + (\alpha - \beta + \gamma) = 2n^2 - 3n + 2$. (7.56)

The polynomials on the left- and right-hand sides of Equation 7.56 must be equal for all integers $n \geq 2$, and hence their coefficients must be equal. This gives

$3\alpha = 2$, $-3\alpha + 2\beta = -3$, $\alpha - \beta + \gamma = 2$, (7.57)

from which it follows that $\alpha = \frac{2}{3}$, $\beta = -\frac{1}{2}$, and $\gamma = \frac{5}{6}$. We cannot determine the value of $\delta$ from Equation 7.56, but this should not be a surprise because our general solution, Equation 7.54, of the associated homogeneous recurrence relation already involves an undetermined constant.

The general solution of the recurrence relation is the sum of the right hand sides of Equations 7.54 and 7.55, giving

$r_n = A + \left(\frac{2}{3}n^3 - \frac{1}{2}n^2 + \frac{5}{6}n + C\right)$. From the initial condition that $r_1 = 0$, we deduce that $A + 1 + C = 0$, giving $A + C = -1$. Hence the solution of Equation 7.49 is

$r_n = \frac{2}{3}n^3 - \frac{1}{2}n^2 + \frac{5}{6}n - 1$. (7.58)

This result shows that although the determinant of an $n \times n$ matrix involves $n!$ terms when expanded in full, and $n!$ increases extremely rapidly, the number of arithmetic operations needed to evaluate it by the row-reduction method only grows in proportion to $n^3$. This makes it possible to carry out calculations in linear algebra with very large matrices in a feasible amount of time.

As it happens, because the recurrence relation in Equation 7.49 is particularly simple, there is a more direct way to find this solution (see Exercise 7.6.6A). The next problem covers a more typical case.

## PROBLEM 7.9

Solve the recurrence relation $a_n - 5a_{n-1} + 6a_{n-2} = 2n^2$, subject to the initial conditions $a_1 = 28$ and $a_2 = 34$.

### Solution

The auxiliary equation is $x^2 - 5x + 6 = 0$ with solutions $x = 2$ and $x = 3$. So the general solution of the associated homogeneous equation is $a_n = A2^n + B3^n$. Because $n^2$ is a polynomial of degree 2 we try to find a particular solution of the same form, that is, with $a_n = \alpha n^2 + \beta n + \gamma$. Substituting this into the recurrence relation gives

$$(\alpha n^2 + \beta n + \gamma) - 5(\alpha(n - 1)^2 + \beta(n - 1) + \gamma) + 6(\alpha(n - 2)^2 + \beta(n - 2) + \gamma) = n^2 \ .$$

That is,

$$2\alpha n^2 + (-14\alpha + 2\beta) n + (19\alpha - 7\beta + 2\gamma) = 2n^2 .$$

Equating the coefficients of $n^2$ and $n$ and the constant terms gives $2\alpha = 2$, $-14\alpha + 2\beta = 0$, and $19\alpha - 7\beta + 2\gamma = 0$. Hence $\alpha = 1$, $\beta = 7$, and $\gamma = 15$. Therefore, the general solution of the nonhomogeneous recurrence relation is given by

$$a_n = A 2^n + B 3^n + n^2 + 7 n + 15 .$$

The initial conditions give $2A + 3B + 23 = 28$ and $4A + 9B + 33 = 34$, that is, $2A + 3B = 5$ and $4A + 9B = 1$. Hence $A = 7$ and $B = -3$. Therefore the solution is

$$a_n = 7(2^n) - 3(3^n) + n^2 + 7n + 15 .$$

### Exercises

- **7.6.1A** Find a formula for $a_n$ given that $a_n - 2a_{n-1} - 8a_{n-2} = 18 - 9n$, with $a_1 = 1$ and $a_2 = 3$.
- **7.6.1B** Find a formula for $a_n$ given that $a_n + 5a_{n-1} + 6a_{n-2} = 2n^2 - 21n^2 + 57n - 43$ for $n \geq 3$ with $a_1 = 1$ and $a_2 = 14$.
- **7.6.2A** Let $a_n$ be the number of sequences of length $n$ of letters of the English alphabet in which between them the five vowels, A, E, I, O, U, occur an even number of times.
    - i. Show that $a_1 = 21$ and that, for $n \geq 2$, $a_n = 16a_{n-1} + 5(26^{n-1})$.
    - ii. Find a formula for $a_n$.
- **7.6.2B** Let $a_n$ be the number of $n$-digit sequences formed using only the digits 0, 1, 2, and 3 in which 0 occurs an odd number of times.
    - i. Show that $a_n = 2a_{n-1} + 4^{n-1}$.
    - ii. Find a formula for $a_n$.
- **7.6.3A** Let $m$ and $n$ be positive integers with $m < n$. How many arithmetic operations are needed to row-reduce an $m \times n$ matrix to echelon form?
- **7.6.3B** Let $\mathbf{A}$ be an invertible (that is, nonsingular) $n \times n$ matrix. The inverse of $\mathbf{A}$ may be calculated by forming the $n \times 2n$ matrix $(\mathbf{A} \vert \mathbf{I}_n)$ by writing the $n \times n$ identity matrix $\mathbf{I}_n$ alongside $\mathbf{A}$ and then row-reducing this matrix to echelon form, thus obtaining a matrix of the form $(\mathbf{I}_n \vert \mathbf{B})$, where $\mathbf{B}$ is the inverse of $\mathbf{A}$. How many arithmetic operations are needed to calculate the inverse of $\mathbf{A}$ by this method?
- **7.6.4A** *The Tower of Hanoi*
    Suppose that we have three pegs. On one of these pegs there are $n$ disks of different sizes arranged in order of size with the largest disk at the bottom. The task is to transfer these $n$ disks to the third peg, by moving one disk at a time to another peg, subject to the rule that no disk may ever be placed on top of a smaller disk.

![](img/eb401bf41900fd678cd9d368a197e486_135_0.png)

(This is an old toy known, for no good reason as the Tower of Hanoi.) If, as the legend says,* in the great temple of Benares, the priests of Bramah are carrying out this task with 64 disks, and they move one disk each second, without making any mistakes, how long will it take before all the disks have been transferred and "tower, temple and Brahmins alike will crumble into dust, and with a thunder clap the world will vanish"?

- **7.6.4B** In this exercise we generalize the Tower of Hanoi problem to one with $n$ disks and $r(>3)$ pegs.

We let $T(n,r)$ denote the minimum number of moves needed to transfer the $n$ disks from one peg to another with, as usual, the restriction that no disk can be placed above a smaller one on the same peg. The Frame Stewart algorithm is as follows.

For each $k$, $1 \le k \le n-1$:
    - i. Move the top $k$ disks (legally) to another peg;
    - ii. Move the remaining $n-k$ disks (legally) to one of the remaining pegs;
    - iii. Move the $k$ disks (legally) to the peg containing the $n-k$ disks.

Deduce that, for $1 \le k \le n-1$, we have $T(n,r) \le 2T(k,r) + T(n-k,r-1)$. Using this inequality find upper bounds for the values of $T(n,4)$ for $1 \le n \le 8$.

- **7.6.5A** Show that
    - i. It is not possible to find a particular solution of Equation 7.49 of the form $r_n = En^2 + Dn + C$, where $C$, $D$, and $E$ are constants.
    - ii. The recurrence relation $r_n - 2r_{n-1} = 2n^2 - 3n + 2$ has a solution of the form $r_n = En^2 + Dn + C$, where $C$, $D$, and $E$ are constants.
- **7.6.5B** Show that the recurrence relation $r_n - r_{n-1} = n^3$ has solutions of the form $r_n = Gn^4 + Fn^3 + En^2 + Dn + C$.
- **7.6.6A** i. Show that the solution of the recurrence relation

$$r_n - r_{n-1} = f(n)$$

is given by $r_n = r_1 + \sum_{k=2}^{n} f(k)$, for $n \ge 2$.
