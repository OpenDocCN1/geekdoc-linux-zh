# 132 CHAPTER 3 Arithmetic Optimization and the Linux Framebuffer

Using a (32,8) format provides 24 bits of range and 8 bit of accuracy, fulfilling both requires for the image transformation.

# 3.6.9 Converting from floating-point to fixed-point arithmetic

This section describes a method for converting the image transformation code described earlier in the chapter to fixed point. The code uses high-level language to perform the fixed-point arithmetic.

Begin by changing the type of the arrays src_pixel, frac, and weights to int. Then define two parameters that can be used to adjust the position of the radix point (m) and its corresponding numerical significance (2^m).

```
#define FRACBITS 8
```

```
#define FRAC_SIG 256
```

The rotation transformation requires the use of sine and cosine functions, and there are no fixed-point versions of these in the POSIX standard math library. Although it is possible to implement them or use a third party library, doing so will have negligible impact on performance since the program calls functions once per frame computing the transformation matrices. As such, the program can calculate these values using floating point and convert the floating-point values to fixed point.

To do this, define a fixed-point version of the transformation matrix by declaring new variables c_row_fp and c_col_fp as 2-element arrays of type int.

After the call to calc_coeffs(), add the following code to convert the floating-point transformation matrix to fixed point. To convert, multiply the floating-point values where f=the number of bits to the right of the radix point, converting the result to an integer as shown below:

```
c_row_fp[0] = (int)(c_row[0] * (float)FRAC_SIG);
c_row_fp[1] = (int)(c_row[1] * (float)FRAC_SIG);
c_col_fp[0] = (int)(c_col[0] * (float)FRAC_SIG);
c_col_fp[1] = (int)(c_col[1] * (float)FRAC_SIG);
```

The inner loop begins by multiplying the destination pixel location at row j(or x=j, y=i) by the transformation matrix. No time int-float casting is necessary.

The following lines map each pixel location in the transformed image to a (fractional) pixel location in the source image. Each line adds two products