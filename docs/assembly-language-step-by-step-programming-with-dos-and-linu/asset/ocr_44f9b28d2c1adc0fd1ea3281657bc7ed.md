# ASSEMBLY LANGUAGE STEP-BY-STEP

If you have a text editor that you've used for some time and prefer, there's no reason not to use it. It just won't make following along with the text quote as easy.

# Compilers and Assemblers

With understanding of DOS files under your belt, you can come to understand the nature of two important kinds of programs: compilers and assemblers. Both fall into a larger category of programs we call translators.

A translator is a program that accepts human-readable source code files and generates some kind of binary file. The binary file could be an executable program file that the CPU can understand, or it could be a font file, or a compressed binary data file, or any of a hundred other types of binary file.

Program translators are translators that generate machine instructions that the CPU can understand. A program translator reads a source code line by line, and writes a binary file of machine instructions that accomplishes the computer actions that the source code describes. This binary file is called an object code file.

A compiler is a program translator that reads in source code files written in higher-level languages as C++ and Pascal and writes out object code files.

An assembler is a special type of compiler. It, too, is a program that reads source code files and outputs object code files for execution by the CPU. However, an assembler is a translator designed specifically to translate what we call assembly language into object code. In the same sense that a language compiler for Pascal or C++ compiles a source code file to an object code file, we say that an assembler assembles assembly language source code to object code file. The process, one of translation, is similar in both cases. Assembly language, however, has an overwhelmingly important characteristic that sets it apart from compilers: total control over the object code.

# Assembly Language

Some people define assembly language as a language in which one line of source code generates one machine instruction. This has never been