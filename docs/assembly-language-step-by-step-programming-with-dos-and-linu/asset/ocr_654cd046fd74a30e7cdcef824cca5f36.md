# The Right to Assemble 101

specified. The .OBJ file needs to be processed by another translator program, the linker.

The linker performs a number of operations on the .OBJ file, most of which would be meaningless to you at this point. The most obvious task the linker does is to weave several .OBJ files into a single .EXE executable program. Creating an assembly language program from multiple .ASM files is called modular assembly, and I explain how to do it (with an example) in Chapter 9.

Why create .OBJ files when writing a single executable program? One of two major reasons is size. A middling assembly language application might be 50,000 lines long. Cutting that single monolithic .ASM file up into 8,000-line .ASM files would make the individual .ASM files smaller and much easier to understand.

The other reason is avoiding assembling completed portions of the program every time it is assembled. One thing you will be doing writing assembly language procedures, which are small detours from the main run of steps and tests that can be taken from within the assembly language program. Once you write and perfect a procedure, you can tuck it away in an .ASM file with other completed procedures, assemble it, and then simply link the resulting .OBJ file into the working .ASM file. The alternative is to waste time by reassembling perfect source code over and again every time you assemble the main portion of the program.

This is shown in Figure 4.5. In the upper-right corner is a row of .OBJ files. These .OBJ files were assembled earlier from correct .ASM files, binary disk files containing ready-to-go machine instructions. When the linker links the .OBJ file produced from your in-progress .ASM file, it adds to the previously assembled .OBJ files, which are called modules. The single .EXE file that the linker writes to disk contains the machine instructions from all of the .OBJ files handed to the linker when then linker is invoked.

Once the in-progress .ASM file is completed and made correct, its .OBJ module can be put up on the rack with the others and added to the next in-progress .ASM source code file. Little by little you construct your application program out of the modules you build one at a time.

A very important bonus is that some of the procedures in an .OBJ module may be used in a future assembly language program that hasn't