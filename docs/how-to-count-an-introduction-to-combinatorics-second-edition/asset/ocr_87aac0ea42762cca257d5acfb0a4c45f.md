x₁,x₂,…,xₖ will usually be natural numbers, and the constants will normally be rational numbers. However, to allow for all possibilities, we could say that they are all real numbers, or even complex numbers, so that the domain of $f$ is $\mathbb{R}^{n}$ or $\mathbb{C}^{n}$.)

*A homogeneous linear recurrence relation* is a recurrence relation of the form

```
a<sub>n</sub> = f(a<sub>n-1</sub>,a<sub>n-2</sub>,…,a<sub>n-k</sub>)	(7.35)
```

where f is a linear function, with $1≤k<n$. The Equation 7.35 brings out the fact that we can use it to calculate a<sub>n</sub> in terms of the previous k terms of the sequence, but in some ways it is more natural to write the equation in the form

```
a<sub>n</sub> − f(a<sub>n-1</sub>,a<sub>n-2</sub>,…,a<sub>n-k</sub>) = 0	(7.36)
```

and thus we can give the following alternative definition.

# DEFINITION 7.2

*A homogeneous linear recurrence relation* is a recurrence relation of the form

```
c<sub>0</sub>a<sub>n</sub> + c<sub>1</sub>a<sub>n-1</sub> + … + c<sub>k</sub>a<sub>n-k</sub> = 0	(7.37)
```

for some integer k, where $1≤k<n$, and where c<sub>0</sub>c<sub>1</sub>…c<sub>k</sub> are constants with c<sub>k</sub> ≠ 0. (Of course, if Equation 7.37 is identical with Equation 7.36, c<sub>0</sub> is 1, but we allow for other values of c<sub>0</sub>.)

The term *homogeneous* is rather a mouthful. It is used to indicate that the right-hand side of Equation 7.36 is 0. We leave the more complicated case of nonhomogeneous linear recurrence relations until later. It will be readily seen that the Fibonacci sequence is defined by a homogeneous linear recurrence relation and that Problem 7.5 also leads to a homogeneous linear recurrence relation.

We illustrate our direct method by returning to this example. We begin by rewriting Equation 7.29 as

```
a<sub>n</sub> − 4a<sub>n-1</sub> − 12a<sub>n-2</sub> = 0	(7.38)
```

```
with a<sub>1</sub> = 7 and a<sub>2</sub> = 40.	(7.39)
```

The idea of the method is to try to find a solution of Equation 7.38 of the form a<sub>n</sub> = xⁿ. This may seem a bold idea, but it does not come completely out of the blue, as we have seen that the formula for the Fibonacci numbers involves expressions of the form xⁿ with $x = \frac{1}{2}(1 ± \sqrt{5})$, and that the solution of Equation 7.38 involves 6ⁿ and (−2)ⁿ. However, it remains to see whether it works. If we put a<sub>n</sub> = xⁿ in Equation 7.38, we obtain

```
xⁿ − 4xⁿ⁻¹ − 12xⁿ⁻² = 0	(7.40)
```