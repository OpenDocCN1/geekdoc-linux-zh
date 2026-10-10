We also look a little at the differences between the PA-RISC 2.0 and PA-RISC 1.1 architectures. PA-RISC 2.0 expanded the PA-RISC architecture to a 64-bit model and added many enhancements for improving system performance. Systems built on the PA-RISC 1.1 architecture run 32-bit kernels. A PA-RISC 2.0 system can run either a 32-bit or a 64-bit kernel. A 64-bit kernel in turn can run either 32-bit or 64-bit user applications.

# ## RISC Architecture

PA-RISC, as its name implies, is a RISC, or Reduced Instruction Set Computer, architecture. But there is more to RISC than just a smaller instruction set. There are several characteristics that are common to all RISC architectures, including PA-RISC, that make these systems fast and easy to implement. Among these are:

+   - Fixed instruction size—All instructions are 32 bits wide.
+   - Small number of addressing modes—PA-RISC has only three methods of specifying a memory address.
+   - Simplified memory access—The only instructions that access memory are explicit loads and stores. Computational operations are done between registers.

These characteristics make for a fast, simple hardware implementation. Performance gains can then be accomplished through pipelining and through optimization of code by compilers.

The PA-RISC architecture also has many features not normally associated with RISC. The instruction set, while smaller than older CISC architectures, has many instructions designed specifically to streamline commonly executed sequences of instructions. In addition, the hardware is designed to speed up typically expensive instructions such as bit operations.

# ## Hardware Modules

Figure 1-1 shows a typical PA-RISC processor. The architecture provides for a translation lookaside buffer (TLB), which is used to assist in translating virtual addresses to physical addresses. The inclusion of a cache is optional, but most PA-RISC processors do have at least some amount of cache. The architecture also provides for assist processors such as a floating-point processor to assist in complex operations.