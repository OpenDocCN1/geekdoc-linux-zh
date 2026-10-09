+   * mips-unknown-linux
+   	* A big-endian MIPS Linux system from an unspecified manufacturer
+   * mipsel-linux
+   	* A little-endian MIPS Linux system from an unspecified manufacturer
+   * xscale-unknown-linux
+   	* An XScale (formerly StrongARM) Linux system from an unspecified manufacturer

Typically, cross toolchain component names are prefixed with the target triplet. Thus, for example, a cross-compiler for a Freescale 8541 PowerQuickIII Linux system will be called powerpc-8540-linux-gnu-gcc (gcc being the executable name for the GNU Compiler Collection), whereas the linker for a little-endian MIPS Linux system might be named mipsel-linux-ld (ld being the executable name of the GNU linker).

# ### Linux kernel headers

The first component required for building a toolchain is the set of the Linux kernel headers. Because the C library, which is part of the toolchain, is a wrapper that presents a more palatable API to the application programmer for the raw Linux kernel system calls, compiling the library requires a subset of the Linux kernel header files that describes the kernel API.

In theory, one should always build the toolchain using the Linux kernel headers from the exact same Linux kernel version that will be used on the target. In practice, however, this is rarely done. Because the ABI of the Linux kernel rarely changes (or more correctly, the parts of it described by the headers rarely change), using the headers from a different, but similar, kernel version is commonplace.

In Linux kernel releases prior to the 2.6 series, C library builds were based on a verbatim copy of the headers found in the Linux kernel directories include/asm-architecture and include/linux. Since the release of Linux 2.6, however, this is no longer supported, as the kernel headers contain much code that is unsuitable for inclusion in user space applications and can easily break the build of user programs, including the C library. Instead, builds use a sanitized version of the Linux kernel headers, suitable for use by user space code such as the C library. As of version 2.6.23 of the Linux kernel, the kernel source is equipped with an automated Make target for building such a “sanitized” version of the Linux kernel headers.

![](bbox=[0.15, 0.69, 0.85, 0.76])

From the kernel source directory, simply issue the following commands, replacing ppc with your architecture and headers/ with the path to the directory where you would like the sanitized headers installed: