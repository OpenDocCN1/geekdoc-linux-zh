4. -OEAT.COM is the name of the output file. You can call the generated code file anything you want. If you don't specify the name of the output file, NASM will just lop off the “ASM” and call the file EAT. Unfortunately, the name “EAT” doesn’t indicate to DOS that it’s a runnable program, DOS won't know what to do with it. That's why you have to specify the full output file name “EAT.COM” on the command line.

Later on in this book, we're going to invoke NASM from the command line to produce a type of file that NASM-IDE won't be able to tell NASM how to produce. Therefore, we'll have to do it ourselves.

# What Happens When a .COM File Runs

It's useful to know what happens when you run a program of your own creation. DOS treats its two kinds of executable programs a little differently when you run them. .COM files are the simpler of the two. (I speak of .EXE files later in this chapter.) .COM files are a simple image of the instructions and data assembled from the source code file. When you execute a .COM program from the DOS command line, here's what happens:

+   1. The .COM file is loaded into memory at a location of DOS’s choosing. It doesn't change the file when it loads the file; the file is loaded exactly as it was saved to the assembler.
2. AX, DX, BP, SI, and DI are set to 0.
3. The instruction pointer IP is set to 0100H.
4. The number of bytes loaded from disk and stored into memory is placed in the CX register.
5. The stack pointer is set to the highest address in the program’s segment, minus one.
6. All four segment registers CS, SS, DS, and ES are set to the same value: the segment of the single segment in which the .COM program must run. DOS chooses this value.
7. DOS transfers control to the instruction at CS:IP, and your program is off and running!

You can see this very plainly by loading EAT.COM with DEBUG. Here's a dump of the registers immediately after loading EAT.COM into memory: