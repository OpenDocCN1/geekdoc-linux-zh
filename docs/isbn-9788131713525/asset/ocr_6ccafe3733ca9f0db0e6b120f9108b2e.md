access). The DAR register tells us that the data address that generated this exception was 0x0000_0000. We know that the moDProbe process produced the error. From the backtrace and NIP (next instruction pointer), we know that it was in a call to strePy() that can be traced directly back to the loop_init() function in the loop_.ko module, which moDProbe was trying to insert at the time of the exception. Given this information, tracking down the source of this errant null pointer dereference should be quite trivial.

# ## 13.5 Binary Utilities

Binary utilities, or binUtils, are a critical component of any toolchain. Indeed, to build a compiler, you must first have successfully built binUtils. In this section, we briefly introduce the more useful tools that the embedded developer needs to know about. As with most of the other tools in this chapter, these are cross-utilities and must be built to execute on your development host while operating on binary files targeted to your chosen architecture. Alternatively, you could compile or obtain versions of these to run on your target, but we assume a cross-development environment for these examples.

# ### 13.5.1 readelf

The readelf utility examines the composition of your target ELF binary file. This is particularly useful for building images targeted for ROM or Flash memory where explicit control of the image layout is required. It is also a great tool for learning how your toolchain builds images and for understanding the ELF file format.

For example, to display the symbol table in an ELF image, use this command:

```
```
s$ readelf -S <elf-image>
```
```

To discover and display all the sections in your ELF image, use this command:

```
```
s$ readelf -e <elf-image>
```
```

Use the -S flag to list the section headers in your ELF image. You might be surprised to learn that even a simple seven-line "Hello World" program contains 38 separate sections. Some of them will be familiar to you, such as .text and .data sections. Listing 13-15 contains a partial listing of sections from our "Hello World" example. For simplicity, we have listed only those sections that are likely to be familiar or relevant to the embedded developer.