# CHAPTER 12 Toolchain Primer

worrying about any aspects of the ABI. Compiler intrinsics are C functions that have a one-to-one or many-to-one relationship with specific instructions.

It's important to note that while some of these techniques are more powerful than others, it's generally possible to do the same things with any of them. As an analogy, consider compiler intrinsics to be like a water hammer, inline assembly to be like a claw hammer, and standalone assembly to be like a sledgehammer. Any of these hammers are capable of driving a nail, but using the right tool for the job tends to make job seem much easier.

# 12.5.1 STANDONE ASSEMBLY

As the names imply, standalone assembly involves writing routines and data structures that are separate from the C source files. Instead of being compiled by the C compiler, these source files are assembled, using the assembler, into an object file, which can be used like any other ELF object file. Compliance with the ABI ensures interoperability between C and assembly. Following GNU Makefile rules, assembly files typically end with .a or .s suffix. By default, files ending with .s are passed to the assembler, files ending with .s run through the C preprocessor to process a .s file, and then are assembled. Use of the C preprocessor for the sharing of C header files between C and assembly code. Another common suffix is .asm.

Many assemblers exist for Linux, but the most common are the GNU assembler, the Netwide assembler, nasm and YASM. The GNU assembler and YASM support the AT&T and Intel instruction syntaxes. Due to their ubiquitous nature, the author tends to use AT&T syntax and target the GNU assembler, which tends to be the most commonly available; the decision on which assembler to use or format usually depends on personal preference.

Symbols, which can mark data or text regions, are exported, for linking, via the .global pseudo-op. Local symbols, are symbols that are not named in the object file, being with the prefix "L". For situations where only a temporary symbol is desired, can be created by using a positive integer for the symbol name. The label can then be referred to the number, suffixed by "f" or "b". The "f" suffix indicates that the numbered label occurs after the current instruction, while the "b" suffix indicates that the numbered label occurs before the current instance.

In order to reserve space or initialize declared ones, a series of pseudo-ops exist. A memory region is reserved for a symbol in the .bss section, by using the .lcomm pseudo-op. This takes the format .comm SYMBOL, SIZE. For instance, to define an uninitialized buffer of 256 bytes named bar:

+   .bss
.lcomm bar, 256

The pseudo-op for reserving a memory region with a given value in one of the various data sections depends on the size of the region. For instance, the following are equivalent: