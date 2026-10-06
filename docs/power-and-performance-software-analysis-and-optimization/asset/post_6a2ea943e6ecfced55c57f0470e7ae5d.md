
## Intel® Pentium Processors

In the previous chapter, the early history of the x86 architecture was introduced. While the early 16-bit processors introduced many of the fundamental principles of the x86 architecture, aside from extending the architecture to 32 bits, they added isolation and memory protection features that are an integral part of modern operating systems. The requirements placed on technology increase at a large order, and therefore technology must continually support these demands. The consumer market was surging with performance-intensive applications, such as 3D games and multimedia, while at the same time the availability of the Internet created a demand for infrastructure capable of supporting these new workloads. This changing landscape significantly shifted the processor design of the time. The successor to the 80486, the Intel® Pentium, focused on improving performance. For example, the floating point coprocessor was integrated directly into the processor, as opposed to the first Pentium.

### 2.1 Intel® Pentium

#### 2.1.1 Superscalar

Prior to the 80486, the predecessor to the Pentium, each instruction was executed serially. In other words, each instruction began and finished execution before the execution of the next instruction could begin. This resulted in inefficient utilization of the processor’s resources, as instruction execution did not require all of those resources simultaneously.

The 80486 introduced the concept of pipelining. Instruction pipelining the execution process into multiple independent steps occurring in parallel. Instructions traverse these paths one stage at a time. Once an instruction progresses to the next stage, the next instruction can take its place in the pipeline, and so on. As a result, the pipeline can simultaneously execute multiple instructions. This leads to better utilization of the processor’s resources, as each instruction only consumes a subset of the total resources. In other words, pipelining provides a finer level of granularity for the allocation of resources.

The execution pipeline of the 80486 is partitioned into five stages, making the pipeline effective utilization on each stage making forward progress to the next stage, with the oldest instruction and a new instruction entering the pipeline. A situation where forward progress cannot be made is referred to as a hazard. There are three types of pipeline hazards:

- Structural Hazards: Two instructions require the same hardware resource.
- Data Hazard: Two instructions share a data dependency. For example, one instruction might depend on the result of another instruction.
- Control Hazard: Instructions within pipeline were speculatively executed but the branch was predicted incorrectly.

When a hazard occurs, the pipeline stalls in order to allow the hazard to pass. This stall is referred to as a bubble in the pipeline, since there is an empty gap introduced.

The Pentium processor increased the ILP of the 80486’s instruction pipeline even further. Whereas the 80486 had one pipeline capable of executing five instructions simultaneously, the Pentium architecture had two pipelines each of executing five instructions simultaneously. This is referred to as multiple issue, because multiple instructions are ideally entering and exiting the pipeline at each stage. In order to accommodate this, the Pentium processor adds duplicate execution units to support the second pipeline.

The number of instructions the processor can issue each cycle is referred to as the processor’s width, so the Pentium processor is described as 2-wide. It is important to understand that the two pipelines are not identical. As a result, there are restrictions on which instructions can be issued together. If any of these restrictions are violated, then only one instruction can be issued. This decision, whether to issue one or two instructions, is performed automatically in hardware during execution.

Therefore, the Pentium processor is classified as a dynamic multiple issue processor, that is, superscalar. This is opposed to a static multiple issue processor, where the programmer and compiler are responsible for scheduling instructions to obey the restrictions.

### 2.2 Intel® PENTIUM® PRO

After the Pentium, the Pentium Pro, shown in Figure 2.2, was introduced in 1995. The Pentium Pro was the first processor to utilize the new P6 architecture, that is, the i686. The P6 architecture introduced a significant number of improvements to the first Pentium, and therefore remained a staple of the Pentium lineup, until the introduction of the NewBurst architecture with the Pentium 4.

Whereas the 80486 and first Pentium only contained one memory cache on-die, the Pentium Pro added a second, larger but slower, cache which is known as the second level cache or L2 cache. Additionally, the introduction of Physical Address Extensions (PAE) increased the amount of usable physical memory from 4-GB to 64-GB. The Pentium Pro also brought improvements to the execution pipeline and $\mu ops$, and by extending the processor's width to out-of-order execution and 3-wide superscalar.

#### 2.2.1 PAE

The PAE increase the number of the processor's physical address pins, expanding the size of the physical address space. It is important to understand that this only... (Israel, 1996).

## References 29

- ISO Joint Technical Committee JTC1, Subcommittee 22, Working Group 14, 2007, 10. ISO/IEC 9899:TC3 Data C language Specification.
- Israel, J., 2009, 2Ic-photo-Intel-D8087-2-(8086-FPU). Used with permission. http://www.happytrees.org/main-images/ic-photo-v2/ic-photo-Intel--D8087-2-(8086-FPU).png PNG converted to grayscale and eps.
- Kahan, W., 1990, 11. On the advantages of the 8087's stack, Unpublished Course Notes.
- Kahan, W., Palmer, J., 1997. On a proposed floating-point standard. SIGNUM Newsl. 105 (4-2), 13–21. doi:10.1145/105750.105752. http://doi.acm.org/10.1145/105750.105752.
- Lanzet, K., 2008, 6, KL Intel386DX – CPU collection Konstantin Lanzet. Used with permission. http://www.comimages.org/wiki/File:KL_Intel_i386DX.jpg#mediaviewer/File:KL_i386DX.jpg, JPEG converted to grayscale and eps.
- Lanzet, K., 2009, 4 KL Intel D0806 – CPU collection Konstantin Lanzet. Used with permission. http://upload.wikipedia.org/wikipedia/en/KL/Intel_D0806.jpg, JPEG converted to grayscale and eps.
- Molnar, I., 2012, 12-uke_i386-as support, Git Pull Request, SHA1 in tree: 743aa5c6185347682d4e6b7d1d0a0f2a8e22.
- Palmer, J.F., 1980. The Intel 8087 numeric data processor. Proceedings of the May 19-22, 1980, National Computer Conference. AFIPS '80, Anaheim, California. ACM, New York, NY, pp. 887–893. http://doi.acm.org/10.1145/1500518.1500674.
- Patterson, D.A., Hennessy, J.L., 2007. Computer Organization and Design: The Hardware/Interface, third ed. Morgan Kaufmann, Burlington, MA.
- Torvalds, L., 1991, 08. What would you like to see most in minix? https://groups.google.com/forum/#topic.com_of_minix/
