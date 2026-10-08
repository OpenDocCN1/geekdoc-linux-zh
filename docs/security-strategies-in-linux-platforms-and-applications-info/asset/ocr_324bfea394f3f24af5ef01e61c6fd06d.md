# PART 2 Layered Security and Linux

Note that some distributions regulate the number of kernels that can be installed on a Ubuntu system. The kernel and initial RAM disk files associated with a kernel can be quite large. Many distributions, including Red Hat, configure the /boot directory on a fairly small partition. By default, Red Enterprise Linux 5 specifies a size of 100MB for this partition.

If you've compiled a custom kernel, the initial RAM disk for that kernel can easily reach several dozen megabytes, which can limit the number of kernels that are practical to install on a system.

# Kernel Development Software

To recompile a kernel, you'll need to install packages with C language libraries and compilers, kernel header files, preprocessors, and related development tools. If you want to use menu-based kernel customization tools, additional packages are required.

Required development software varies by by distribution. Some of the differences are based on the Ubuntu and Red Hat systems are configured. The commands for Ubuntu systems have changed from the Hardy Heron (8.04) to the Lucid Lynx (10.04) releases. The packages required for Red Hat systems are also subject to change.

When installing such software, keep careful records of the packages that are installed. When installed on production systems, the software associated with compiling the kernel may present risks. It may also allow black-hat hackers to compile more dangerous malware from your systems. If kernel development software is installed on a production system, be sure to remove that after the new kernel is operational.

# Red Kernel Development Software

The packages listed in this section can be used to customize and build a kernel on Red Hat systems. While the same basic functionality is required to build kernels on other Linux systems, at least the package names will vary. The key packages are listed in Table 10-2.

| TABLE 10-2 Red Hat kernel development packages |
| PACKAGE | DESCRIPTION |
| binutils | Binary utilities |
| cpp | C language pre-processor |
| gcc | GNU's not UNIX (GNU) C language compiler |
| glibc-headers | Kernel header files |
| glibc-devel | Kernel development files associated with C language libraries |
| ncurses | New curses library for updating character screens; supports the make menuconfig command |