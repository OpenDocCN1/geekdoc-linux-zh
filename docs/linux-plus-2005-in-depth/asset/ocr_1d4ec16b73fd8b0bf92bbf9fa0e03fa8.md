# # Software Installation

Primary responsibilities of most Linux administrators typically include the installation and maintenance of software packages. Software for Linux can consist of binary files that have been precompiled to run on certain hardware architectures such as 32-bit Intel (i386), or as source code, which must be compiled on the local architecture before use. The largest advantage to obtaining and compiling source code is that the source code is not created for a particular hardware architecture. After being compiled, the program executes on the architecture from which it was compiled.

![](bbox=[0.16, 0.33, 0.85, 0.45])

The most common method for obtaining software for Linux is via the Internet. Appendix C, “Finding Linux Resources on the Internet,” lists some common Web sites that host Linux Open Source Software for download.

![](bbox=[0.16, 0.5, 0.85, 0.63])

When downloading software files from the Internet, many Internet sites list a **check-sum** value for the file, which was calculated from the exact file contents. Nearly all checksum values are calculated using a Message Digest 5 (MD5) algorithm. To ensure that the file was received in its entirety after you download it, you should use the **sum command** to verify that the MD5 checksum value is still the same. Simply run the `sum filename` command, where `filename` is the name of the file downloaded.

Program source code is typically distributed in tarball format; the tarball can then be uncompressed and the source code extracted so that it can be compiled. Precompiled binary programs can also be distributed in tarball format, but are typically distributed in a format for use with a package manager.

Recall from Chapter 1, “Introduction to Linux,” that a **package manager** provides a standard format for distributing programs as well as a central database to store information about software packages installed on the system; this allows software packages to be queried and easily uninstalled. The most common package manager used by Linux systems today is the **Red Hat Package Manager (RPM)**.

# ## Compiling Source Code into Programs

The procedure for compiling source code into binary programs is standardized today among most Open Source Software developers. Because most source code comes in tarball format, you must decompress and extract the files. This creates a subdirectory under the current directory