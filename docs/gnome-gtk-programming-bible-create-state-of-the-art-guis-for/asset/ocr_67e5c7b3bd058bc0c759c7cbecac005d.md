You can compile it from the command line this way:

```
gcc helloworld.c -o helloworld
```

The **gcc** program recognizes the .c extension as being a C program. It compiles the program and links it with the standard libraries and, because of the -o option, writes the resulting executable to the file named *helloworld*. If there were no -o, the executable would have been named *a.out*. Type **/helloworld** and the program runs showing this output:

```
hello, world
```

![](bbox=[0.12, 0.32, 0.18, 0.38])

**Note**
You can use either **cc** or **gcc**. The file /usr/bin/cc is a symbolic link to /usr/bin/gcc. There is a similar program named /usr/bin/g++ that contains some additional features for C++.

The program **gcc** is sort of “Jack of all trades” in the world of compiling and linking. In the command line that compiles the program, **gcc** assumes the program with the .c suffix is a C source code program. As shown in Table 2-1, there are other suffixes recognized by **gcc**.

Table 2-1
Suffixes Recognized by gcc

| Suffix | File Contents |
| :--- | :--- |
| .a | A library file containing one or more object files (also called an archive file) |
| .c | Source code of a C program |
| .C | Source code of a C++ program |
| .cc | Source code of a C++ program |
| .cxx | Source code of a C++ program |
| .h | A preprocessor file |
| .i | Source code of a C program that already has been preprocessed |
| .ii | Source code of a C++ program that already has been preprocessed |
| .m | Source code of an Objective-C program |
| .o | An object file produced from compiling or assembling source code |
| .s | Source code of an assembly language program |
| .S | Source code of an assembly language program that needs to be preprocessed |