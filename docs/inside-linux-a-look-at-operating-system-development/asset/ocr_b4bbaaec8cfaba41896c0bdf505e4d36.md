format an output string, compute the sine of an angle, open a display window, etc., instead of rewriting these subroutines each time they are needed.

The executable image is created and moved to memory in stages: first the program source is compiled to an object file, then the necessary libraries are consulted to provide the support code. These subroutines can be bound to the user code in several different ways and at different times. The linker can bind the library code to the user program (1) while the executable is being built, or the loader can bind the library code to the user program (2) when it is loaded into memory, or the loader can bind the library code to the user program (3) at each reference to the library code. This last method of binding is called “dynamic linking”, “dynamic loading”, or sometimes “dynamic libraries”.

![](bbox=[0.12, 0.43, 0.9, 0.72])

By delaying binding until the program is executing, dynamic linking provides an opportunity to (1) use only the latest version of the library and (2) share the library code among programs.

An early version of dynamically linking to libraries can be attributed to Multics.

Linux has supported dynamically linked libraries for some time. Details are discussed in Section 7.1.2