
## 12.2 ELF and the x86/x86_64 ABIs

through the Procedure Linkage Table (PLT) and Global Offset Table (GOT). The GOT contains the calculated addresses of the relocated symbols, while the PLT is used as a trampoline to that address for function calls.

Each entry in the PLT, except the first, corresponds to a specific function. Rather than directly calling the relocated symbol, the code jumps to the function's PLT entry. The first instruction in a function's PLT entry jumps to the address stored in the function's corresponding GOT. Initially, before the symbol has been bound, the GOT address points back to the next instruction in the PLT entry, which is, the next instruction pushes the symbol's relocation offset onto the stack. Then the next instruction jumps to the first PLT entry, which invokes the dynamic linker to resolve the relocation pushed onto the stack. Once the dynamic linker has calculated the relocated address, it updates the relevant entry in the GOT and jumps to the relocated function.

For future invocations of function, the code will still jump to the function's PLT entry and the address stored in the GOT, which will now point to the relocated address. In other words, the cost of binding the symbols occurs the first time the function is used. After that, the only additional cost is an indirect jump into the PLT.

Another problem with the dynamic linker patching code at runtime is that the code pages must be writable and dirty, that is, writable code pages are a security risk, since those pages are also marked as executable. Additionally, dirty pages can't be shared between processes and must be committed back to disk when swapped. To solve this, the relocations need to be shifted from the code pages to the data pages, since each process will require its own copy of those away. This is the key insight of Position Independent Code (PIC).

The PLT is not modified by relocations, so it is marked read-only and shared between processes. On the other hand, each process will require its own GOT, containing the specific relocations for process. In PIC, the PLT can only indirectly access the GOT.

The method for addressing the GOT in the PLT works differently between the 32- and 64-bit ELF formats. In both specifications, the address of the GOT is encoded relative to the instruction pointer. For 64-bit PIC, access to the GOT is encoded as an offset relative to the current instruction pointer. This straightforward approach is possible using RIP-relative addressing, which is only available in 64-bit mode. For 32-bit PIC, the ELF reserves the EBX register for holding the base address of the GOT.

Since the instruction pointer isn't directly accessible in 32-bit mode, a special trick must be employed. The CALL instruction pushes the address of the next instruction, onto the stack so that the RET instruction can resume execution after the function is called. Leveraging this, a simple function can read saved address from the stack, and then return. In the GNU library implementation, this type of function is typically called __i686_get_pc_thunk.bx, which loads the program counter, i.e., the instruction pointer, into the EBX register. Once the instruction pointer is loaded into EBX, the offset of the GOT is added.

While PIC improves security, by keeping the code pages read-only, and can improve memory usage, by preventing the code pages from being dirtied by relocations, it has a negative impact on performance. This impact is caused by all of the indirect calls and data references. The impact is much more significant on 32-bit, where the loss of the EBX register also leads to increased register pressure.

Because dynamic linking allows for an application to be built, or utilize different versions of the same shared library, it can be useful when benchmarking. By default, the dynamic linker searches for shared libraries in the paths configured via /etc/ld.so.conf, or in modern distros, /etc/ld.conf.d. The configured paths can be overridden by setting the LD_LIBRARY_PATH environmental variable. As such, a user performing benchmarking can modify this environmental variable to run the benchmark with multiple revisions of the same library, in order to measure the differences. For instance:

```
$ ls
project1 bench
$ export LD_LIBRARY_PATH=project0/
$ ldd bench
linux-vdso.so.1 -> (0x00007ffaffe0000)
libc.so.6 -> /lib64/liblibc.so.6 (0x0000000371a00000)
lib64/ld-linux-x86-64.so.2 (0x0000000319c00000)
project0.so => /home/jkt/jpa/project0/libproject.so
(0x000000392ae00000)
$ ./bench > result_version
$ export LD_LIBRARY_PATH=project1/
$ ldd bench
linux-vdso.so.1 -> (0x00007ffaffe0000)
libc.so.6 -> /lib64/liblibc.so.6 (0x0000000371a00000)
lib64/ld-linux-x86-64.so.2 (0x0000000319c00000)
project1.so => /home/jkt/jpa/project1/libproject.so
(0x000000392ae00000)
$ ./bench > result_version1
```

The LD_PRELOAD environment variable can be defined as a colon-separated list of libraries the dynamic linker should load first. To see how this can be used to intercept and instrument functions in a shared library, refer to the buGL and Apitrace tools described in Sections 10.2 and 10.3 of Chapter 10.

## 2.2.2 ABI

The Application Binary Interface (ABI) standardizes the architectural interactions between various system components. The ABI defines items, such as the calling conventions, structure layout and padding, type alignments, and other aspects that must remain consistent between various software components to ensure compatibility and interoperability. This section focuses on dealing with the C ABI.

### Natural alignment

Alignment refers to the power of two that an address is a multiple of. In binary, this has the interesting property of being the first bit after zero or more consecutive zeros from the least significant bit. For instance, the binary numbers 00001100, 11111000, 10110000, and 00110000 all have an alignment of 8. Using this knowledge, whether a specified address, x, meets the alignment criteria, a, given that a is a power of two, can be determined by:

```
#include <intypes.h>
#include <assert.h>

static inline is_aligned(uintptr_t x, int a)
{
    assert(a && (x & (a - 1)));
    return (x & (a - 1));
}
```

Unlike architectures, Intel® Architecture does not enforce strict data alignment, except for special cases. The C standard specifies that, by default, types should be created with regards to their natural alignment, i.e., their size. So for instance, an integer on both x86 and x86_64 has a natural alignment of 4 bytes, whereas a long integer would have a natural alignment of 4 bytes on x86, and 8 bytes on x86_64.

### Calling conventions

Calling conventions describe the transfer of data between a function callee and caller. Additionally, the conventions describe which function, callee or caller, is responsible for cleaning up the stack after the function call. Without standardized calling conventions, it would be very difficult to combine multiple object files or libraries, as functions might lack the ability to properly invoke others.

The calling convention for x86 is known as cdecl. Functions written to this specification expect their arguments on the stack, pushed right to left. Since the CALL instruction pushes the return address, that is, the address of the next instruction after the function call returns, off the stack, the elements can be accessed at offset 4 of the stack pointer.

The calling convention for x86_64 is similar, but is designed to take advantage of the extra registers available when the processor is in 64-bit mode. Rather than passing all arguments on the stack, arguments are passed in registers, with the stack used to handle any extras. The first integer argument is passed in the RDI register, the second in the RSI register, the third in the RDX register, the fourth in the RCX register, the fifth in the R8 and the sixth in R9. Floating point arguments are passed in the XMM registers, starting at XMM0 and ending at XMM7.

Typically, immediately on being invoked, a function sets up a frame pointer, that is a special reserved register that contains the base address for the current stack frame. Saving the base of the stack for each function is useful for unwinding the stack for debugging purposes, such as recording the stack trace. On both x86 and x86_64,
