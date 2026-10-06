# 12.4 Coding style 227

The downside to this method is that it is an extension to the ELF standard and therefore will not be portable to other toolchains or systems. Also, support for older Linux distributions can be problematic, since support has only been available for five years and has not made it into some enterprise distributions.

# Dynamic linking

For 32-bit x86, the dynamic linker, `ld.so`, supports the connect of hardware capabilities. Each predefined capability, listed in the manual page, corresponds to a search directory, which will be utilized if the underlying processor architecture supports that feature. For example, with SSE2 feature the linker will include the contents of `/usr/lib/sse2/` in the library search path.

As a result, it is possible to leverage this functionality building multiple versions of a shared library, each with different processor functionality enabled, and installing them into the appropriate directories. The benefit of this approach is that no runtime checks need to occur, since the library compiled with certain processor features will only be used on a processor that supports those features. The drawbacks to this approach are that there will be multiple versions of the library, corresponding to each possible combination of supported features, and that this feature is only available on 32-bit systems.

The author includes this technique for completeness, since in general, the other approaches are much better. Providing multiple versions of a shared library means a significant extra testing burden, and the runtime checking for processor features can easily be performed outside of any hotspot, during code initialization, making it irrelevant.

# 12.4 CODING STYLE

If the tools discussed in Part 2 have led to a hotspot, the problems are mostly missed optimization opportunities or simply bad code generation, the next step is not to jump directly into rewriting the code in assembly. Instead, it is much more preferable to coax the compiler into generating better code. This typically occurs by providing the compiler with as much information as possible about the context of the code, to enable better optimizations.

This section provides some useful techniques for writing code in such a way that actively helps the compiler to improve performance.

# 12.4.1 POINTER ALIASING

Two pointers are said to alias when they both point to the same region of data, what the C specification would refer to as an object. For the compiler, determining pointer aliasing is important for both correctness and performance.

Before diving into the specifics, consider the simple example presented in Listing 12.8, where every element of an array of doubles is set based on the value of a double referenced via the second pointer.