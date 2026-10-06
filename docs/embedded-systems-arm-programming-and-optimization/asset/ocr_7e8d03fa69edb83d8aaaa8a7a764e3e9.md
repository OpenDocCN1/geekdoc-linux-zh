# 5.7 Chapter Wrap-Up 229

Table 5.4 Kernel Performance for
N=128 MB, NWG=N/(4 × VS × WGS),
WGS = 256
| VS | Kernel FP Throughput (Gflops) |
| 1 | 4.8 |
| 2 | 9.4 |
| 4 | 15.6 |
| 8 | 15.5 |
| 16 | 14.7 |

For this test, the maximum performance is again above 15.6 Gflops, which is achieved for the maximum workgroup size of 256, matching the same parameters from the last row of the previous table.

# 5.6.4 Vector size

Regardless of the native width of the GPU's SIMD functional units, wider vectors in the kernel may provide the GPU architecture more opportunity for exploiting data-level parallelism.

Table 5.4 shows the performance results, as reported by the OpenCL profiler, with

+   - NWG=N/(4 × VS × WGS), which is the maximum possible, such that the kernel's for-loop executes only one iteration.
- WGS =256, the best-performing setting for this parameter was determined by the previous test.
- sweeping VS from 1 to 16.

The performance exhibits an increasing trend from VS=1 to VS=4 and a decreasing trend from VS=4 to VS=16. The maximum performance is at VS=4 with 15.6 Gflops, achieved with the same parameters as in the previous test.

# 5.7 CHAPTER WRAP-UP

This chapter introduces OpenCL, an openly framework for developing and dispatch general purpose programs to a slave-type coprocessor such as a GPU. OpenCL is adopted by several CPU, GPU, FPGA, DSP manufacturers, allowing programs written in OpenCL to be portable across a wide range of diverse embedded and high-performance processing technologies.