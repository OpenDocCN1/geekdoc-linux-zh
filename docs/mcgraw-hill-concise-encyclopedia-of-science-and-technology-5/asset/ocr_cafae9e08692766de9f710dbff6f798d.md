![](bbox=[0.15, 0.04, 0.48, 0.2])

# **Fig. 2.** The definite integral.

that the same unit of length is used along the two axes.) This tangent is also called the slope of the curve.

The standard notation for the derivative of y with respect to x is dy/dx. If the functional notation *y = f(x)* is used, the derivative is often denoted by *f*(x). See DIFFERENTIATION.

If *f* is a function defined on the finite interval from x₁ to x₂ inclusive, the definite integral of *f* from x₁ to x₂, denoted by

```
$$\int_{x_1}^{x_2} f(x) dx$$
```

is defined by applying to *f* a rather intricate process which entails the consideration of what are called approximating sums. When the function *f* is subject to certain restrictions, this process culminates in the determination of a number as the limit of the approximating sums, and this number is called the definite integral of *f* from x₁ to x₂. The integral is not defined unless the approximating sums do converge to a well-defined limit. A sufficient condition that this is so is that the function *f* be continuous.

There is a geometrical representation of the process of defining the definite integral, and it furnishes a plausible argument for the convergence of the approximating sums to a limit. Divide the interval from x₁ to x₂ into a finite number *N* of not necessarily equal parts. Let the lengths of these parts be h₁, h₂, . . ., hₙ and let tₖ be the value of x in the kth part (Fig. 2). Then the expression

```
$$f(t_1)h_1 + f(t_2)h_2 + . . . + f(t_n)h_n$$
```

is called an approximating sum. In Fig. 2, where the function is continuous and the function values are all positive, each term is *f(tₖ)*hₖ in the approximating sum is equal to the area of a certain shaded rectangle, and the whole sum is an approximation of the area between the graph of the function and x axis, from x₁ to x₂ inclusive. The limiting process is carried on by the increasing *N* and making the largest of the hₖs approach 0. It is then intuitively clear that the definite integral is the number which represents the exact area between the x axis and the graph. This geometrical interpretation of the integral is the basis of an important application of integral calculus, to the calculation of areas.

It would be tedious and difficult in practice to compute definite integrals by actually working out the limits of approximating sums. It is however fortunate that by purely mathematical reasoning it is possible to demonstrate a theorem which links derivatives and integrals and makes it possible, in many important instances, to compute definite integrals by an easier procedure. See INTEGRATION.

The two fundamental theorems of calculus are as follows:

+   1.  For the calculation of

```
$$\int_{x_1}^{x_2} f(x) dx$$
```

find, if possible, a function *F* with continuous derivative *F*\' such that *F*\'(*x*) = *f*(*x*) when x₁ ≤ *x* ≤ x₂. Then Eq. (1) can be written

```
$$\int_{x_1}^{x_2} f(x) dx = F(x_2) - F(x_1) \qquad (1)$$
```

This is one of the two central theorems.

2. Suppose *f* is continuous, and consider the function *F* defined by Eq. (2).

```
$$F(x) = \int_{x_1}^{x} f(t)dt \qquad (2)$$
```

Then *F* has a derivative given by *F*\'(*x*) = *f*(*x*).

# ## Calculus of variations

An extension of the part of differential calculus which deals with maxima and minima of functions of a single variable. The functions of the calculus of variations depend in an essential way upon infinitely many independent variables. Classically these functions are usually integrals whose integrand depends on a function whose specification by any finite number of parameters is impossible. For example, let *C* be a smooth bounded region of a space of *n* variables, x₁, x₂, . . ., xₙ, let *y* any function of some smooth class on *C* and its boundary into real numbers or into *n*-tuples of real numbers and taking specified values on the boundary, and let *f*(x, *y*, p₁, p₂, . . ., pₙ) be a smooth function of 2n + 1 variables x₁, x₂, . . ., xₙ, *y*, p₁, p₂, . . ., pₙ. Then the integral, shown below, is a function on the space of functions *y* to the real numbers, and this space of functions is infinite dimensional unless excessive restrictions are placed on it. Here pᵢ denotes the derivatives ∂y/∂xᵢ.

The calculus of variations studies such functions and their maxima and minima. The limitation of the competing functions to arrive as realistically, and with sufficient restrictions it is possible to arrive at a rewarding theory; these restrictions do not always include the fixed boundary conditions stated above.

Principal applications may be to physical systems involving flexible components or time-dependent orbits; equilibrium positions or orbits may be determined by minimizing energy or action integrals. The problems of the mathematician are in part because of intrinsic difficulties (largely related to lack of topological compactness of bounded regions in spaces of infinitely many dimensions) and possibly because more progress with difficult nonlinear problems has been made here than elsewhere. See HAMILTON'S PRINCIPLE; LEAST-ACTION PRINCIPLE.

Much of the work on the calculus of variations is devoted to meticulous detail with regard to the number of derivatives assumed to be available for various functions, particularly the competitive admissible functions *y*(x). If too many derivatives are assumed, minima may not exist; if too few are assumed, the solution might not be sufficiently smooth to be acceptable in the light of the original statement of the problem. In an attempt to use fewer derivatives, different approaches are used depending on the number of independent variables x.

# ## Calculus of vectors

In its simplest form, a vector is a directed line segment. Physical quantities, such as velocity, acceleration, force, and displacement, are vector quantities, or simply vectors, because they can be represented by directed line segments. Vector analysis is a tool of the mathematical physicist, because many physical laws can be expressed in vector form. Two vectors *a* and *b* are added according to the parallelogram law (Fig. 1). An equivalent definition is as follows: From the end point of *a*, a vector is constructed parallel to *b*, of the same magnitude and direction as *b*. The vector from the origin of *a* to the end point of *b* builds the vector sum *s* = *a* + *b* (Fig. 2). Any number of vectors can be added by this rule.