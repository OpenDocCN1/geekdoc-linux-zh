# 306 PART 2 | Layered Security and Linux

> TIP
developers behind the Linux kernel are working to make it easier to compile the kernel. Options for the make command are described in the Makefile in the directory with the kernel source.

If the process stops with an error, pay attention to the last messages before the error. There may be an incompatible option in the custom configuration. The commands required to compile a kernel vary slightly, depending on the distribution and release.

# Compile a Kernel on Ubuntu Systems

On Ubuntu systems, the following command should create the new kernel as a Debian-style package in the local directory.

```
# make-kpkg buildpackage --initrd kernel_image
```

# Compile a Kernel on Red Hat Systems

On Red Hat systems, the command is even simpler. But this is one time when it's important to be in the root administrative account. Compiling a kernel even with sudo privileges can lead to errors. From the root administrative account, the following make command creates a kernel and sets up a custom RPM in the /usr/src/redhat/RPMS/`uname -m`

```
# make rpm
```

# Compile a Stock Kernel

When compiling a stock kernel, the distribution-specific commands may not always work. If they don't work, and you're confident that the problem is not related to some custom configuration error in the kernel, run the following command to compile that stock kernel:

```
# make
```

While not strictly necessary, you should also run the following command. Without it, Linux may not have access to modules that are compatible with the custom kernel:

```
# make modules_install
```

When the process associated with these commands is complete, the following command should set up the new kernel and initial RAM disk in /boot/ directory. It should have made changes to the bootloader:

```
# make install
```

# Install the New Kernel and More

The distribution-specific commands to compile a kernel should create appropriate binary packages in the directories just described. You should be able to run appropriate package-management commands such as rpm or dpkg to install the newly customized and compiled kernel. When you do, make sure to use the install switch with the package-management command to avoid overwriting any current and presumably working kernel.