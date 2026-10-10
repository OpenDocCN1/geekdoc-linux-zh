used code refers to the external subroutine or global variable. The resulting executable image uses more disk storage, takes longer to load into memory, uses valuable memory, and may be out-of-date.

Dynamic linking (also called dynamic loading) avoids three of these four problems and helps deal with the fourth problem.

The trick to dynamic linking is to substitute a library full of *stubs* for the full library. The linker will *bind* these stubs to the user program so that a call to a function, say *printf*, goes to the stub instead of the function. The code in the stub loads the full library code and, after patching a jump-table to avoid further loading, transfers control to the full library code.

The stub code is smaller than the full library code, so the executable file is smaller and it will take less time to load into memory.

Because the full library is referenced only when the program finally executes, changes to the full library effect all programs, not just programs built after the library changed.

Finally, because the library calls are made indirectly through the stubs, the library code can reside in memory accessible to many processes. (It is because the library code may already be present in memory that the terms “linking” and “loading” can apply to the same program at different occasions.)

Library code can be shared without the dynamic linking described above. In this case, the user’s program is linked to well known addresses. If the library code isn’t already in memory when the user program is loaded, the library is loaded as well.

# COFF

COFF was a short-lived attempt to generalize object file formats. It has been supplanted by ELF on Linux, but it is still used by SCO.

# ELF

ELF, which stands for Executable and Linking Format, is a portable object file format which is supported by many different system kernels running on the Intel 386, 486, Pentium and compatible architectures. This format differs from the a.out format in that it supports an arbitrary