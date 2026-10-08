# gprof 465

program. This means that all time spent outside the main object (time spent in object) is not included in the profile summary. Thus, the total time reported for the program may be less than the total time used by the program.

Because the time spent in a shared object cannot be accounted for, you should minimize the time spent of shared objects whenever a program is profiled with gprof. You can link the program to the profiled version of a library (or to the standard archive version if no profiling version is available, instead of to the shared object, to profile information on the functions of the system in the /usr/lib/libprof directory. Refer to compiler documentation on profiling.

Consider an extreme case. A profiled program dynamically linked with the C library hundreds of units of time in routine A, malloc(). Suppose malloc() is called only from routine B and consumes 1 unit of time. Suppose further that routine A consumes 10 units of time, more than any other routine in the (main) portion of the image. In this case, gprof concludes that most of the time is being spent in A and almost no time in B. From this result, it is almost impossible to tell that the greatest improvement can be made by at routine B and not routine A. The value of the profiler in this case is severely degraded; the solution is to use archives as much as possible for profiling.

# Notes

If the executable image has been stripped and has no symbol table (.symtab), then gprof uses the dynamic symbol table. If the dynamic symbol table is used, then the information for global symbols is available and the behavior is identical to that with the -a option

LD_LIBRARY_PATH must not contain /usr/lib as a component when compiling a program for profiling. If LD_LIBRARY_PATH contains it the program links incorrectly with the profiling versions of the system in /usr/lib/libprof.

The times reported by gprof may have variances due to cache-hit ratios that result from sharing the cache with other processes. If a program is the only one used by the machine, hidden background or asynchronous processes may blur the data. In rare cases, ticks initiating recording of the program counter may change because of loops in distort measurements. Call counts are always precisely however.

All programs that call exit or return are guaranteed to produce a profile file, unless another is explicitly coded. Currently shared objects cannot be profiled with gprof. Thus, when a dynamically linked program is executed, only the main portion of the image is sampled. This means that all time spent outside the main object, that time is spent in shared object, not included in the profile summary; the total time reported for the program may be less than the total time used by the program.

With functions as count(), __count(), _moncontrol(), monitor(), and _monitor() may appear in the gprof report. These functions are part of the profiling implementation and thus account for some amount of the overhead. Because these sections are not present in an unprofiled application, you can ignore time accumulated and call counts for these functions when evaluating the performance of an application.

# Bugs

Parents that are not themselves profiled have the time of their profiled children propagated to them, but they appear to be spontaneously invoked in the call-graph listing and do with no time propagated further. Similarly, signal counters, even