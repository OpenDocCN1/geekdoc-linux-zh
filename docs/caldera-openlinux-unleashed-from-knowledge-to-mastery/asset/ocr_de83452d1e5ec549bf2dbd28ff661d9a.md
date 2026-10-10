This example generates the object files main.o and helper.o, and then links them (along with the C runtime library) to form the executable file program.

Note that gcc was invoked to perform the linking. Although the actual program that performs linking is called ld, you should generally link object files to form an executable using gcc. This is because gcc adds runtime startup code and the C runtime library to the final executable file.

gcc is a front-end to the actual compiler and linker. It examines the filename suffix to determine what to do for each file. Table 36.1 shows how gcc interprets filename suffixes.

# **TABLE 36.1 gcc's Interpretation of Filename Suffixes**

| Suffix | Meaning |
|---|---|
| .c | C source code which must be pre-processed before compilation. |
| .i | C source code that has already been pre-processed. It is simply compiled. |
| .cc, .cxx, .cpp, .C | C++ source file which must be pre-processed before compilation. |
| .ii | C++ source code that has already been pre-processed. |
| .h | C header file. |
| .s | Assembler code. |
| .S | Assembler code which must be pre-processed. |
| other | An object file that is passed to the linker. |

# ## gcc Compilation Options

gcc has many command-line options; they are well-documented in the gcc info page. Table 36.2 lists some of the most common gcc compilation options.

# **TABLE 36.2 Common gcc Compilation Options**

| Option | Meaning |
|---|---|
| -c | Compile source files, but do not link them. Each source file is compiled into a corresponding object file. By default, this file is named by replacing the suffix of the original source file with .o. |
| -E | Only perform pre-processing. The C pre-processor is run for each source file and the result sent to standard output. |