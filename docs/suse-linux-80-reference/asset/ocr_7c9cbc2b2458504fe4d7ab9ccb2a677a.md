The standard SuSE kernel, written to disk during installation and found in a correctly installed system, under `/boot`, is configured to support as wide a range of hardware as possible. If you have made the right selection during the installation or update, this kernel will be specifically optimized for your processor. Therefore, it is not necessary to compile your own kernel. However, if you want to test experimental features and drivers, you might need to generate a new kernel. You will certainly get an interesting insight into the current state of development.

Several Makefiles are provided with the kernel to automate the process. These Makefiles handle nearly all the details for you. The only thing you have to do by hand is make selections for hardware settings and other kernel features.

# Kernel Sources

To build a kernel, the following packages must be installed: the kernel sources (package `kernel-source`), the C compiler (package `gcc`), the GNU binutils (package `binutils`), and the include files for the C compiler (package `glibc-devel`). They are located in series D (Development). In any case, it is highly recommended to install the C compiler, since the C language is inseparable from UNIX operating systems.

The kernel sources are located in `/usr/src/linux`. If you plan to experiment with different kernels, unpack them in different subdirectories and create a symbolic link to the current kernel source. Since there are software packages that rely on the sources being in `/usr/src/linux`, you should maintain this directory as a symbolic link to your current kernel source to provide an error-free compilation of system programs that need to access the kernel sources.

# Kernel Modules

Many drivers and features no longer have to be compiled directly into the kernel, but can be loaded at run time as kernel modules. The drivers to compile into the kernel and to load as run-time modules is defined in the kernel configuration. Kernel modules are located at `/lib/modules/<Version>`, where `<Version>` is the current kernel version.