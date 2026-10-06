
Gaussian elimination performs successive row transformations on the concatenated matrix having the objective of transforming the left-side of the concatenated matrix—the original A matrix—into the identity and the right side into the inverted form of A.

This requires three discrete steps. The first step is to convert the matrix into triangular form, in which the transformations systematically set each element of the bottom triangle to zeros beginning with the lower-left element and each element along each upper-left to lower-right diagonal as shown below.

![](img/e6ebc663bbb86c6e7bf9ef22ad136e6f_247_0.png)

For purpose of this simple example, assume that the original A matrix contains no zero elements. This allows the matrix to be converted to triangular form using the following row transformations:

- 1. set element (3,0) to zero R3 → R3−($A_{3,0}/A_{2,0}$)R2
- 2. set element (2,0) to zero R2 → R2−($A_{2,0}/A_{1,0}$)R1
- 3. set element (3,1) to zero R3 → R3−($A_{3,1}/A_{2,1}$)R1
- 4. set element (1,0) to zero R1 → R1−($A_{1,0}/A_{0,0}$)R0
- 5. set element (2,1) to zero R2 → R2−($A_{2,1}/A_{1,1}$)R1
- 6. set element (3,2) to zero R3 → R3−($A_{3,2}/A_{2,2}$)R1

This gives the result:

| R0 | 1.0 | 2.0 | 3.0 | 1.0 | 0.0 | 0 | 0 |
| R1 | 0 | -3.0 | -2.0 | -1.0 | -2.0 | 1.0 | 0 | 0 |
| R2 | 0 | 0 | -10.3 | -2.7 | -2.3 | -1.3 | 1.0 | 0 |
| R3 | 0 | 0 | 0 | 0.9 | 1.2 | -1.0 | -1.2 | 1 |

Assuming the input matrix is stored in row-major order in array a and the identity matrix is stored in array b, the code that performs this is as follows:

```
for (i=3; i>0; i--) {
    for (j=0; j<4; j++) {
        coeff = -a[(i+j)*4+j]/a[((i+j)-1)*4+j];
        for (k=0; k<4; k++) {
            b[(i+j)*4+k] += coeff * b[((i+j)-1)*4+k];
            a[(i+j)*4+k] += coeff * a[((i+j)-1)*4+k];
        }
    }
}
```

# APPENDIX B NEON Intrinsic Reference

gcc 4.8.2 does not generate any NEON SIMD instructions when compiling this code, even when requesting maximum optimization and specifically identifying their target architecture and NEON support (using the -O3 -mfpu=neon -march=armv7-a switches).

The programmer can replace the entire innermost loop (the k-loop) with two 4-wide (quad) VMLAQ (multiply-accumulate quad) intrinsics, using:

```
*((float32x_t*)&bb((i+j)*4)));

vmlaq_f32(*(float32x_t*)&bb((i+j)*4));

*((float32x_t*)&ba((i+j)*4)));

dupq_n_f32(coeff));

*((float32x_t*)&a((i+j)*4)));

vmlaq_f32(*(float32x_t*)&a((i+j)*4));

*((float32x_t*)&a((i+j)*4)));

dupq_n_f32(coeff));
```

The a- and b-arrays must be referenced, as float32x4_t pointers, and then dereferenced for both the vector inputs and outputs. Also, the coeff scalar value must be converted from a scalar to a vector using the duplicate (vdupq) intrinsic.

The next step of the Gaussian elimination is to refine the matrix by setting each element in the upper triangle to zero using a similar approach:

- 1. set element (2,3) to zero
- 2. set element (1,2) to zero
- 3. set element (1,3) to zero
- 4. set element (0,1) to zero
- 5. set element (0,2) to zero
- 6. set element (0,3) to zero

| R0 | 1.0 | 0 | 0 | -0.6 | 0.3 | 0 | 0.1 |
| R1 | 0 | -3.0 | 0 | 0 | -0.9 | 0.7 | -0.8 | 0.5 |
| R2 | 0 | 0 | -10.3 | 0 | 1.1 | -4.3 | -2.5 | 2.9 |
| R3 | 0 | 0 | 0 | 0.9 | 1.2 | -1.0 | -1.2 | 0 |

This gives the result:

| R0 | 1.0 | 0 | 0 | -0.6 | 0.3 | 0 | 0.1 |
| R1 | 0 | -3.0 | 0 | 0 | -0.9 | 0.7 | -0.8 | 0.5 |
| R2 | 0 | 0 | -10.3 | 0 | 1.1 | -4.3 | -2.5 | 2.9 |
| R3 | 0 | 0 | 0 | 0.9 | 1.2 | -1.0 | 0 |

## B.4 Optimizing Floating-Point Code with NEON Intrics

This can be performed with the following loop:

```
for (i=2;i>=0;i--) {
    for (j=i+1;j<4;j++) {
        coeff = -a[i*4+j]/a[j*4];
        for (k=0;k<4;k++) {
            b[i*4+k]+=coeff * b[j*4+k];
            a[i*4+k]+=coeff * a[j*4+k];
        }
    }
}
```

Again the innermost loop can be replaced with NEON intrinsics:

```
*((float32x_t*)&b2[i*4]) =
    vmlaq_f32(*(float32x_t*)&b2[i*4]),
    *((float32x_t*)&b2[j*4]),
    dupq_n_f32(coeff));

*((float32x_t*)&a2[i*4]) =
    vmlaq_f32(*(float32x_t*)&a2[i*4]),
    *((float32x_t*)&a2[j*4]),
    dupq_n_f32(coeff));
```

As a final step, divide each row by its diagonal value to complete the transformation into the identity matrix:

- 1. set element (0,0) to one R0/A_{0,0}
- 2. set element (1,1) to one R1/A_{1,1}
- 3. set element (2,2) to one R2/A_{2,2}
- 4. set element (3,3) to one R3/A_{3,3}

This gives the following result:

| R0 | 1.0 | 0 | 0 | -0.6 | 0.3 | 0 | 0.1 |
| R1 | 0 | 1.0 | 0 | 0 | 0.3 | -0.2 | 0.3 | -0.2 |
| R2 | 0 | 0 | 1.0 | 0 | -0.1 | 0.4 | 0.2 | -0.3 |
| R3 | 0 | 0 | 0 | 1.0 | 1.3 | -1.1 | -1.3 | 1.3 |

This can be performed with the following code:

```
for (i=0;i<4;i++) for (j=0;j<4;j++) b[i*4+j] = a[i*4+j];
```

# B.5 SUMMARY OF NEON ININSICS

NEON intrinsics begin with the letter “v” and follow the following naming scheme:

```
v{prefix}{operation}{modifier}_{operand type}{operand width}
```

The prefix is optional, and depending on the intrinsic, is used to specify one of the available rounding and saturating modes.

The operation is a mnemonic usually named the same or similar to the intrinsic’s associated instruction.

The modifier is optional and is used for intrinsics that do not use standard 64-bit operands and results.

The operand type and width defines the datatype of each vector element.

### B.5.1 Prefix

The set of allowable prefix values depends on the operation. Example prefixes include:

- h (halving): shifts each output element to the right
- d (doubling): shifts each output element by one bit to the left
- r (rounding): rounds each output element (used with the hh modifier)
- rh (rounding halving): shifts each output element one bit to the right and rounds
- q (saturate): sets each output element to its maximum value on overflow or minimum value on underflow
- qd (saturating doubling): saturates and doubles
- qrd (saturating, rounding, and doubling): saturates, rounds, and doubles

### B.5.2 Operation

NEON operations can be grouped into several basic categories:

Arithmetic:

- add, sub, mul: add, subtract, multiply
- mla, mls: multiply-accumulate, multiply-subtract
- padd, padd: (or add and accumulate) each adjacent pair of elements from each input vector recipe, rsqte: reciprocal square root estimate (can be fp)
- abs, neg: absolute value and negate (can be fp)
- fma: fused multiply-accumulate
- fms: fused multiply-subtract

Bit manipulation:

- shl, shr: shift left, shift right (logical)?
- sra: and accumulate. Each element is shifted.
- sli, sri: shift left insert, shift right insert. Bits are not shifted element boundaries. Each element is shifted. [do these support the prefixes?]
- and (Bitwise AND), vbic (Bitwise Clear), veor (Bitwise Exclusive OR), vorn (Bitwise NOT OR), and vor (Bitwise OR): bitwise logical operations between two registers, and place the results in the destination
- mov, mvn: move negate
- cls, cl, cnt: count leading bits, count leading zeros, count set bits
- vbf, vbit, vsld: bitwise insert true, bitwise insert false, bitwise select; copies bits from the source operands into the destination.

Comparison:

- ceq, cge, cgt, cle, clt: compare equal, greater-than-or-equal, greater-than, less-than-or-equal
- tst: performs a bitwise AND between the corresponding elements in both vectors, if the AND is not zero, sets the output element to all ones, otherwise sets the output element all zeros
- abd, aba: absolute difference and accumulate
- max, min: sets each output element to the maximum or minimum of the two corresponding elements
- pmin, pmax: sets each output element to the maximum or minimum of each of the adjacent pairs of elements in both vectors

### B.5.3 Modifier

By default the intrinsic will use a 64-bit input and output width, implying that the vector size is 64/(operand width). The following modifiers are:

- q specifies 128 bit input and output width.
