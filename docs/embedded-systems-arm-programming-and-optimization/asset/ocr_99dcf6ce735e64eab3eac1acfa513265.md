How does it compare, in terms of number of instructions and runtime performance, as compared to the equivalent compiler-generated code for:

```
res = ((longlong)op1 * (longlong)op2) >> (rp1:rp2)
rp1:rp2)+(rpl:rp2 ? (((longlong)op1 * (
longlong)op2) >> (rp1-1)&1 :
((((longlong)op1*(longlong)op2)) >> (rp2-1)&1);
```

Make sure you the "-O3" and "-march" switches when compiling with gce.

+   Schedule the instructions of the inline assembly version of the multiply to minimize data density measures. Its performance relative to the version given in Section 3.6.6.

+   For the inline implementation, how much throughout is achieved if changing such that the radix point positions are fixed instead of variable as in the code? For this question, both the number of instructions and runtime behavior.

+   Calculating the pixel values for a Mandelbrot set requires a function for converting the iteration count to the R, G, and B color channels. Setting all three channels to the same value will generate a gray image, so the slope of each color function should be unique, and whichever is greatest will determine the hue of the image. As described in Section 3.8.1, the number of polynomials may exceed the value that exceeds the range of a color channel. To avoid a potential overflow, you must use saturating arithmetic when calculating each pixel. This way, if the value exceeds the maximum allowed value, set it to the maximum value.

+   Write a C macro that performs an 8-bit unsigned arithmetic The function will take two 8-bit operands and produce an 8-bit product to set 255 if the product exceeds 255. The macro must not include branch instructions and be scheduled for data dependencies.

+   This exercise will explore increasing the precision of the fixed-point types for the Mandelbrot generator to 64-bit.

+   Using a zoom rate of 1.5^n to what level can the frame be zoomed before exceeding this precision?

+   Define a macro in C for adding two (64,56) fixed-point values. The macro can perform the 128-bit add using four 32-bit adds and use the carry flag to implement carries from each 32-bit group to the next most significant 32-bit group.

+   Define a macro in C for multiplying two (64,56) fixed-point values. Build this macro on top of the 64-bit add macro from part b. As shown in Figure 3.6, a simple way to perform a 64-bit multiply is to perform a series of four 32-bit multiply/shift/accumulate operations each produce a 64-bit result.