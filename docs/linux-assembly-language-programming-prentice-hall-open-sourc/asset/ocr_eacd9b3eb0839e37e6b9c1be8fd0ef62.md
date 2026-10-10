If the space which is occupied by this data is ever written to by the program, then it must be in a data segment. The

section .data

directive is the right tool for this job.

Sometimes stored data is never overwritten. For example, control strings such as "Hello world!" are essentially never written on. This kind of data may just as well be stored in write-protected pages. In the gnu assembler there is a special section label for sections of this kind, .rodata.

# ## 8.5.2 Uninitialized Data Space

Space which is needed by the running program, but which does not contain data initially, may be added to the program when it is loaded. An array declared by

int x[100000];

may well occupy 400,000 bytes of space. Putting such an array into an executable file would be a waste of disk space. To set the space aside at load time, the .bss section label is used.

# ## 8.5.3 Dynamically Allocated Memory

Programs get memory at run time using the system call malloc(). System calls are discussed in chapter 9, section 9.5.

# ## 8.6 I/O Protection

In section 8.3 we have discussed the use of paging as a way of protecting memory from unregulated user access. We have also noted that I/O addressing is unprocessed. It doesn't use paging, segmentation, or any other kind of tampering with the addresses in the brackets. But there is support for I/O protection in the x86 architecture and Linux does use it.

# ## 8.7 Executable Files in ELF Format

In chapter 6, section 6.4 we noted that because programs contain absolute addresses which are not determined until loading time, executable files contain relocation tables which list these locations in the file. These tables need to have some specified format.

In section 8.4 we noted that since programs have segments which are saved on separate pages, depending on whether the segments are writeable or not, the location of these segments within the file must be known to the operating system. If Linux did not have this information, it would not be able to determine which parts of the file to store in writeable pages of memory and which in read-only.

For all these reasons, executable files must have some definite format. The format used by Linux, starting with version 2.0, is called ELF (Executable and Linking Format).

Two other Unix executable file formats are COFF (Common Object File Format) and a.out. Although all Unix systems use a.out as the name of the executable file produced by the C compiler, it is also the name of one particular format for executable files and object code files. At one time all versions of Unix used the a.out format. Now most versions use ELF. The book Understanding and Using COFF presents a thorough description of both COFF and a.out.

Figure 8–9 shows the layout of an executable file in ELF format.

![](bbox=[0.059, 0.94, 0.941, 0.954])