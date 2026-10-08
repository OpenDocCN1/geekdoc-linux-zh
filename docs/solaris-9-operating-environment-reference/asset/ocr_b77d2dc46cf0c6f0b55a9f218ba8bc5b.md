# as 63

+   -V Write the version number of the assembler being run on the standard error output.

+   -XF Generate additional information for performance analysis of the executable, using SunShop analyzer. If the input file does not contain any stabs (debugging directives), then the assembler generates some default faults that are needed by the SunWork analyzer. Also, see the dbx manual page available with SunWork.

The following options are for SPARC:

+   -q Perform a quick assembly. When you use the -q option, many error checks are not performed. Note: This option disables many error checks. It is recommended that you do not use this option to assemble handwritten assembly language.

+   -xarch=v7 Instruct the assembler to accept instructions defined in the SPARC version 7 (V7) architecture. The resulting object code is in ELF format.

+   -xarch=v8 Instruct the assembler to accept instructions defined in the SPARC V8 architecture, less the quad-precision floating-point instructions. The resulting object code is in ELF format.

+   -xarch=v8a Instruct the assembler to accept instructions defined in the SPARC V8 architecture, less the quad-precision floating-point instructions and less the femlardır. The resulting object code is in ELF format. This choice is the default of the -xarch=options.

+   -xarch=v8plus Instruct the assembler to accept instructions defined in the SPARC V9 architecture, less the quad-precision floating-point instructions. The resulting object code is in ELF format. It does not execute on a Solaris V8 system (a machine with a V8 processor). It does execute on a Solaris V8+ system.

+   -xarch=v9 Instruct the assembler to accept instructions defined in the SPARC V9 architecture, less the quad-precision floating-point instructions, plus the instructions in the Visual Instruction Set (VIS). The resulting object code is in V+ ELF format. It does not execute on a Solaris V8 system (a machine with a V8 processor). It does execute on a Solaris V8+ system.

+   -xarch=v9 Limit the instruction set to the SPARC V9 architecture. The resulting object files are in 64-bit ELF format and can be linked with other object files in the same format. The resulting executable can be run only on a 64-bit SPARC processor running 64-bit Solaris with the 64-bit kernel.