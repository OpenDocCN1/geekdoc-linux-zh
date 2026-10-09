
For standard, nonembedded uses, all three are the same (although some people download binaries and don't care what the build system is). In most embedded scenarios, the build and the host will be the same machine—the workstation on which the developers work—whereas the target will be the embedded board for which you are developing an application.†

When you build software using the GNU configure and build system, as we do here for the various toolchain components, you specify the build, host, and target systems through names in GNU configuration files, which follow a standardized format:

```
cpu-manufacturer-kernel-os
```

The *kernel* component, being a later addition, is optional. In fact, triplets containing only the *cpu*, *manufacturer*, and *os* are still quite common. The various components specify:

-   ***cpu***: The system's chip architecture. Where both a big-endian and little-endian variant exists, it is customary to denote the little-endian variant by appending *el* to the architecture name.
-   ***manufacturer***: A specific maker or family of boards using the aforementioned CPU. As this rarely has any effect on the toolchain itself, it is not uncommon to specify an *unknown* machine type or simply to omit the machine description altogether.
-   ***kernel***: Used mainly for GNU/Linux systems, and even in that case it is sometimes omitted for brevity.
-   ***os***: The name of the operating system (or ABI) used on the system. Configuration names may be used to describe all sorts of systems, including embedded systems that do not run any operating system; in those cases, this field indicates the object file format, such as *Elf* or *COFF*.

Some examples of possible host, target, or build triplets follow:

-   ***i386-pc-linux-gnu***: A PC-style x86 Linux system
-   ***powerpc-8540-linux-gnu***: A Freescale 8540 PowerQuickIII Linux system

> † It's so rare to use a different build system and host system that the situation has earned its own informal name: a "Canadian Cross" toolchain. A Canadian Cross build is most frequently used when building programs to run on a non-Unix system, such as DOS or Windows. It may be simpler to configure and build on a Unix system than to support the non-Unix system's configuration machinery. The unusual name springs from the historical coincidence that Canada had three national political parties at the time developers wanted to invent a name for this procedure.

-   ***mips-unknown-linux***: A big-endian MIPS Linux system from an unspecified manufacturer
-   ***mipsel-linux***: A little-endian MIPS Linux system from an unspecified manufacturer
-   ***xscale-unknown-linux***: An XScale (formerly StrongARM) Linux system from an unspecified manufacturer

Typically, cross toolchain component names are prefixed with the target triplet. Thus, for example, a cross-compiler for a Freescale 8541 PowerQuickIII Linux system will be called `powerpc-8540-linux-gnu-gcc` (gcc being the executable name for the GNU Compiler Collection), whereas the linker for a little-endian MIPS Linux system might be named `mipsel-linux-ld` (ld being the executable name of the GNU linker).

### Linux kernel headers

The first component required for building a toolchain is the set of the Linux kernel headers. Because the C library, which is part of the toolchain, is a wrapper that presents a more palatable API to the application programmer for the raw Linux kernel system calls, compiling the library requires a subset of the Linux kernel header files that describes the kernel API.

In theory, one should always build the toolchain using the Linux kernel headers from the exact same Linux kernel version that will be used on the target. In practice, however, this is rarely done. Because the ABI of the Linux kernel rarely changes (or more correctly, the parts of it described by the headers rarely change), using the headers from a different, but similar, kernel version is commonplace.

In Linux kernel releases prior to the 2.6 series, C library builds were based on a verbatim copy of the headers found in the Linux kernel directories `include/asm-architecture` and `include/linux`. Since the release of Linux 2.6, however, this is no longer supported, as the kernel headers contain much code that is unsuitable for inclusion in user space applications and can easily break the build of user programs, including the C library. Instead, builds use a sanitized version of the Linux kernel headers, suitable for use by user space code such as the C library. As of version 2.6.23 of the Linux kernel, the kernel source is equipped with an automated Make target for building such a “sanitized” version of the Linux kernel headers.

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_115_0.png)

From the kernel source directory, simply issue the following commands, replacing `ppc` with your architecture and `headers/` with the path to the directory where you would like the sanitized headers installed:

```bash
$ make ARCH=ppc headers_check
$ make ARCH=ppc INSTALL_HDR_PATH=headers/ headers_install
```

### Binutils

Another important component of the toolchain is the binutils package. This package includes the utilities most often used to manipulate binary object files. The two most important utilities in the package are the GNU assembler, `as`, and the linker, `ld`. Table 4-2 contains the complete list of utilities found in the binutils package.

*Table 4-2. Utilities found in the binutils package*

| Utility | Use |
| :--- | :--- |
| as | GNU assembler |
| ld | GNU linker |
| gasp | GNU assembler pre-processor |
| ar | Creates and manipulates archive content |
| nm | Lists the symbols in an object file |
| objcopy | Copies and translates object files |
| objdump | Displays information about the content of object files |
| ranlib | Generates an index to an entry in an archive |
| readelf | Displays information about an ELF format object file |
| size | Lists the sizes of sections within an object file |
| strings | Prints the strings of printable characters in object files |
| strip | Strips symbols from object file |
| c++filt | Converts low-level, mangled assembly labels resulting from overloaded C++ functions to their user-level names |
| addr2line | Converts addresses into line numbers within original source files |

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_116_0.png)

Although `as` supports many processor architectures, it does not necessarily recognize the same syntax as other assemblers available for a given architecture. The syntax recognized by `as` is actually a machine-independent syntax inspired by BSD 4.2 assembly language.

### The C library

The standard C library most often used with current day Linux systems is their GNU C library, often abbreviated as glibc. glibc is a portable, high-performance C library supporting all relevant standards (ISO C 99, POSIX.1c, POSIX.1j, POSIX.1d, Unix98, and the Single Unix Specification). It also supports internationalization, sophisticated name resolution, time zone information, and authentication through the use of the NSS, the Name Service Switch, and PAM, the Pluggable Authentication Modules architecture.

The main website for the glibc development project, containing links to the development source tree, bug Database, and many resources, can be found at http://www.gnu.org/software/libc. A list of all platforms the library supports can be found at http://www.gnu.org/software/libc/ports.html, and the library itself can be downloaded from the mirrors found at http://ftp.gnu.org/gnu/glibc.

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_117_0.png)

For recent glibc releases, supported architectures are separated into those supported by the core maintainers (x86, PowerPC, SPARC, SuperH, and their 64-bit counterparts are currently the most interesting to embedded system developers) and those supported by volunteers outside the main glibc core group (currently Arm and MIPS). Code for the latter architectures is in a separate glibc-ports package, which can be downloaded from the same location.

glibc is truly a robust, complete, and modern C library, and it can fit very well in many system designs. Indeed, many embedded Linux systems, especially in the telephony and networking market segments, are based on it. However, because it was never designed to be used in an embedded system context, developers building embedded Linux systems with more limited resources, such as consumer electronic devices, often find its resource usage less compelling.

Being rich and full-featured, glibc is huge. To compound the problem for embedded systems, it is not very modular: removing features is a cumbersome and sometimes even impossible job. Additionally, glibc's designers and implementors have traditionally optimized for performance instead of resource use. For instance, they have optimized for speedier operation at the expense of RAM utilization.

How much of a burden does the size of glibc impose? First of all, the various library files in a minimal glibc take up as much as 2 MB of storage space. But this is by no means the full extent of the problem. Keep in mind that almost every application is compiled against the C library headers. So, the C library also affects the size of application executable files and other libraries.

Executables built with alternative C libraries can be as little as one half the size as those built with glibc, depending on the actual program code and the compiler version used. Savings of 50 percent are quite rare, though; the difference varies widely and occasionally executables end up just as large as they would with glibc.

A similar effect, although usually much less dramatic, can be seen on application run-time RAM usage.

As a rule of thumb, glibc can be a good fit for projects with Flash storage sizes of 16 MB or more. If your project requires smaller RAM, however, you might want to consider popular embedded alternatives such as uClibc and diet libc, which we will describe in the upcoming sections.
