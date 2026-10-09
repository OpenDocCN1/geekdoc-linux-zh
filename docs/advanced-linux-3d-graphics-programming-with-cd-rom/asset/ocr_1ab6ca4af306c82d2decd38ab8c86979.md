We can simplify the solution for *u* further. A naive attempt to apply the simplify and normalize-rational commands to the entire expression at once results in Calc reporting a “division by 0” error. But the expression can be simplified. By simplifying and normalizing the equation piece for piece using selections, and by collecting terms for *x*, *y*, *z*, *ux*, *uy*, and *uz*, the expression finally simplifies to the form shown in Figure 2-35. I encourage you to try to arrive at the same result yourself by using Calc.

![](bbox=[0.67, 0.25, 0.85, 0.4])

By repeating the solution procedure for variables *v* and *w*, we arrive at the following simplified solutions for *u*, *v*, and *w*:

Equation 2-23
$u = \frac{x(v_z w_y - v_y w_z) + y(v_z w_x - v_x w_z) + z(v_y w_x - v_x w_y) + o_x(v_y w_z - v_z w_y) + o_y(v_x w_z - v_z w_x) + o_z(v_x w_y - v_y w_x)}{u_z(v_z w_y - v_y w_z) + u_y(v_z w_x - v_x w_z) + u_x(v_y w_x - v_x w_y)}$
$v = \frac{x(u_z w_y - u_y w_z) + y(u_z w_x - u_x w_z) + z(u_y w_x - u_x w_y) + o_x(u_y w_z - u_z w_y) + o_y(u_x w_z - u_z w_x) + o_z(u_x w_y - u_y w_x)}{u_x(v_z w_y - v_y w_z) + u_y(v_z w_x - v_x w_z) + u_z(v_y w_x - v_x w_y)}$
$w = \frac{x(u_z v_y - u_y v_z) + y(u_z v_x - u_x v_z) + z(u_y v_x - u_x v_y) + o_x(u_y v_z - u_z v_y) + o_y(u_x v_z - u_z v_x) + o_z(u_x v_y - u_y v_x)}{u_x(v_z w_y - v_y w_z) + u_y(v_z w_x - v_x w_z) + u_z(v_y w_x - v_x w_y)}$

These equations are the solution to the world-to-texture-space problem. Given variables *x*, *y*, and *z* representing world space coordinates, and a texture space definition as specified by the *O* point and vectors *U*, *V*, and *W*, these equations give us the equivalent coordinates *u*, *v*, and *w* in texture space. As you can see, the solution is not completely intuitive, and would have been rather tedious to derive by hand.

There is still more structure to be discovered in these equations. Notice the recurring pairs of differences which appear: (*vz wy – vy wz*), (*vx wz – vz wx*), and so forth. These terms are actually components of cross product vectors. In particular, the solution for *u* contains the components of the cross product vector *V W*; the solution for *v* contains the components of *U W*; the solution for *w* contains the components of *V U*. The denominator in each case is *U*( *V W* ). Making this simplification, and recasting the equation into matrix form, gives us Equation 2-24. The subscripts on each cross product expression mean to take the corresponding component of the vector after the cross product operation. For instance, (*V W*)*x* means to take the cross product of vectors *V* and *W*, and to use the *x* component of the resulting vector.

Equation 2-24
$\begin{bmatrix} (W \times V)_x & (W \times V)_y & (W \times V)_z \\ (U \times W)_x & (U \times W)_y & (U \times W)_z \\ (V \times U)_x & (V \times U)_y & (V \times U)_z \end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \begin{bmatrix} u \\ v \\ w_{tex} \end{bmatrix}$