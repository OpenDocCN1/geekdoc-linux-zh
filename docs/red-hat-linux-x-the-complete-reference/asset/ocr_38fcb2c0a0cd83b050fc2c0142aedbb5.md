# Installing a New Kernel Version

To install a new kernel, you need to download the software packages for that kernel to your system. You can install a new kernel either by downloading a binary version from your distribution's Web site and installing it or by downloading the source code, compiling the kernel, and then installing the resulting binary file along with the modules. For Red Hat, the binary version of the kernel is provided in an RPM package. You can install a new kernel, just as you would any other RPM software package.

The easiest way to install a new kernel on Red Hat is to use the Red Hat Network update agent (the Red Hat Network is now a subscription service you need to pay for). The update agent automatically downloads, updates, and installs a new kernel. The Red Hat Network does not automatically select kernel files for download. Although they are listed, you have to explicitly select them to be downloaded and installed.

If you want to download kernel RPM packages manually, directly from Red Hat, keep in mind that the complete kernel installation usually includes a series of RPM packages, all beginning with the word kernel. There are also other packages you may need, which contain updated system configuration files used by the new kernel. You can use the packages already installed on your system as a guide. Use the rpm command with the -qa option to list all packages and then pipe that list through the grep command with the kernel pattern to display only the kernel packages:

```
rpm -qa | grep kernel
```

The source code version is available for download from distribution FTP sites and is included on distribution CD-ROMs. You can also download the latest source directly from www.kernel.org. Wherever you download a kernel version from, it is always the same. The source code downloaded for a particular kernel version from a distribution site is the same as the one for www.kernel.org. Patches for that version can be applied to any distribution.

# Red Hat Kernel Packages

As an example, the kernel packages for Red Hat are listed here. You should install only one of the kernel-version-i386 and athlon packages. This will suffice for standard single-processor computers. The others are optimization, support, or configuration packages that you may need, depending on the hardware configuration of your PC, namely for multiprocessor machines, laptops, and computers with memory larger then 4GB. The name includes nptl, which indicates that this version of the kernel supports the Native POSIX Thread Library (NPTL) providing more efficient process control, improving performance and processor scalability.

```
kernel-2.4.22-1.2115.nptl.athlon.rpm
kernel-2.4.22-1.2115.nptl.i586.rpm
kernel-2.4.22-1.2115.nptl.i686.rpm
kernel-doc-2.4.22-1.2115.nptl.i386.rpm
kernel-bigmem-2.4.22-1.2115.nptl.i686.rpm
kernel-pcmcia-cs-3.1.31-13.i386.rpm
kernel-smp-2.4.22-1.2115.nptl.i686.rpm
kernel-smp-2.4.22-1.2115.nptl.athlon.rpm
kernel-utils-2.4.9-1.101.fedora.i386.rpm
kernel-source-2.4.22-1.2115.nptl.i386.rpm
kernel-BOOT-2.4.22-1.2115.nptl.i686.rpm
```

# CPU Kernel Packages

Red Hat provides different kernel packages optimized for various popular CPUs. Choose the appropriate one for your machine. Each package is named kernel, but each has a different qualifier. Red Hat includes three different kernel packages, one for Athlon and Duron CPUs, one for Pentium 2, 3, and 4 CPUs, and one for