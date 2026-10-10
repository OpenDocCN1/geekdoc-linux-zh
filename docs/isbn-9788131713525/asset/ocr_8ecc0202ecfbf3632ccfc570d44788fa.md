# 3.1 Stand-alone Processors

Here we present a sample from each of the major manufactures of stand-alone processors. These processors are well supported under Linux and have been used in many embedded Linux designs.

# 3.1.1 IBM 970FX

The IBM 970FX processor core is a high-performance 64-bit capable stand-alone processor. The 970FX is a *superscalar* architecture. This means the core is capable of fetching, issuing, and obtaining results from more than one instruction at a time. This is done through a pipelining architecture, which provides the effect of multiple streams of instruction simultaneously. The IBM 970FX contains up to 25 stages of pipelining, depending on the instruction stream and operations contained therein.

Some of the key features of the 970FX are as follows:

+   - A 64-bit implementation of the popular PowerPC architecture
+   - Deeply pipelined design, for very-high-performance computing applications
+   - Static and dynamic power-management features
+   - Multiple sleep modes, to minimize power requirements and maximize battery life
+   - Dynamically adjustable clock rates, supporting lower-power modes
+   - Optimized for high-performance, low-latency storage management

The IBM 970FX has been incorporated into a number of high-end server blades and computing platforms, including IBM’s own Blade Server platform.

# 3.1.2 Intel Pentium M

Certainly one of the most popular architectures, x86 in both 32- and 64-bit flavors (more properly called IA32 and IA64, respectively) has been employed for embedded devices in a variety of applications. In the most common form, these platforms are based on a variety of commercial off-the-shelf (COTS) hardware implementations. Numerous manufacturers supply x86 single-board computers and complete platforms in a variety of form factors. See Section 3.2 “Integrated