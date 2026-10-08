
# Accessing the Intel® MKL Documentation

This section details the contents of the Intel MKL documentation directory and explains how to access man pages for the library.

# Contents of the Documentation Directory

Table 3-8 shows the contents of the doc subdirectory in the Intel MKL installation directory:

Table 3-8 Contents of the doc Directory

| File name | Comment |
| --- | --- |
| Install.txt | Intel MKL Installation Guide |
| mkl_documentation.htm | Overview and links for the Intel MKL documentation |
| mklULA.txt | Intel MKL end user license |
| mkl.pdf | Intel MKL Reference Manual |
| mkl90_j.pdf | Intel MKL Reference Manual in Japanese |
| mksupport.txt | Information on package number for customer support reference |
| redist.txt | List of redistributable files |
| Release_Notes.pdf | Intel MKL Release Notes |
| userguide.pdf | Intel MKL User's Guide, this document |

# Accessing Man Pages

### During installation

To make the man pages accessible through the man command in your command shell, add the directory with the man pages to the MANPATH environment variable (see Set Environment Variables).

Once the environment variable is set, to view the man page for an Intel MKL function, enter the following command in your command shell:

```
man <function base name>
```

In this release, <function base name> is the function name with omitted prefixes denoting data type, precision, or function domain.

Examples:

- * For the BLAS function ddot, enter man ddot
- For the ScaLAPACK function pgeql2, enter man pgeql2
- For the FFT function DftiCommitDescriptor, enter man CommitDescriptor

> **NOTE.** Function names in the man command are case-sensitive.

![](img/78e923baedeba397a89d376927830122_37_0.png)

# Configuring Your Development Environment

This chapter explains how to configure your development environment for the use with the Intel® Math Kernel Library (Intel® MKL).

Chapter 2 explains how to set environment variables INCLUDE, MKLROOT, LD_LIBRARY_PATH, MANPATH, LIBRARY_PATH, CPATH, FPATH, and NLSPATH. Section Automating Setting of Environment Variables explains how to automate setting of these variables at startup.

For information on how to set up environment variables for threading, see Setting the Number of Threads Using OpenMP® Environment Variable.

# Automating Setting of Environment Variables

To automate setting of the INCLUDE, MKLROOT, LD_LIBRARY_PATH, LIBRARY_PATH, FPATH, and NLSPATH environment variables, add mklvars*.sh to your shell profile so that time you login, the script will automatically execute and set the path to the appropriate Intel MKL directories.

With the local user account, you should edit the following files by adding the appropriate script to the mani section right before exporting variables:

- bash: ~/.bash_profile, ~/.bash_login or ~/.profile

# setting up MKL environment for bash
<absolute_path_to_installed_MKL>/tools/environment/mklvars<arch>.sh

- sh:
  ~/.profile

# setting up MKL environment for sh
. <absolute_path_to_installed_MKL>/tools/environment/mklvars<arch>.sh

- csh:
  ~/.login

# setting up MKL environment for csh
<absolute_path_to_installed_MKL>/tools/environment/mklvars<arch>.

In the above commands, replace mklvars<arch> with mklvars32, mklvars64t, or mklvars64.

If you have super permissions, you can add the same commands to a general-system file in /etc/profile (for bash) and in /etc/csh.login (for csh).

Before uninstalling Intel MKL, remove the above commands from all profile files where the script execution was added, to avoid problems logging in.

# Configuring the Eclipse* IDE to Link with Intel MKL

This section describes how to configure the Eclipse* IDE C/C++ Development Tools (CDT) 3.x and 4.0 to link with Intel MKL.

> TIP. After linking your CDT with Intel MKL, you can benefit from the Eclipse-provided code assist feature. See Code/Context Assist description in Eclipse Help.

# Configuring the Eclipse* IDE CDT 4.0

To configure Eclipse 4.0 to link with Intel MKL, follow the instructions below:

- 1. If the tool-chain/compiler integration supports include path options, go to the Includes tab of the C/C++ General > Paths and Symbols property page and set the Intel MKL include path, that is, <mkl directory>/include.
- 2. If the tool-chain/compiler integration supports library path options, go to the Library Paths tab of the C/C++ General > Paths and Symbols property page and set the Intel MKL library path for the target architecture, such as <mkl directory>/lib/em64t.
- 3. For a particular build, go to the Tool Settings for the C/C++ Build -> Settings property page and specify the names of the Intel MKL libraries to link with your application, for example, mkl_solver_lp64 and mkl_core (compilers require library names rather than file names, so may omit the "lib" prefix and "a" extension). To learn how to choose the libraries, see Selecting Libraries to Link. The name of the property setting where libraries are specified depends upon the compiler integration.

Note that the compiler/linker will automatically pick up the include and library paths only if the automatic makefile generation is turned on; if not, specify the include and library paths directly in the makefile.

# Configuring the Eclipse** IDE CDT 3.x

To eclipse CDT 3.x to link with Intel MKL, follow the instructions below:

- * For Standard Make projects:
  - 1. Go to C/C++ Include Paths and Symbols property page and set the Intel MKL include path to <mkl directory>/include.
  - 2. Go to the Tabs of the C/C++ Project property page and set the Intel MKL libraries to link with your applications, for example, <mkl directory>/lib/64t/lmkl_intel_lp64.a, <mkl directory>/lib/64t/lmkl_intel_thread.a, and <mkl directory>/lib/64t/lmkl_core.a.

To learn how to choose the libraries, see Selecting Libraries to Link.

Note that with the Standard Make, the above settings are needed for the CDT internal functionality only. The compiler/linker not automatically pick up these settings and you will still have to specify them in the makefile.

- * For Managed projects, you can specify settings for a particular build. To do this:
  - 1. Go to the Tool Settings for the C/C++ Build page. All the settings you need to specify are on this page. Names of the particular settings depend upon compiler integration and are therefore not given.
  - 2. If the compiler integration supports path options, set the Intel MKL include path to <mkl directory>/include.
  - 3. If the compiler integration supports library path options, set a path to the MKL libraries for the target architecture, such as <mkl directory>/lib/64t.
  - 4. Specify the names of the Intel MKL libraries to link with your application, for example, mkl_solver_lp64 and mkl_core (compilers require library names rather than library file names, so omit the "lib" prefix and "a" extension). To learn how to choose the libraries, see Selecting Libraries to Link.

# Configuring the Out-of-Core (OOC) DSS/PARDISO Solver

When using the configuration file for the OOC DSS/PARDISO Solver, be aware that the maximum length of the path lines in the file is 1000 characters.

For more information, see the "Sparse Solver Routines" chapter in the Intel MKL Manual.

# Linking Your Application with the Intel® Math Kernel Library

This chapter discusses linking applications with the Intel® Math Kernel Library (Intel® MKL) for the Linux* OS. The chapter provides information on the libraries that should be linked with your application, presents linking examples, and explains building of custom objects.

To link with MKL, which employs the layered linking model, choose one library from the Interface layer, one library from the Threading layer, the library from the Computational layer, and, if necessary, add-run-time libraries. Table 5-1 lists typical sets of libraries to suffice with link MKL.

Table 5-1 Typical Link Libraries

| Interface layer | Threading layer | Computational layer | RTL |
|---|---|---|--|
| IA-32 architecture, static linking | libmkl_intel.a | libmkl_intel_thread.a | libmkl_core.a | libomp5.so |
| IA-32 architecture, dynamic linking | libmkl_intel.so | libmkl_intel_thread.so | libmkl_core.so | libomp5.so |
| Intel® 64 and IA-64 architectures, static linking | libmkl_intel_lp64.a | libmkl_intel_thread_lp64.a | libmkl_core.a | libomp5.so |
| Intel® 64 and IA-64 architectures, dynamic linking | libmkl_intel_lp64.so | libmkl_intel_thread_lp64.so | libmkl_core.so | libomp5.so |

For exceptions and alternatives to the libraries listed above, see Selecting Libraries to Link. See also: Listing Libraries on a Link Line.
