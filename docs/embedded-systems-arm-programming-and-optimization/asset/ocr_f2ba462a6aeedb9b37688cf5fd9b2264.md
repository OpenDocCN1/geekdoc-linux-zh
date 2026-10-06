# 134 CHAPTER 3 Arithmetic Optimization and the Linux Framebuffer

```
green = ((g[0]) * (weights[0]) +
(g[1]) * (weights[1]) +
(g[2]) * (weights[2]) +
(g[3]) * (weights[3])) >> FRACBITS*2;
```

```
blue = ((b[0]) * (weights[0]) +
(b[1]) * (weights[1]) +
(b[2]) * (weights[2]) +
(b[3]) * (weights[3]) >> FRACBITS*2;
```

# 3.7 FIXED-POINT PERFORMANCE

As compared to floating point, using fixed point reduces the latency after each arithmetic instruction at the cost of additional instructions required for rounding and radix point management, although if the overhead contains sufficient instruction level parallelism of these additional instructions on throughput may not be substantial.

On the other hand, for graphics applications like the image transformation that require frequent conversions between floating point and integer, using fixed point may result in a reduction of executed instructions.

In fact, when compared the floating-point implementation on the Raspberry Pi, the fixed-point implementation achieves approximately the same CPI and cache miss rate, but decreases the number of instructions per pixel from 225 to 160. This resulted in a speedup of throughput of approximately 40%.

# 3.8 REAL-TIME FRACTAL GENERATION

A fractal is a mathematical set that exhibits infinitely repeating self-similar patterns at increasingly finer scale.

Perhaps the well-known fractal is the Mandelb set shown in Figure 3.5. The Mandelb set is a set of complex numbers, all of which have a Euclidean norm that is less than 2. In other words, when the complex numbers in the Mandelb set are plotted on a 2D space where the real part is plotted on the X-axis and the imaginary part is plotted on the Y-axis, every point would be contained within a radius 2 circle of the origin.