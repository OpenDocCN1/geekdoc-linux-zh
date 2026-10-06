To overcome this problem, the chapter introduced fixed-point representation and arithmetic. Fixed-point arithmetic gives the programmer access to fractional number arithmetic using integer instructions and without using floating point. Fixed-point is available to applications that have a narrow, predefined numerical range.

The chapter described the accuracy, range, and precision of fixed-point values as compared to floating point. In order to explore the practical aspects of fixed point, the chapter showed macros for fixed-point addition and multiplication, written in both high-level language and inline assembly code.

Using these as examples, the chapter demonstrated how using inline assembly language allows the programmer to exploit architectural features useful in fixed-point arithmetic that are not available to the C-language code. An example of this taking advantage of the status register to capture the last shifted-out bit to implementing running.

After this, the chapter described how to convert the image transformation example from floating point to fixed point. This provided a 40% improvement to performance by reducing the number of instructions per pixel.

Another example of a computationally expensive graphical application, the chapter introduced Mandelbrot set generation. Although the Mandelbrot set has practical applications, it serves as a benchmark for a compute-arithmetically intensive program, and it has the advantage that speeding up the application produces a visible improvement in frames per second as the images as rendered in real time on an attached monitor.

The Mandelbrot set is also amenable to fixed-point arithmetic but requires careful selection of radius point location to maintain sufficient range and maximize precision. The behavior of the Mandelbrot set, in terms of the number of zoom levels, is determined by the amount of precision in the intermediate data types. This makes fixed-point arithmetic, being amenable to multi-precision integer arithmetic, even more attractive for this application.

The next chapter covers the VideoLinux system, which allows us to capture video frames from an attached camera for processing with computer vision algorithms. This chapter's optimization strategy is memory optimization through loop transformation.

# EXERCISES

+   1. Write a fixed-point implementation of the Mandelbrot generator.
   a. You will notice that the performance is inconsistent between different pixels and different frames. Why is this?