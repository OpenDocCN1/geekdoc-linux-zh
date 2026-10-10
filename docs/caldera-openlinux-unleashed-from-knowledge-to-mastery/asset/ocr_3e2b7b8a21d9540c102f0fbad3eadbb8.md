# Development Environment

# PART V

Serious programmers need powerful development environments to write programs. This chapter introduces some of the GNU development tools included with Linux. I discuss the gcc C and C++ compiler, the GNU make program for building projects, and the gdb source-level debugger.

Most large UNIX programs are written in C or C++, and the GNU development tools are perfect for these projects. This chapter introduces the GNU tools so you will know how to start a programming project. It cannot cover them in great depth; fortunately, the GNU tools have excellent info pages. This chapter does, however, give you the background you need to understand the info pages.

For this chapter, I assume you are familiar with C or C++ programming on some platform and understand the basic concepts of editing, compiling, linking, and debugging. This chapter also introduces you to the Linux-specific tools for performing these tasks.

# Terminology

I use several programming terms in this chapter. Here is a definition of each term:

+   - **Source File**—A text file containing C or C++ source code: C source filenames usually end with `.c` (although headers can end with `.h`), and C++ source filenames end with `.C`, `.cpp`, `.cxx` or `.cc`. (My preference is to use `.cc`.)
+   - **Executable**—A binary file which that is a complete program. An executable can be run from the shell prompt by typing its pathname.
+   - **Object File**—A file containing machine code and linker information. Object files cannot be directly executed; they must be linked to form an executable. Object file- names end with `.o`.
+   - **Linker**—A program that combines object files into an executable. The linker resolves references to symbols across object files.

**Note**

Actually, the linker need not produce an executable—it can produce a larger, partially-linked object file. For the purposes of this chapter, the linker will always be used to produce an executable.

+   - **Library Archive**—A library archive is a collection of object files placed into one file for ease of file maintenance. The linker can extract individual object files from the library archive. Library archive filenames end with `.a`.