mention a cramped hand. Most of the work involved in solving this system of equations seems tedious, repetitive, manual, and error-prone. It seems like a perfect job for the computer. The Calc package can help us here. So, let's now take a detour to look at how to use the Calc package to solve this system of equations.

> **NOTE** If you are uninterested in understanding how to solve the system of equations, you can skip this section and just use the results. However, I sincerely hope that you take the time to learn to use Calc and to understand how to solve such problems using Calc as a tool. Sooner or later, every 3D programmer will be confronted with solving systems of equations. A technique as ubiquitous as texture mapping cannot be fully understood without understanding the solutions to the equations.

# Calc: A Symbolic Algebra Package

Calc is a free (zero cost and open source) mathematical tool which runs as part of the Emacs environment. It can perform numeric and symbolic mathematical manipulations. Its ability to perform numeric math operations means that Calc can compute quantities specified as numbers, just as with a normal desk calculator-for instance, (37-140)/15.3. Its ability to perform symbolic math operations means that Calc can solve systems of equations specified algebraically in terms of known and unknown variables. For the problem at hand-converting from world space to texture space-we are mostly interested in the symbolic capabilities of Calc.

Here is an example of Calc's symbolic capabilities. If we have the system of equations:

**Equation 2-21**
$x + y = k$
$x - y = 3k$

then Calc can automatically solve this system of equations for *x* and *y* to give us the solution:

**Equation 2-22**
$x = 2k$
$y = -k$

Internally, therefore, Calc has performed the typical grade school algebraic manipulations for solving systems of equations. For this example, the equations are very easy to solve by hand, but in the case of inverting the texture space to world space matrix, the system of equations is quite simply tedious to solve by hand. The symbolic algebra capabilities of Calc relieve us of exactly this burden. Let's first take a brief tour of how to use Calc, then focus on using the symbolic algebra capabilities to solve the texture mapping equations.

> **NOTE** Calc has excellent online info documentation, including many hands-on tutorials. Alternatively, within Calc, press ? and type i to display the info documentation from within Calc. Since we don't have enough space here to describe all of Calc's features-many of which are very interesting and useful for solving the types of problems which arise in 3D graphics-I encourage you to have a look at Calc's info documentation.

# Starting and Exiting Calc

To use Calc, you must have both Emacs and the Calc package installed, and you must know how to do basic editing in Emacs. See the Appendix for instructions on installing Calc.

*TEAM LinG - Live, Informative, Non-cost and Genuine!*