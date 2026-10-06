# 1.1 Performance-Oriented Programming

However, next-generation embedded applications such as computer vision will require rapidly evolving algorithms, and most of these compute bound. Examples of these include programs that stitch individual images to a panoramic image, facial detection and recognition, augmented-reality, and object recognition.

This textbook provides a general overview of some of the methods of how program design can influence processor performance—methods in which a programmer can make changes to code without changing program semantics but improving code performance.

These techniques generally require the programmer write his or her code in a way as expose specific features in the underlying microarchitecture. In other words, the programmer must write code at a low level in a way such that the program is aware of the underlying processor technology. This is often referred to as performance tuning or code optimization.

These ideas are not new; many of these techniques are common in the area of high-performance computing. However, this book will present these in the context of embedded processors, and ARM processors in particular. This will also provide insight into computer architecture, application design, and embedded systems, as well as gain practical knowledge in the area of embedded software design for modern embedded systems.

In describing these methodologies, the textbook will use several example applications, including image transformations, fractal generation, image convolution, and several computer vision tasks. These examples will target the ARMv6 and ARMv7-A architectures used on three cores:

+   - ARM11 used in the generation 1 Raspberry Pi,
- Cortex-A9 used in the Xilinx Zynq (the device used in the Avnet Zedboard, Adaptera Parallel, and National Instruments myRIO),
- Cortex-A15 used in the NVIDIA Tegra K1.

This book also introduces methodologies for programming mobile general-purpose GPUs using the OpenCL programming model.

This textbook will take advantage of the system families offered by the Linux OS, including Linux's GCC compiler toolchain and debug tools, performance monitoring support, OpenMP multicore runtime environment, video buffer frame, and video capture capabilities.

This textbook is designed to accompany with any of the many low-cost Linux/ARM embedded development boards currently on the market. Examples of these include the following: