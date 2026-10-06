# 248 APPENDIX B NEON Intrinsic Reference

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

+   1. set element (2,3) to zero
2. set element (1,2) to zero
3. set element (1,3) to zero
4. set element (0,1) to zero
5. set element (0,2) to zero
6. set element (0,3) to zero

| R0 | 1.0 | 0 | 0 | -0.6 | 0.3 | 0 | 0.1 |
| R1 | 0 | -3.0 | 0 | 0 | -0.9 | 0.7 | -0.8 | 0.5 |
| R2 | 0 | 0 | -10.3 | 0 | 1.1 | -4.3 | -2.5 | 2.9 |
| R3 | 0 | 0 | 0 | 0.9 | 1.2 | -1.0 | -1.2 | 0 |

This gives the following result:

| R0 | 1.0 | 0 | 0 | -0.6 | 0.3 | 0 | 0.1 |
| R1 | 0 | -3.0 | 0 | 0 | -0.9 | 0.7 | -0.8 | 0.5 |
| R2 | 0 | 0 | -10.3 | 0 | 1.1 | -4.3 | -2.5 | 2.9 |
| R3 | 0 | 0 | 0 | 0.9 | 1.2 | -1.0 | -1.2 | 0 |