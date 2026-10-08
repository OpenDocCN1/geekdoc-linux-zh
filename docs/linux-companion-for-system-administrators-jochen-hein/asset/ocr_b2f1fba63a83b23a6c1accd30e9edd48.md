# 12.3 The iBCS emulator

For UNIX systems that run on Intel processors, iBCS (Intel Binary Compatibility Specification) is a standard which allows binary programs to be executed between different UNIX systems on Intel processors. UNIX itself is not compatible with iBCS because it uses a different method to execute system calls (int 80 instead of lcall 7). Also, a series of internal kernel structures are organized differently, so direct access to kernel-internal data is not possible. Nevertheless, with the aid of the emulator, it becomes possible to use programs for other UNIX systems under LINUX as well.

+   First, the programs that are not present in LINUX binary format must be loaded into memory. This requires a new loading routine which can read and load these formats. The following binary formats are supported:

+   - aout(with the standard LINUX loading routine)
- ELF, the standard format for LINUX and SVR4
- COFF (Common Object File Format) from SVR3
- XOUT from Xenix 386

Execution of programs of the following operating systems is made possible, partly in a limited form, by the introduction of personalities. These are rules for the conversion of system calls, signals, and error codes. The following personalities are supported:

+   - i386 BSD (386BSD, FreeBSD, NetBSD, BSDI/386) is currently being tested
- SVR4 (Unixware, USL, Dell, and so on)
- generic SVR3
- SCO (SVR3 with extensions)
- Wyse V/386 (SVR3 with extensions)
- Xenix V/386 (only 386 programs in the ‘small model’)
- Xenix V/286