Function

The computation is expressed as follows:
$z_i \leftarrow x_i y_i \quad \mathrm{for} \ i = 1, n$

If $n$ is 0, no computation is performed. For CVEM, intermediate results are accumulated in long precision (short-precision Multiply followed by a long-precision Add), with the final result truncated to short precision.

Error Conditions

Computational Errors: None

Input-Argument Errors: $n < 0$

Example 1

This example shows vectors $x$, $y$, and $z$, with positive strides.

Call Statement and Input:

N X INCX Y INCY Z INCZ
$egin{array}{c} 5 \ \downarrow \end{array}$
$egin{array}{c} X \ \downarrow \end{array}$
$egin{array}{c} 1 \ \downarrow \end{array}$
$egin{array}{c} Y \ \downarrow \end{array}$
$egin{array}{c} 2 \ \downarrow \end{array}$
$egin{array}{c} Z \ \downarrow \end{array}$
$egin{array}{c} 1 \ \downarrow \end{array}$
CALL SVEM( 5 , X , 1 , Y , 2 , Z , 1 )

X = (1.0, 2.0, 3.0, 4.0, 5.0)
Y = (1.0, . , 1.0, . , 1.0, . , 1.0, . , 1.0)

Output:
Z = (1.0, 2.0, 3.0, 4.0, 5.0)

Example 2

This example shows vectors $x$ and $y$ having strides of opposite sign, and an output vector $z$ having a positive stride. For $y$, which has negative stride, processing begins at element $Y(5)$, which is 1.0.

Call Statement and Input:

N X INCX Y INCY Z INCZ
$egin{array}{c} 5 \ \downarrow \end{array}$
$egin{array}{c} X \ \downarrow \end{array}$
$egin{array}{c} 1 \ \downarrow \end{array}$
$egin{array}{c} Y \ \downarrow \end{array}$
$egin{array}{c} -1 \ \downarrow \end{array}$
$egin{array}{c} Z \ \downarrow \end{array}$
$egin{array}{c} 2 \ \downarrow \end{array}$
CALL SVEM( 5 , X , 1 , Y , -1 , Z , 2 )

X = (1.0, 2.0, 3.0, 4.0, 5.0)
Y = (5.0, 4.0, 3.0, 2.0, 1.0)

Output:
Z = (1.0, . , 4.0, . , 9.0, . , 16.0, . , 25.0)

Example 3

This example shows a vector, $x$, with 0 stride, and a vector, $z$, with negative stride. $x$ is treated like a vector of length $n$, all of whose elements are the same as the single element in $x$. For vector $z$, results are stored beginning in element $Z(5)$.

Call Statement and Input:

N X INCX Y INCY Z INCZ
$egin{array}{c} 5 \ \downarrow \end{array}$
$egin{array}{c} X \ \downarrow \end{array}$
$egin{array}{c} 0 \ \downarrow \end{array}$
$egin{array}{c} Y \ \downarrow \end{array}$
$egin{array}{c} 1 \ \downarrow \end{array}$
$egin{array}{c} Z \ \downarrow \end{array}$
$egin{array}{c} -1 \ \downarrow \end{array}$
CALL SVEM( 5 , X , 0 , Y , 1 , Z , -1 )

X = (1.0)
Y = (5.0, 4.0, 3.0, 2.0, 1.0)

Output:
Z = (1.0, 2.0, 3.0, 4.0, 5.0)