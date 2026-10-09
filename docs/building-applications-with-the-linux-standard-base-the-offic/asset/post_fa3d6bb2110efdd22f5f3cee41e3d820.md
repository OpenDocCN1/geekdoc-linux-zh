
## 5.4 RUNTIME LIBRARIES

A linker is responsible for linking the executables with the required shared libraries. Though both environments follow the same method for linking, there are some subtle differences (Table 5.3). Linux maintains two different sets of libraries: system libraries and user libraries. Solaris has only one set of libraries.

**Table 5.3: Runtime Library Differences between Solaris and Linux**

| Function | Solaris | Linux |
| :--- | :--- | :--- |
| runtime linker | /usr/lib/lib/ld.so.1 | /lib/ld-linux.so.1 |
| runtime linker configurator | crle | ldconfig |

8. http://www.ibm.com/developerworks/eserver/articles/porting_linux/

## 5.5 FILESYSTEMS

Migrating data from one filesystem to another can be accomplished either by data migration tools or by transferring the data over the network. Data transfer is the most time-consuming of the two. Linux has support for over thirty different filesystems, which are listed in the `mount (8)` manual page. In Solaris the predominant filesystem is UFS, in Linux it is ext2. Table 5.4 gives some filesystem differences between Linux and Solaris.

**Table 5.4: Filesystem Differences between Solaris and Linux**

| Filesystem | Solaris | Linux |
| :--- | :--- | :--- |
| Common filesystem | UFS | ext2/ext3 |
| Journaling filesystems | Veritas | ext3, reiserfs |
| Filesystem for reading CDs | HSFS | iso9660 |
| System information | PROCFS | proc |
| MS-DOS filesystem | PCFS | msdos or vfat |

## 5.6 THREADS

Solaris provides a threading model under which all processes are based on threads called lightweight processes (LWP). In Solaris, a process will be associated with one or more LWP. In the case of Linux, all threads are based on processes and each thread will be mapped to a process.

Solaris supports not only its native threading model but also the POSIX threading model; POSIX threads are also supported on Linux. If an application uses the Solaris native thread model then the application needs a lot of rework before it can be ported. If an application uses on standard proprietary functions, then the Solaris-compatible Thread Library (STL)^9 available on Linux can be used to ease the migration of that application. This library provides the Solaris thread interfaces built upon the POSIX thread library.

## 5.7 ABSOLUTE ADDRESSES

Applications that use hard-coded addresses might be difficult to port. Some applications use `mmap()` calls for page fixing. Since each platform has its own way of handling the program stack, heap, system libraries, and so on, such a call to `mmap()` with a hard-coded address might result in a segment violation.

For instance, some addressing schemes ignore the high-order bits. So a hard-coded address of 0x80000000 might get translated to 0x00000000 and cause unintentional results. It is desirable to eliminate the usage of hard-coded addresses in the code. If an application mandates the use of hard-coded addresses, then it has to be changed to use only an allowed memory range, which you can obtain from `/proc/<application_pid>/map`.

## 5.8 PADDING

When a structure or an aggregate data type are used in the code, each platform has its own way of laying out the constituent elements. This arrangement is dependent on structure, architectural limitations, efficiency, and compiler. Most of the architectures cannot read data from odd addresses. Architectures such as PowerPC are inefficient in reading the data if it starts at an address not divisible by four. So, for efficiency purposes, compilers add the so-called *pad bytes*. The function of these bytes is to maintain byte alignment so that the code can perform efficiently.

On a 4-byte alignment platform, the compiler would lay out the structure in Example 5.6 as shown in Table 5.5, where *P* is padding, d1$_0$, d1$_1$ are bytes of d1, and d2$_0$–d2$_3$ are bytes of d2.

In Table 5.5, the data structure occupies eight bytes because of the padding. On a platform that does not need any alignment, the compiler would lay out the same structure differently (Table 5.6).

**Example 5.6: Pad Bytes**

```c
struct struct1 {
   DATA2 d1;   // data of size 2 bytes
   DATA4 d2;   // data of size 4 bytes
} struct1;
```

**Table 5.5: 4-Byte Alignment**

| Byte 0 | Byte 1 | Byte 2 | Byte 3 |
| :--- | :--- | :--- | :--- |
| d1$_0$ | d1$_1$ | P | P |
| d2$_0$ | d2$_1$ | d2$_2$ | d2$_3$ |

**Table 5.6: No Alignment**

| Byte 0 | Byte 1 | Byte 2 | Byte 3 |
| :--- | :--- | :--- | :--- |
| d1$_0$ | d1$_1$ | d2$_0$ | d2$_1$ |
| d2$_2$ | d2$_3$ | ... | ... |

In Table 5.6, the data structure occupies only 6 bytes. If you are using functions such as `sizeof()` to measure the size of the structure, this behavior has to be taken into account while porting. Most compilers provide options for disabling or enabling byte alignment (including padding) that can be used if necessary, but disabling alignment will usually result in performance degradation.

## 5.9 TOOLSET

### 5.9.1 C/C++ Resources

On the Linux platform, the development tools are mostly those of the GNU Compiler Collection (GCC). GCC includes tools for both C and C++. GNU tools are also available for Solaris.$^{10}$ All Solaris applications can be first compiled with the GNU versions instead of the proprietary Solaris versions. However, the differences between the Solaris **make** utility and the GNU make utility (**gmake**) have to be resolved. The respective documentations can be used for this purpose. Once makefiles are made to work with **gmake**, rebuild the application. The errors thrown from a dry run with this makefile can be classified into command-line option errors and code errors. Command-line option errors are easy to resolve using Table 5.7 that contains the common options for the C compilers on Solaris and the GNU GCC (from *Technical Guide for Porting Applications from Solaris to Linux, Version 1.0*). For additional options, the respective compiler manuals should be used.

**Table 5.7: Differences between Options for Sun Workshop and GCC**

| Sun Workshop | GCC | Description |
| :--- | :--- | :--- |
| -# | -v | Turn on verbose mode, showing each component as it is invoked. |
| -xa | -ansi | Specify compliance with the **ANSI/ISO standard**. The GCC supports all ISO C89 programs. You can use -std to specify the particular version of ISO C. |
| -xinline | -finline-functions | Inline **only those functions which are specified**. |
| -xa | -ax | Generate extra code to write profile information for basic blocks, which will record the number of times each basic block is executed. |
| -xspace | -O0 | Do not optimize. |

![](img/d75cffbcb54aabfb0f9854162061d394_92_0.png)

**Table 5.2 (Continued)**

| Signal | Solaris | Linux |
| :--- | :--- | :--- |
| SIGHUP | Not set | Not set |
| SIGINT | Interrupt | Interrupt |
| SIGQUIT | Terminate | Ignore |
| SIGILL | Terminate | Terminate |
| SIGTRAP | Terminate | Terminate |
| SIGABRT | Terminate | Terminate |
| SIGBUS | Terminate | Terminate |
| SIGSEGV | Terminate | Terminate |
| SIGPIPE | Terminate | Terminate |
| SIGALRM | Terminate | Ignore |
| SIGTERM | Terminate | Terminate |
| SIGUSR1 | Terminate | Ignore |
| SIGUSR2 | Terminate | Ignore |
| SIGCHLD | Ignore | Ignore |
| SIGCLD | Ignore | Ignore |
| SIGPWR | Ignore | Ignore |
| SIGWINCH | Ignore | Process stop |
| SIGURG | Ignore | Ignore |
| SIGPOLL | Terminate | Not supported on Linux |
| SIGSTOP | Process stop | Process stop |
| SIGTSTP | Process stop | Process stop |
| SIGCONT | Ignore | Ignore |
| SIGTTIN | Process stop | Process stop |
| SIGTTOU | Process stop | Process stop |
| SIGVTALRM | Terminate | Terminate, core |
| SIGPROF | Terminate | Ignore |
| SIGXCPU | Terminate, core | Terminate, core |
| SIGXFSZ | Terminate, core | Terminate, core |
| SIGWAITING | Ignore | Not supported on Linux |
| SIGLWP | Ignore | Not supported on Linux |
| SIGFREEZE | Ignore | Not supported on Linux |
| SIGHAWK | Ignore | Not supported on Linux |
| SIGCANCEL | Ignore | Not supported on Linux |
| SIGRTMIN | Terminate | Not supported on Linux |
| SIGRTMAX | Terminate | Not supported on Linux |
