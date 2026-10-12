# **Oracle 10g Release 2 (10.2.0)**

+   Red Hat Enterprise Linux EL 3 or EL 4

+   SUSE Linux Enterprise Server 9.0 (SLES9)

Within these Linux distributions, it is necessary to first install the software development packages in order to have the gcc compiler and libraries installed. If you might need to upgrade the Linux kernel, you should install the kernel development package as well. It is recommended that the following packages be included in the list of packages you choose to install.

# ## Red Hat Linux Packages

When installing Red Hat Linux, it is recommended you install the following packages in addition to the default packages and any other packages you have chosen. This is not a complete list and does not imply that other packages should not be installed.

+   **Development Tools** This set of packages includes the gcc compiler, PERL, python, and debuggers.

+   **Kernel Development** This is not specifically required for installing Oracle, but it is a requirement if you ever need to update the Linux kernel.

The minimum set of components required by the Oracle 10g installation is listed next:

# **System Components for Oracle 10g R1**

| System | Components |
|---|---|
| Red Hat 2.1 and 3.0 | make-3.79 | 
| | binutils-2.11.90.0.8-12 |
| Red Hat Enterprise Linux 2.1 (x86) | gcc-2.96.108.1 | 
| | openmotif-2.1.30-11 |
| Red Hat Enterprise Linux 3 | gcc-3.2.3-2 | 
| | compat-db-4.0.14.5 | 
| | compat-gcc-7.3-2.96.122 | 
| | compat-gcc-c++-7.3-2.96.122 | 
| | compat-libstdc++-7.3-2.96.122 | 
| | compat-libstdc++-devel-7.3-2.96.122 | 
| | openmotif-2.2.2-16 | 
| | setarch-1.3-1 |