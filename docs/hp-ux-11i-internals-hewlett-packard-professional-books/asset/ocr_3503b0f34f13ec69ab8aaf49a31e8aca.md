These options are only for use by narrow programs (running on either a 32-bit or a 64-bit kernel and hardware platform).

# SHARE_MAGIC

The SHARE_MAGIC directive is the system default and requires no special parameter to be passed to the compiler or linking-loader. The term share as used here refers to the fact the executable image should be built with the code and data separated into different objects. This is necessary if you want to allow multiple copies of the same program to be resident on the system and have them share access to a common text object, reducing overall system memory utilization. This is often called a multiprocess shared-code access model and is implemented on most modern operating systems.

In this model, the various memory objects are assigned to the quadrants according to the default access settings. A program's data and possibly a null-dereference page are placed in Q1. Q2 gets, starting from the lowest offset, the process's private data, comprised of the program's initialized data, uninitialized data (or BSS, an old mainframe term: Block Store by Symbol), and the beginning of the process's heap space (this is where additional data storage may be allocated to a running process using calls such as malloc( )). The uarea is located near the highest offset to Q2, and working back toward the private data area, we have the process's stack, which contains a "red zone" and room for the process's private stack area. Next, we find any private memory mapped objects. The heap grows up, and the maps grow down until there is no space left. The red zone we mentioned is a type of buffer area at the high-address end of the stack: this address space is off limits to the process. In the case of a stack overflow, the kernel must kill the process, and the red zone space is used by the signal code during the kill procedure.

Several tunable kernel parameters control the size of objects located in Q1 and Q2.

+   - maxtsiz limits a 32-bit process's text object; defaults to 16384 pages.
+   - maxtsiz_64bit limits a 64-bit process's text object; defaults to 16384 pages.
+   - maxdsiz limits a 32-bit process's private data object; defaults to 65536 pages.
+   - maxdsiz_64bit limits a 64-bit process's private data object; defaults to 65536 pages.
+   - maxssiz limits a 32-bit process's stack object; defaults to 2048 pages.
+   - maxssiz_64bit limits a 64-bit process's stack object; defaults to 2048 pages.

As you can see, these default values are fairly conservative. The reason for setting these limits along with other tunables is to give the kernel a best guess/mode as to the amount of space it will need to allocate for its internal data tables. It can always allocate more pages as needed, but it is nice to start with a reasonable amount at system boot.

The Q4 and Q3 quadrants are used for shared library text, shared memory, shared memory-mapped files, and other shared objects. The Q4 space is allocated first, then Q3 (this order was established with the release HP-UX 10.0; in previous versions Q3 was used first, then Q4).