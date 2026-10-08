# # Chapter 2. Preparing the Host System

# ## 2.1. Introduction

In this chapter, the host tools needed for building LFS are checked and, if necessary, installed. Then a partition which will host the LFS system is prepared. We will create the partition itself, create a file system on it, and mount it.

# ## 2.2. Host System Requirements

Your host system should have the following software with the minimum versions indicated. This should not be an issue for most modern Linux distributions. Also that many distributions will place software headers into separate packages, often in the form of “<package-name>-devel” or “<package-name>-dev”. Be sure to install them if your distribution provides them.

Earlier versions of the listed software packages may work, but have not been tested.

+   - Bash-3.2 (/bin/sh should be a symbolic or hard link to bash)
- Binutils-2.25 (Versions greater than 2.32 are not recommended as they have not been tested)
- Bison-2.7 (/usr/bin/yacc should be a link to small or script that executes bison)
- Bzip2-1.0.4
- Coreutils-6.9
- Diffutils-2.8.1
- Findutils-4.2.31
- Gawk-4.0.1 (/usr/bin/awk should be a link toawk)
- GCC-6.2 including the C++ compiler, g++ (Versions greater than 9.2.0 are not recommended as they have not been tested)
- Glibc-2.11 (Versions greater than 2.30 are not recommended as they have not been tested)
- Grep-2.5.1a
- Gzip-1.3.12
- Linux Kernel-3.2

The reason for the kernel software requirement is that we specify when when building glibc in Chapter 6 at the recommendation of the developers. It is also required by udev.

If the host kernel is earlier than 3.2 you need to replace the kernel with a more up to date version. There are two ways to go about this. First, see if your Linux vendor provides a 3.2 or later kernel package. If so, you may wish to install it. If your vendor doesn't offer an acceptable kernel package, or you prefer not to install it, you may compile a kernel yourself. Instructions for compiling the kernel and configuring the boot loader (assuming the host uses GRUB) are located in Chapter 8.

+   - M4-1.4.10
- Make-4.0
- Patch-2.5.4
- Perl-5.8.8
- Python-3.4
- Sed-4.1.5
- Tar-1.22