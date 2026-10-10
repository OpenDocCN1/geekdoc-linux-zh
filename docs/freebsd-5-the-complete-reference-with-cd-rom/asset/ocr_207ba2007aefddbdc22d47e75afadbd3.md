job will take a few seconds as xmkmf checks the files on your system and creates an appropriate Makefile. The configure script that's used by many projects often takes a bit longer to run because these scripts frequently check more details about your system. If the program's documentation describes configuration options, you may want to try applying them to your project. If you're not sure what an option does, do a web search using your favorite search engine, or try to find a more elaborate description in the documentation. MLVVM offers no configuration options.
If you know enough about the compilers used by the program, you can edit the Makefile directly to optimize compilation for your CPU or to achieve other effects. Such changes require a fairly high level of expertise, though, so I don't describe them here.

# Compiling the Software

Typically, compiling the program requires issuing a single command: make. The make program examines the Makefile and uses it as a guide to calling compilers, assemblers, and linkers to create an executable program. Depending upon the size of the project and the speed of your computer, you may find a completed executable just a second or two or many hours after you type make. You'll see a line displayed for each operation that make performs—that is, each file that it compiles. These lines typically begin with cc, gcc, or the name of some other compiler, and include a large number of options. In fact, each line has so many options that it probably occupies two or three lines on a standard 80-column display.
Chances are you'll see occasional compiler warnings, such as the following:

> borders.c:729: warning: `win' might be uninitialized in this function

Warnings are usually harmless; they tell the programmer about a condition that doesn't prevent the program from compiling or running, but that might have unintended consequences. Usually the programmer knows better than the compiler what the code actually does, so you shouldn't be concerned about warnings in program compilation. Errors, on the other hand, cause the compilation process to terminate:

> borders.c: In function `SetUpFrame':
> borders.c:254: `lcp' undeclared (first use in this function)

The output continues with several warnings, then displays the following:

> *** Error code 1
> Stop in /home/rodmith/Projects/mlvwm091/mlvwm.
> *** Error code 1