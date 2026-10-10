where it occurred. One debugger found on many UNIX systems is called dbx; it is described in Appendix F.

# 25.8 The make Utility

When writing large programs, it is the usual practice to divide the source code up among several different files. This allows different programmers to work on different parts of the program. It is also more efficient to change and recompile one part of the program at a time, rather than having to compile the entire program whenever a small change is made. The make program is used to keep track of the files making up a large program and to recompile parts of the program as needed. Although **make** is most often used with programs, it can also be useful in updating any project consisting of multiple files.

# 25.9 Other Programming Tools

Most UNIX systems come equipped with a battery of programming utilities, most of which are designed for use in creating C programs:

| Utility | Description | Function |
| :--- | :--- | :--- |
| cb | C beautifier | Formats C source code |
| cflow | Flow analyzer | Shows flow of control in C programs |
| ctrace | Execution tracer | Traces execution of a C program |
| cxref | C tracer | Lists references to variables in C programs |
| lint | C verifier | Warns of potential bugs, portability problems |
| prof | Profiler | Tests efficiency |
| time | Program timer | Times program execution |
| timex | Program timer | Times program execution |