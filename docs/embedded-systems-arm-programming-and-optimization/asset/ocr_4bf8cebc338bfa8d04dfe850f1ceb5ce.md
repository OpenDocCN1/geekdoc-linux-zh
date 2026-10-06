# Exercises 145

| A1 | A0 | B1 | B0 |
|---|---|---|---||
| 10 | 11 | X | 11 | 10 |

| A0*B0=32=6 |
| A0*B1<=2=9<=36 |
| A1*B0<=2=4<=16 |
| A1*B1<=4=6<=96 |

■ **FIGURE 3.6** An 8-bit multiplier implemented with 4-bit multipliers.

In the figure, 4-bit values A and B holding values $11_{10}$ and $14_{10}$ are each separated into 2-bit upper and lower portions, named A1, A0 and B1 and B0. Assuming the products are 4-bits, the 8-bit product is computed as $(A1*B1) \ll 4 + (A1*B0) \ll 2 + (A0*B1) \ll 2 + (A0*B0).

To apply this to a 64-bit multiply, each of the two 64-bit values must be held in two 32-bit registers. Each multiply generates a 64-bit result, allowing for a 128-bit final product.

+   d. Using these macros, implement a 64-bit Mandelbrot set generator and measure the resultant performance difference.
e. Implement both macros in inline assembly language and measure the result speedup of the Mandelbrot generator as compared to that part d.