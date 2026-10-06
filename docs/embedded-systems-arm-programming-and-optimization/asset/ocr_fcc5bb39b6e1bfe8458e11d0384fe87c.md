# 1.12 PERFORMANCE BOUNDS

A program loop or loop nest that comprises a substantial portion of the execution time is referred to as a kernel. The runtime behavior of relatively simple kernels can be characterized by arithmetic intensity, or number of primitive CPU operations performed per unit of data. When the kernel's arithmetic intensity is known, it can be used to compute a performance upper bound as a function of a processor's peak memory bandwidth.

The exact arithmetic intensity value at which a kernel goes from being memory bound depends on the processor, but in practice very few kernels are compute bound. Even kernels seem to have very high arithmetic intensity, such as matrix-matrix multiply that perform O(n³) flops for every O(n²) input and output value, are still potentially bounded due to load-store stalls or data dependency stalls. This is seen in cases where SGEMM achieves 50-75% of the peak theoretical performance for a particular processor.

Arithmetic intensity is measured in floating-point operations per byte (flops/byte). Thus the performance upper bound for a kernel can be computed as P=A×B, where A = arithmetic intensity in flops/byte, B = memory bandwidth in bytes/s, and P = performance in flops/s (flops).

# 1.13 BASIC ARM INSTRUCTION SET

This section provides a concise summary of a basic subset of the ARM instruction set. The information provided here is only enough to get you started writing ARM assembly programs, and does not include any specialized instructions, such as system instructions and those related to

![](bbox=[0.336, 0.946, 0.563, 0.966])