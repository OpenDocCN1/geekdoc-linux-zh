# 34 LINUX STANDARDS

# ## 2.4.8 /usr/src - source texts of programs and the kernel

This is where all (non-local) source texts that are needed for the compilation of programs or of the kernel should be stored. The include files of the kernel are particularly important, because these are also required for the compilation of applications. Each distribution that installs the C compiler installs at least the include files in this directory.

The kernel sources can usually be found in the /usr/src/linux directory. It is very important that the include files belonging to the kernel are not copied into the /usr/include directory, but that a symbolic link is established from /usr/include/linux to /usr/src/linux/include/linux. Similarly, a link for the asm directory must be created. If the include files are copied, the result is to be a mixture of old and new files, which can cause the most peculiar errors. For system-related programs such as DOSemu, it is definitely required that the kernel itself be recompiled. At the very least, in any case a make config be executed.

The /usr/src/linux directory (or even /usr/src) itself can be a symbolic link, for example to /var/src. This is sensible for a write-protected file system, such as a 'Life' file system on a CD.

# ## 2.5 /var - variable data

This directory hierarchy contains variable data. Since this hierarchy has only found a wider audience with FHS-compatible distributions, many older systems still do not have a clean separation between /usr and /var. This separation is sensible if we wish to avoid the LINUX partition that is the largest (/usr) having to be mounted with write access. Modern distributions usually follow the rules of the FHS.

With version 2.0 of the FHS, a great changes have taken place, but it will be some time before they become an accepted part of the distributions. These changes are a consequence of LINUX growing closer to other UNIX systems.

Many of the directories were introduced to avoid individual programs or program packages requiring a writable /usr partition. Therefore, some of the directories presented here are optional for many systems, while others must be created by the system administrator for new software. So long as not all programs have been completely adapted to this standard, the system administrator will