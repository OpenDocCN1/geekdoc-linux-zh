
# 8.7.1 The ELF Header

The ELF header identifies the file as an ELF file and specifies what kind of ELF file it is. It also specifies the size and location of the program header table and the section header table.

- The first entry is an identifier string containing ELF.
- The second entry is a number which is 1 if the file is an object file, 2 if the file is an executable file, 3 if the file is a shared object file, and 4 if it is a core file. Shared object files are discussed in chapter 11. Core files are produced whenever a program crashes. They are created for debugging purposes.
- The third entry number specifies the machine architecture. The number 3 stands for the x86 architecture.
- There are 11 more entries in the ELF header file, including entries for the size and location of the program header table and the section header table.

# 8.7.2 The Program Header Table

The program header table has one entry for each segment. Each entry in the program header table contains eight items of information:

1. **Type.** The type is 1 if the segment is to be loaded when the file is executed. Other types are not loaded into memory.
2. **File Offset.** This offset gives the location of the segment within the file. Like all offsets, it is the number of bytes from the beginning.
3. **Virtual Address.** This is the address where the first byte of the segment is to be loaded.
4. **Physical Address.** For x86 Linux systems this entry is a misnomer. It is ignored.
5. **File Size.** This is the number of bytes in the segment before it is loaded.
6. **Memory Size.** This is the number of bytes in the segment after it is loaded.
7. **Permissions.** This code contains the read-write-execute permissions.
8. **Alignment.** The segment must begin on a multiple of this entry.

As an example, Table 8.1 lists the Program Header table for `chmod`. Like most Unix commands, the `chmod` command is actually an executable file. On most systems it is located in `/bin`. Table 8.1 was produced by running the ob program on this file.

# 8.7.3 ELF Segments

In Linux 2.0 an executable file typically has five segments. Segment 0 is always the Program Header table. Note that in Table 8.1 the value of the Type field for Segment 0 is 6 for *program header*.

Segments have *read-write-execute* permissions associated with them, just as files in Unix do. The seventh item in each entry of the Program Header table is the permission code for that entry. It is easily understood when written as a binary number. For example, a permission code of 6 means permission to read and write but not to execute.

**Table 8.1. Program Header Table for `chmod`**

```
0034:00d4 Program Header Table
```

| Num | Seg Type | File Offset | Virtual Address | Physical Address | File Size | Mem Size | Perm | Alignment |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 00: | 0006 | 0034 | 8048034 | 8048034 | 00a0 | 00a0 | 0005 | 0004 |
| 01: | 0003 | 00d4 | 80480d4 | 80480d4 | 0013 | 0013 | 0004 | 0001 |
| 02: | 0001 | 0000 | 8048000 | 8048000 | 1d29 | 1d29 | 0005 | 1000 |
| 03: | 0001 | 1d30 | 804ad30 | 804ad30 | 011e | 011fc | 0006 | 1000 |
| 04: | 0002 | 1dc4 | 804adc4 | 804adc4 | 0088 | 0088 | 0006 | 0004 |

Type 1 = loadable, 2 = dynamic info, 3 = interpreter, 4 = note, 6 = program header

| | r | w | x |
| --- | --- | --- | --- |
| | 1 | 1 | 0 |

Note that two of the segments are loadable. These are the code and data segments.

Although the linker combines sections into segments, there are sections which are not part of any segment. The Section Header table lists and describes these sections. These parts of an executable file also occur in an object file and are discussed in section 8.8.

Consider the following C program. Program 8.6 prints out pointers. Pointers are just addresses. Because C is a relatively low-level language, we would expect these pointers to be the same as those occurring in the machine code.

# 8.8 Object Files in ELF Format

Most programs are not written completely from scratch. They rely on programs which have already been written and are used over and over again, such as `printf()`. Files which need other code in order to run are called object code files. It is the job of the linker to combine object code from different files into an executable file. The code for `printf()`, for example, is located in `/lib/libc.so`. Typically the programmer creates one or two of these object code files using gcc or an assembler, and the rest are retrieved by the linker from standard libraries stored on the system. This process is not obvious from the command line since the linker is called by gcc.

It is important to realize that the creation of an object code file is the main purpose of an assembler. In section 8.9, assembler commands for shaping object files will be discussed. But first, object code files themselves need to be described. Just as the format of an executable file is prescribed by ELF, so is the format of an object code file. Figure 8-10 shows the structure of an ELF object code file. The ELF Header in an object file is the same as the ELF header in an executable file.

**Program 8.6**

```c
int a = 0x55555555, b = 0x66666666;
int c = 0x77777777, d = 0x88888888;

main()
{
    /* Store numbers which will be very easy to pick out
       from the machine code of the compiled program. */
    
    a = 0x11111111;
    b = 0x22222222;
    c = 0x33333333;
    d = 0x44444444;

    printf("Variables: Addresses:\n");
    printf(" a %x\n", &a);
    printf(" b %x\n", &b);
    printf(" c %x\n", &c);
    printf(" d %x\n", &d);

    /* %x means to use "hexadecimal" output. */
    printf("\n");
}
```

**Table 8.2. Section Header Table for Program 8.6**

```
01bc:0374 Section Header Table
```

| Name | Type | Flgs | Virtual Address | Offset | Size | Link | Info | Algn | Mod | Entry Size |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 00: | 0000 | 0000 | 0000 | 00000000 | 0000 | 0000 | 0000 | 0000 | 0000 | 0000 |
| 01: | 001b | 0001 | 000c | 00000000 | 0034 | 0091 | 0000 | 0000 | 0004 | 0000 |
| 02: | 0021 | 0009 | 0000 | 00000000 | 0490 | 00a0 | 0009 | 0001 | 0004 | 0008 |
| 03: | 002b | 0001 | 0003 | 00000000 | 00c8 | 0010 | 0000 | 0000 | 0004 | 0000 |
| 04: | 0031 | 0008 | 0003 | 00000000 | 00d8 | 0000 | 0000 | 0000 | 0004 | 0000 |
| 05: | 0036 | 0007 | 0000 | 00000000 | 00d8 | 0014 | 0000 | 0000 | 0001 | 0000 |
| 06: | 003c | 0001 | 0002 | 00000000 | 00cc | 0070 | 0000 | 0000 | 0001 | 0000 |
| 07: | 0044 | 0001 | 0000 | 00000000 | 015c | 0012 | 0000 | 0000 | 0001 | 0000 |
| 08: | 0011 | 0003 | 0000 | 00000000 | 016e | 004d | 0000 | 0000 | 0001 | 0000 |
| 09: | 0001 | 0002 | 0000 | 00000000 | 0374 | 0010 | 000a | 0009 | 0004 | 0010 |
| 0a: | 0009 | 0003 | 0000 | 00000000 | 0464 | 002b | 0000 | 0000 | 0001 | 0000 |

Name: index into the Section Header String Table ( `.shstrtab` )
Type: 1 = Progbits, 2 = Symtab, 3 = Strtab, 4 = Rel, 5 = Hash, 6 = Dynamic, 7 = Note, 8 = Nosbits, 9 = Relplt

# 8.8.1 Section Header Table

The Section Header table lists all the sections in the object file. The table shown in Table 8.2 was produced by running `objdump` on the object file for Program 8.6. The Flags item contains attribute bits, which are somewhat like the permission bits in the program header table of the executable file. Bit 2 is 1 if a section is executable. In Table 8.2 the only section with bit 2 set is section 1, which is in fact the text section. Bit 0 is 1 for writable sections. Only sections 3 and 4 are writable. Section 3 turns out to be the data section.

# 8.8.2 Sections

When the linker creates a text segment, it combines the text sections from the object code files. When it creates a data segment, it combines data sections. The linking process involves collating.

When the gnu linker links .o files, it needs to designate an address where execution is to commence. The programmer can designate this by using the label main and making sure it is visible to the linker by using the global assembler directive.

# Further Reading

Understanding ELF Object Files and Debugging Tools, Mary Lou Nohr, Prentice Hall: 1994.

# Chapter 9. INTERRUPTS

The fetch-execute cycle is a program-driven model of computation. But computers are not totally program driven. To some extent they are hardware driven. CPUs are equipped with input signal pins which allow the fetch-execute cycle to be interrupted. The original purpose of these pins was to increase processor efficiency by reducing the amount of time spent in communication with I/O devices.

In chapter 8 we saw how a device to increase memory efficiency was adopted as a device for controlling memory access. Interrupts have undergone a similar transition. This chapter begins by describing how interrupts economize on processor time. Then, starting with section 9.6, we will see how interrupts are used to control processor access.

# 9.1 Polling
