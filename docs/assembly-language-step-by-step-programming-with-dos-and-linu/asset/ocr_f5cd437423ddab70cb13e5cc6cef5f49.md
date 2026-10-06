business. While it looks like gcc does all the work, what gcc really does is act as master controller for several GNU tools, supervising a code assembly line that you don’t need to see unless you specifically want to.

Theoretically, this is all you need to do to generate an executable binary from C source code:

```
gcc eatc.c -o eat
```

Here, gcc takes the file eatc.c (which is a C source code file) and crunches it to produce the file. The (–o option tells gcc what to name the executable output file). Note well that in the Linux world, executable files typically do not have file extensions, as they do DOS and Windows. What might be eatc.com or eatc.exe under DOS is simply eat under Linux.

However, there’s more going on here that meets the eye. Take a look at Figure 12.1 as we go through it. In the figure, shaded arrows indicate movement of information. Blank arrows indicate program control.

The programmer invokes gcc from the shell command line. gcc takes control of the system and immediately invokes a utility called the C processor, cpp. The preprocessor takes the original C source code file and handles items like #includes and #defines. It can be thought of as a sort of macro expansion pass on the source code file, if “macro expansion pass” means anything to you. If not, don’t fret it—it’s C thing and not germane to assembly work.

When cpp is finished with its work, gcc takes over in earnest. From the preprocessed source code file, gcc generates an assembly language source code file with a .s extension. This is literally the assembly code equivalent of the C statements in the original .c file, in human-readable form. If you develop any skill in reading AT&T syntax and mnemonics, you can learn a lot from inspecting the .s files produced by gcc.

When gcc has completed generating the assembly language equivalent of the C source code file, it invokes the GNU assembler, gas, the .s file into object code. This object code is written out in a file with a .o extension.

The final step involves the GNU linker, ld. The .o file contains binary code, but it’s only the binary code generated from statements in the original .c file. The .o file does not contain the code from the standard C