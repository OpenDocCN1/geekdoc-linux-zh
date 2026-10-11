ISO standards for C and the 2003 standard for C++ since most Linux programming is done in one of those two languages.

Also, the POSIX standard for library and system call interfaces, while large, has broad industry support. Writing to POSIX greatly improves the chances of successfully moving your code to other systems besides GNU/Linux. This standard is quite readable; it distills decades of experience and good practice.

# Pick the best interface for the job.

If a standard interface does what you need, use it in your code. Use Autoconf to detect an unavailable interface, and supply a replacement version of it for deficient systems. (For example, some older systems lack the `memmove()` function, which is fairly easy to code by hand or to pull from the GLIBC library.)

# Isolate portability problems behind new interfaces.

Sometimes, you may need to do operating-system-specific tasks that apply on some systems but not on others. (For example, on some systems, each program has to expand command-line wildcards instead of the shell doing it.) Create a new interface that does nothing on systems that don’t need it but does the correct thing on systems that do.

# Use Autoconf for configuration.

Avoid `#ifdef` if possible. If not, bury it in low-level library code. Use Autoconf to do the checking for the tests to be performed with `#ifdef`.

# ## 1.6 Suggested Reading

+   1. *The C Programming Language*, 2nd edition, by Brian W. Kernighan and Dennis M. Ritchie. Prentice-Hall, Englewood Cliffs, New Jersey, USA, 1989. ISBN: 0-13-110370-9.
+   This is the “bible” for C, covering the 1990 version of Standard C. It is a rather dense book, with lots of information packed into a startlingly small number of pages. You may need to read it through more than once; doing so is well worth the trouble.

+   2. *C, A Reference Manual*, 5th edition, by Samuel P. Harbison III and Guy L. Steele, Jr. Prentice-Hall, Upper Saddle River, New Jersey, USA, 2002. ISBN: 0-13-089592-X.