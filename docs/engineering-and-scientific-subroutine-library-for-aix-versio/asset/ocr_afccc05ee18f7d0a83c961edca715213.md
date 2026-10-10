# SRCFT2 and DRCFT2

the next larger acceptable value returned in this argument. For details, see “Providing a Correct Transform Length to SSL” on page 38.

+   **n2** is the number of columns of data—that is, the length of the rows in arrays X and Y involved in the computation.
+   
+   Specified as: a fullword integer; *n2* ≤ 37748736 and must be one of the values listed in “Acceptable Lengths for the Transforms” on page 743. For all other values specified less than 37748736, you have the option of having the next larger acceptable value returned in this argument. For details, see “Providing a Correct Transform Length to SSL” on page 38.

+   **isign** controls the direction of the transform, determining the sign $\text{Isign}$ of the exponents of $W_{n1}$ and $W_{n2}$, where:
+   
+   If $\text{isign} =$ positive value, $	ext{Isign} = +$ (transforming time to frequency).
+   If $\text{isign} =$ negative value, $	ext{Isign} =$ (transforming frequency to time).
+   
+   Specified as: a fullword integer; $\text{isign} > 0$ or $\text{isign} < 0$.

+   **scale** is the scaling constant *scale*. See “Function” on page 796 for its usage.
+   
+   Specified as: a number of the data type indicated in Table 144 on page 793, where *scale* $> 0.0$ or *scale* $< 0.0$.

+   **aux1** is the working storage for this subroutine, where:
+   
+   If $\text{init} \neq 0$, the working storage is computed.
+   
+   If $\text{init} = 0$, the working storage is used in the computation of the Fourier transforms.
+   
+   Specified as: an area of storage, containing *aux1* long-precision real numbers.

+   **naux1** is the number of doublewords in the working storage specified in *aux1*.
+   
+   Specified as: a fullword integer; *naux1* $\ge$ (minimum value required for successful processing). To determine a sufficient value, use the processor-independent formulas. For all other values specified less than the minimum value, you have the option of having the minimum value returned in this argument. For details, see “Using Auxiliary Storage in SSL” on page 32.

+   **aux2** has the following meaning:
+   
+   If *naux2* $= 0$ and *error* 2015 is unrecoverable, *aux2* is ignored.
+   
+   Otherwise, it is the working storage used by this subroutine, which is available for use by the calling program between calls to this subroutine.
+   
+   Specified as: an area of storage, containing *naux2* long-precision real numbers. On output, the contents are overwritten.

+   **naux2** is the number of doublewords in the working storage specified in *aux2*.
+   
+   Specified as: a fullword integer, where:
+   
+   If *naux2* $= 0$ and *error* 2015 is unrecoverable, SRCFT2 and DRCFT2 dynamically allocate the work area used by the subroutine. The work area is deallocated before control is returned to the calling program.
+   
+   Otherwise, *naux2* $\ge$ (minimum value required for successful processing). To determine a sufficient value, use the processor-independent formulas. For all other values specified less than the minimum value, you have the