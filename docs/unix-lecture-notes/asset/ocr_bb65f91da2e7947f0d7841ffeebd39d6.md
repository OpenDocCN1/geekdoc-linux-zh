System Interface, is a family of standards known formally as IEEE 1003. It is also published by the International Standards Organization (ISO) as ISO/IEC 9945:2003; these are one and the same document. The most recent version of POSIX is IEEE Std 1003.1-2008, also known as POSIX.1-2008. The POSIX.1-2008 standard consolidates the major standards preceding it, including POSIX.1, and the Single UNIX Specification (SUS). The spirit of POSIX is to define a UNIX system, as is stated in the Introduction to the specification (http://pubs.opengroup.org/onlinepubs/9699919799/):

The intended audience for POSIX.1-2008 is all persons concerned with an industry-wide standard operating system based on the UNIX system. This includes at least four groups of people:

+   - Persons buying hardware and software systems
+   - Persons managing companies that are deciding on future corporate computing directions
+   - Persons implementing operating systems, and especially
+   - Persons developing applications where portability is an objective

The Single UNIX Specification was derived from an earlier standard written in 1994 known as the X/Open System Interface which itself was developed around a UNIX portability guide called the Spec 1170 Initiative, so called because it contained a description of exactly 1,170 distinct system calls, headers, commands, and utilities covered in the spec. The number of standardized elements has grown since then, as UNIX has grown.

The Single UNIX Specification was revised in 1997, 2001, and 2003 by The Open Group, which was formed in 1996 as a merger of X/Open and the Open Software Foundation (OSF), both industry consortia. The Open Group owns the UNIX trademark. It uses the Single UNIX Specification to define the interfaces an implementation must support to call itself a UNIX system.

What, then, does this standard standardize? It standardizes a number of things, including the collection of all system calls, the system libraries, and those utility programs such as grep, awk, and sed that make UNIX feel like UNIX. The collection of system calls is what defines the UNIX kernel. The system calls and system libraries together constitute the UNIX application programming interface. They are the programmer's view of the kernel. The utility programs are the part of the interface that the UNIX user sees.

From the Introduction again:

POSIX.1-2008 is simultaneously IEEE Std 1003.1™-2008 and The Open Group Technical Standard Base Specifications, Issue 7.

POSIX.1-2008 defines a standard operating system interface and environment, including a command interpreter (or "shell"), and common utility programs to support applications portability at the source code level. POSIX.1-2008 is intended to be used by both application developers and system implementers [sic] and comprises four major components (each in an associated volume):

+   - General terms, concepts, and interfaces common to all volumes of this standard, including utility conventions and C-language header definitions, are included in the Base Definitions volume.