macro written here in GCC inline assembly does the job of pretouching the necessary bootloader instructions onto I-cache. You need a working knowledge of PowerPC assembly to understand this code snippet:

```
Code View:
/* instr_length is the number of instructions to touch
into I-cache. _load_i$copy and _end_i$copy are
program labels */
#define load_into_icache_copy(instr_length) \
asm volatile("lis     %r3, 0x1@h\n \
            ori     %r3, %r3, 0x1@l\n \
            mticcr  %r3\n \
            isync\n \
            \n \
            lis     %r6, _end_i$copy@h\n \
            ori     %r6, %r6, _end_i$copy@l\n \
            icbt    %r0, %r6\n \
            lis     %r4, 0@h\n \
            ori     %r4, %r4, 0@l\n \
            mctr    %r4\n \
_load_i$copy: \
            addis   %r6, %r6, 32@ha\n \
            addi    %r6, %r6, 32@l\n \
            icbt    %r0, %r6\n \
            bdnz    _load_i$copy\n \
_end_i$copy: \
            nop\n" \
: : "1"(instr_length) \
: "%r6", "%r4", "%r0", "%r8", "x9");
```

# Debugging

To debug the real mode kernel, you cannot use debuggers such as the Kernel Debugger (kdb) or the Kernel GNU Debugger (kgdb), which we discussed in Chapter 21, "Debugging Device Drivers." A quick way to debug kernel assembly snippets is by using the DOS debug tool after converting your code to Intel-style syntax. But debug was created in the 16-bit era, so you can't, for instance, step through code that initializes the RAX register. You can find 32-bit debug-type freeware tools available for download on the Internet. JTAG debuggers, also discussed in Chapter 21, are a kind of panacea because a single tool can be used to debug the BIOS, bootloader, Linux real mode code, and kernel-BIOS interactions.