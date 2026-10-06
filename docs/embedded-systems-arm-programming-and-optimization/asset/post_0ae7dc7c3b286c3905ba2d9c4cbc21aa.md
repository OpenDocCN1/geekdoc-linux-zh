
# Table C.2 OpenCL Types

| Kernel Type | Description | Host Type (If Applicable) |
| --- | --- | --- |
| char | 8-bit signed | cl_charn |
| uchar | 8-bit unsigned | cl_uchar |
| short | 16-bit signed | cl_short |
| ushort | 16-bit unsigned | cl_ushort |
| int | 32-bit signed | cl_int |
| uint | 32-bit unsigned | cl_uint |
| long | 64-bit signed | cl_long |
| ulong | 64-bit unsigned | cl_ulong |
| float | 32-bit float | cl_float |
| double | 64-bit float | cl_double |
| image2d_t | 2D image handle | |
| image3d_t | 3D image handle | |
| image2d_array_t | 2D image array | |
| image1d_t | 1D image handle | |
| image1d_buffer | 1D image buffer | |
| image1d_array_t | 1D image array | |
| sampler_t | Sampler handle | |
| event_t | Event handle | |
| bool | Boolean vector | |
| half | 16-bit float, vector | |
| quad, quadn | 128-bit float, vector | |

# APPENDIX OpenCL Reference

## Table C.2 OpenCL Types —cont'd

| Kernel Type | Description | Host Type (If Applicable) |
|---|---|---|
| complex_half,complex_half | 16-bit complex, vector | | |
| imaginary_half,imaginary_half | 16-bit imaginary, vector | | |
| complex_float,complex_float | 32-bit complex, vector | | |
| imaginary_float,imaginary_float | 32-bit imaginary, vector | | |
| complex_double,complex_double | 64-bit complex, vector | | |
| imaginary_double,imaginary_double | 64-bit imaginary, vector | | |
| complex_quad,complex_quad | 128-bit complex, vector | | |
| imaginary_quad,imaginary_quad | 128-bit imaginary, vector | | |
| floatnxm | nxm matrix of 32-bit floats | | |
| doublenxm | nxm matrix of 64-bit floats | | |

In. this case, the programmer can provide workgroup and vector size information to the kernel in the form of attributes, as shown below.

### Kernel Attributes

```
__attribute__((vec_type_hint(type)))
__attribute__((work_group_size_hint(X, Y, Z)))
__attribute__((reqd_work_group_size(X, Y, Z)))
```

OpenCL also allows for declared variables to be given attributes for alignment, packing, and endianness.

### Type Attributes

```
__attribute__((aligned(n)))
__attribute__((aligned))
```

```
__attribute__((packed))
__attribute__((endian(host)))
__attribute__((endian(device)))
__attribute__((endian))
```

# C.9 CONSTANTS

OpenCL defines a list of single-precision floating-point constants as defined in Table C.3. Each constant that ends with "_F" has a corresponding double precision without the "_F" suffix and half precision by replacing the "_H" suffix, when supported by the OpenCL implementation.

# C.10 BUILT-IN FUNCTIONS

OpenCL provides a set of built-in functions available for use in kernel code. Some of these functions are standard mathematical primitives and many of these accept vector operands. Others are utility functions for work-item identification and vector loads stores.

### C.10.1 Integer functions

Table C.4 lists the integer functions. These functions accept vector operands.

### C.10.2 Floating-point functions

Table C.5 lists the floating-point functions. Most of these functions accept vector operands.

### C.10.3 Vector functions

OpenCL kernels should always use vector load and store functions to exchange data between vector variables and arrays (Table C.6).

### C.10.4 Work-item functions

OpenCL kernels can be dispatched as a 1-, 2-, and 3-dimensional array of work-items. The array of work-items can optionally be subdivided into 1-, 2-, or 3-dimensional groups (when get_local_id() is called with the local_work_size argument). workload distribution is governed by the ability for each work-item to self-identify within this coordinate system, while its global ID is calculated relative to its location within its workgroup (Table C.7). Work-items within workgroup can be synchronized with a barrier operation and their memory operations ordered (Table C.8).

## Table C.3 OpenCL Constants

| Constant | Description |
|---|---|
| MAXFLOAT | Value of maximum finite single-point number |
| HUGE_VAL | Positive float expression, evaluates to +infinity |
| HUGE_VAL | Positive double expression, evaluates to +infinity |
| INFINITY | Constant float expression, unsigned |
| NAN | Constant float expression, NaN |
| M_E_F | Value of e |
| M_LOG2E_F | Value of log$_2$ |
| M_LOG10E_F | Value of log$_{10}$ |
| M_LN2_F | Value of log$_e$ |
| M_LN10_F | Value of log$_{10}$ |
| M_PI_F | Value of $\pi$ |
| M_PI_2_F | Value of $\pi$/2 |
| M_PI_4_F | Value of $\pi$/4 |
| M_1_PI_F | Value of $1/\pi$ |
| M_2_PI_F | Value of $2/\pi$ |
| M_2_SQRTPI_F | Value of $2/\sqrt{\pi}$ |
| M_SQRT2_F | Value of $\sqrt{2}$ |
| M_1_SQRT2_F | Value of $1/\sqrt{2}$ |

## Table C.4 Built-in Functions

| Function | Description |
|---|---|
| abs(x) | x (unsigned) |
| abs_diff(x) | x-y without overflow (unsigned) |
| add_sat(x,y) | x+y and saturate the result |
| hadd(x,y) | (x+y)>>1 without overflow |
| rhadd(x,y) | (x+y+1)>>1 |
| clamp(x,minval,maxval) | min(max(x,minval),maxval) min and max can be vectors or scalars |
| clz(x) | Number of leading 0-bits in x |
| mad_hi(a,b,c) | mul_hi(a,b)+c |
| mad_sat(a,b,c) | a*b+c and saturates the result |
| max(x,y) | y if x<y else x can be a vector or scalar |
| min(x,y) | y if y<x else x can be a vector or scalar |
| mul_hi(x,y) | high half of x*y |
| rotate(v,i) | rotate v by bits |
| sub_sat(x,y) | x-y and saturate the result |
| popcount(x) | Number of one-zero bits in x |
| short[n] upsample(char[n] hi, char[n] lo) | result[j] = ((short)hi[i]<<8) | lo[j]) |
| ushort[n] upsample(uchar[n] hi, uchar[n] lo) | result[j] = ((ushort)hi[i]<<8) | lo[j]) |
| int[n] upsample(short[n] hi, ushort[n] lo) | result[j] = ((int)hi[i]<<16) | lo[j]) |
| uint[n] upsample(ushort[n] hi, int[n] lo) | result[j] = ((uint)hi[i]<<16) | lo[j]) |
| long[n] upsample(int[n] hi, uint[n] lo) | result[j] = ((long)hi[i]<<32) | lo[j]) |
| ulong[n] upsample(uint[n] hi, long[n] lo) | result[j] = ((ulong)hi[i]<<32) | lo[j]) |
| mad24(x,y,z) | Multiply 24-bit integer values x, y, add 32-bit int. result to 32-bit int. z |
| mul24(x,y) | Multiply 24-bit integer values x and y |

## Table C.5 Built-in Floating-Point Functions

| Trigonometry functions | |
|---|---|
| sin(x), cos(x), tan(x), | Basic trigonometry functions |
| asin(x), acos(x), atan(x), | Inverse trigonometry functions |
| sinh(x), cosh(x), tanh(x), | Hyperbolic trigonometry functions |
| asinh(x), acosh(x), atanh(x), | Inverse hyperbolic functions |
| sinpi(x), cospi(x), tanpi(x), | Basic trigonometry functions, result by pi |
| asinpi(x), acospi(x), atanpi(x), | Inverse trigonometry functions, result by pi |
| atan2(x,y), | Tangent of x/y |
| atan2pi(x,y) | atan2(x,y)/pi |
| Logarithms, exponentiation, and power functions | |
| log(x), log2(x), log10(x), | Logarithm base e, 2, and 10 |
| log1p(x), logb(x), | In (1.0+x) |
| exp(x), exp2(x), exp10(x), | Exponentiation, base e, 2, and 10 |
| expm1(x), | e⁻1.0 |
| pow(x,y), pown(x,y), powr(x,y), | Computes xʸ |
| rootn(x,y), | x¹/ |
| ilogb(x), | Extract exponent |
| ldexp(x,n), | x*² |
| frexp(x, *exp), | Extract mantissa and exponent |
| modf(x, *iptr), | Decompose floating-point number |

## Table C.5 Built-in Floating-Point Functions —cont'd

| Geometric functions | |
|---|---|
| cbrt(x) | Cube root of x |
| hypot(x,y) | Square root of $x^2+y^2$ |
| cross(p0,pl) | Cross product (vector size 3 or 4) |
| distance(p0,pl) | Vector distance |
| dot(p0,pl) | Dot product |
| length(p) | Normal vector length 1 |
| normalize(p) | Normalize |
| fast_distance(p0,pl) | Vector distance |
| fast_length(p) | Vector length |
| fast_normalize(p) | Normal vector length 1 |
| Rounding operations | |
| ceil(x), floor(x) | Ceiling, floor |
| rint(x) | Round to nearest even integer |
| copysign(x,y) | x changed to sign of y |
| erf(x), erfc(x) | Error function, complementary error function |
| fabs(x), | Absolute value |
| fdim(x) | Positive difference between x and y |
| Multiply accumulate | |
| fma(a,b,c), mad(a,b,c) | Multiply accumulate |
| Max/min functions | |
| fmax(x,y), fmin(x,y) | Maximum, minimum |
| maxmad(x,y), minmad(x,y) | Maximum, minimum magnitude of x and y |
