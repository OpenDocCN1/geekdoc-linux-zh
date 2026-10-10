# # Programs, Processes, and Threads

The study of UNIX internals may be approached from several points of view. One is to simply define all the individual kernel data structures and their basic functionality. While this presents a suitable framework for our study, we would like to also consider the kernel's construction and utilization from the perspective of an individual process or thread. The kernel perspective is macro in its scope, while the view from a process or thread is more closely related to the user or programmer's perspective.

# ## The Players

There was a time when the process was the smallest schedulable entity of concern to the kernel; today, however, that honor belongs to the thread. Before we discuss HP-UX kernel structures in depth, we must define the relationship between programs, processes, and threads.

# ### The Program

The term *program* refers to a file that stores an executable image. A program file contains a header record defining the architecture for which it was compiled, magic numbers, and a list of system resources it will require access to during its execution life cycle.

The first HP series 800 computers were based on the then newly developed 32-bit HP Precision Architecture (PA-RISC 1.x) chip set. This product line was called the Specturm computing platform. The linking-loader for this architecture used a proprietary header format called the Spectrum Object Module, or SOM. With the advent of the 64-bit HP Precision Architecture (PA-RISC 2.0), the loader format adopted was the POSIX Executable Linking Format (ELF) defini-