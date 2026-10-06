# Using Machine-Specific GNU Compiler Optimizations

GCC also has the ability to use optimizations on the machine to which you expect the application to run. For example, applications running on the Pentium Pro and later Pentium processors can greatly benefit from the -march=686 and -mpu=686 flags. Those flags use processor-specific instructions in the final binary executable that can significantly increase the speed of the application when compared to an executable using the lowest common denominator instruction set. Using these flags is especially important when compiling a Linux kernel, where every ounce of optimization can improve the performance of your system.

Remember one caveat when using machine-specific optimizations on any compiler: The code produced is nonportable. Executables are only guaranteed to run on identical or compatible processors. If an application is compiled with Pentium optimizations, it will most likely not run on an older x86 system that doesn't understand some of the instructions or has the registers available on a Pentium. This problem usually doesn't manifest itself in the other direction—a program built with Pentium optimizations will run on a Pentium because the Pentium instruction set is backward compatible.

![](bbox=[0.047, 0.356, 0.098, 0.396])

# Real-World Example: Optimization Mishaps

A junior administrator was busy compiling optimizations in preparation for an operating system upgrade when he came upon Ghostscript, the PostScript interpreter. He used the -03 optimization flag when compiling, as had with so many applications before. After the compilation completed successfully, the administrator tested the executable, and each time core-dumped with a segmentation fault. After hours of looking for patches and similar problems on newsgroups, he recompiled using the -02 flag, reducing the optimizations. This version of the executable worked fine! Certain parts of the code did not optimize properly under -03, but without those optimizations, the program worked flawlessly. You cannot predict when these optimization failures will occur, but it is easy to experiment with reduced optimizations when they happen

# Setting Process Priorities

One of the oldest methods of performance tuning is setting process scheduling priorities. A priority determines a process's relative importance to other processes running on the same system, when two processes are vying for time on the same CPU, the higher priority process will get to use the CPU first.

The priority of a process in Unix is traditionally known as its "nice" value, named for the command used to set it. The nice command used to make a process play nicely with others; if one process is causing sluggishness on a system by taking up its CPU time, the nice value can be adjusted to lower its priority. Nice values range from -20 to 19, with lesser values having higher priority. The default value is zero.