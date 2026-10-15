far outweighs the increase in code size. Figure 17.1 also shows some language statement examples to demonstrate the increased readability of programs as the level of programming languages increases.

# 17.3 THE COMPILATION PROCESS

Because our focus in this chapter is on UNIX tools—primarily for the C programming language (a compiled language)—we need to describe briefly the compilation process before moving on. As we stated in Section 17.2, computer programs written in compiled languages must be translated to the machine code of the CPU used in the computer system on which they are to execute. This translation is usually a three-step process consisting of compilation, assembly, and linking. The compilation process translates the source code (e.g., a C program) to the corresponding assembly code for the CPU used in the computer system. The assembly code is then translated to the corresponding machine code, known as object code. Finally, the object code is translated to the executable code. Figure 17.2 outlines the translation process.

The object code consists of machine instructions, but it is not executable because the source program might have used some library functions that the assembler cannot resolve

![](bbox=[0.4, 0.58, 0.6, 0.92])

FIGURE 17.2 The process of translating a high-level language program to executable code.