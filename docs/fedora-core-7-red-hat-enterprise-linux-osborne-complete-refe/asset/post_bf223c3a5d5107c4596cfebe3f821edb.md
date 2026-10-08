
On distributions that support RPM packages, you can use an RPM query to learn what version is installed, as shown here:

`rpm -q kernel`

You could have more than one version of the kernel installed on your system. To see which one is running currently, you use the **uname** command with the **-r** option (the **-a** option provides more detailed information).

`uname -r`

The Linux kernel is being worked on constantly, and new versions are released when they are ready. Distributions may include different kernel versions. Fedora includes the most up-to-date stable kernel in its releases. Linux kernels are available at **kernel.org**. Also, RPM packages for a new kernel are often available at distribution update sites. One reason you may need to upgrade your kernel is to provide support for new hardware or for features not supported by your distribution's version. For example, you may need support for a new device not provided in your distribution's version of the kernel. Certain features may not be included in a distribution's version because they are considered experimental or a security risk.

> **NOTE** In many cases, you don't need to compile and install a new kernel just to add support for a new device. Kernels provide most device support in the form of loadable modules, of which only those needed are installed with the kernel. Most likely, your current kernel has the module you need; you simply have to compile it and install it.

> **TIP** Many modules can be separately compiled using *sources provided by vendors*, such as updated network device drivers. For these you only need the Kernel headers, which are already installed in the */usr/lib/modules/version/build* directory, where *version* is an installed kernel version. In these cases, you do not have to install the full kernel source to add or modify modules.

## References

You can learn more about the Linux kernel from **kernel.org**, the official repository for the current Linux kernels. The most current source code, as well as documentation, is there. Your distribution Web site will also provide online documentation for installing and compiling the kernel on its systems. Several Linux HOW-TOs also exist on the subject. The kernel source code software packages also include extensive documentation. Kernel source code files are always installed either directly in a local directory or in the Fedora */usr/src/redhat/BUILD* directory (the */usr/src/kernels* directory is used for library headers, not the kernel source). The source itself will be in a directory labeled *linux-version*, where *version* is the kernel release, as in **linux-2.6.21**. In this directory, you can find a subdirectory named */Documentation*, which contains an extensive set of files and directories documenting kernel features, modules, and commands. The following listing of kernel resources also contains more information:

- **kernel.org**
  The official Linux kernel Web site. All new kernels originate from here
- **www.linuxhq.com**
  Linux headquarters, kernel sources, and patches
- **kerneloops.org**
  Linux kernel sources and information
- **en.tldp.org**
  Linux Documentation Project

## Kernel Tuning: Kernel Runtime Parameters

Several kernel features, such as IP forwarding or the maximum number of files, can be turned on or off without compiling and installing a new kernel or module. These tunable parameters are controlled by the files in /proc/sys directory. Parameters that you set are made in the /etc/sysctl.conf file. Fedora installs this file with basic configuration entries such as those for IP forwarding and debugging control. You use the sysctl command directly. The -p option causes sysctl to read parameters from the /etc/sysctl.conf file (you can specify a different file). You can use the -w option to change specific parameters. You reference a parameter with its key. A key is the parameter name prefixed with its proc system categories (directories), such as net.ipv4.ip_forward for the ip_forward parameter located in /proc/sys/net/ipv4. To display the value of a particular parameter, just use its key. The -a option lists all available changeable parameters. In the next example, the user changes the domain name parameter, referencing it with the kernel.domainname key (the domainname command also sets the kernel.domainname parameter):

```bash
# sysctl -w kernel.domainname="mytrek.com"
```

The following example turns on IP forwarding:

```bash
# sysctl -w net.ipv4.ip_forward=1
```

If you use just the key, you display the parameter’s current value:

```bash
# sysctl net.ipv4.ip_forward
net.ipv4.ip_forward = 1
```

## Installing a New Kernel Version

To install a new kernel, you need to download the software packages for that kernel to your system. You can install a new kernel either by downloading a binary version from your distribution’s Web site and installing it or by downloading the source code, compiling the kernel, and then installing the resulting binary file along with the modules. For the binary version of the kernel is provided in an RPM package. You can install a new kernel, just as you would any other RPM software package.

The easiest way to install a new kernel on Fedora is to use Pirut. Pirut will automatically download and install a new kernel. The installation will create a GRUB entry so that when you boot, the new kernel will be listed as one of the options, usually the default.

If you want to download kernel RPM packages manually, keep in mind that the complete kernel installation usually includes a series of RPM packages, all beginning with the word kernel. There are also other packages you may need, which contain updated system configuration files used by the new kernel. You can use the packages already installed on your system as a guide. Use the rpm command with the -qa option to list all packages and then pipe that list through the grep command with the kernel pattern to display only the kernel packages:

```bash
rpm -qa | grep kernel
```

The kernel source code version is available for download from distribution FTP sites in the source directory and is included on distribution source code CD-ROM. You can also download the latest source directly from www.kernel.org. Wherever you download a kernel version from, it is always the same. The source code downloaded for a particular kernel version from a distribution site is the same as the one for www.kernel.org. Patches for that version can be applied to any distribution.

## CPU Kernel Packages

Fedora and Red Hat provide different kernel packages optimized for various popular CPUs. Choose the appropriate one for your machine. All the kernels include multiprocessor support. The x86 distribution will include the x86 versions, and the 64-bit distribution will hold the x86_64 versions. Each package is named kernel, but each has a different qualifier. For the x86, there are two different kernel packages, one for the newer Pentium 2, 3, and 4 CPUs, and one for the older Pentiums, AMD K6 CPUs, and other older systems. Each package will have a CPU reference in its filename: 686 for Pentium 2, 3, and 4; 586 for Pentium, K6, and other systems.

```text
kernel-2.6.version.i586.rpm
kernel-2.6.version.i686.rpm
```

For 64-bit systems, like the Athlon 64 series, the 64-bit distribution will include only an x86_64 package.

```text
kernel-2.6.version.x86_64.rpm
```

There are also kernel packages for the Xen virtualization and the PAE kernel for extended system memory support (kdump support is included in 32 bit kernels).

```text
kernel-xen
kernel-PAE
```

For each kernel, there are also corresponding kernel header packages (also known as builds), denoted with the term devel, that contain only the kernel headers. These are used for compiling kernel modules or software applications that do not need the full kernel source code, just the headers. The headers for your current kernel are already installed. The kernel headers will be installed in the /usr/src/kernels directory with a build link to it in the kernel’s /lib/modules directory.

## Installing Kernel Packages: /boot

You will not need all of these packages. For example, for a simple kernel upgrade for a basic Pentium computer, you would need only the 686 package. You can download and install easily using Pirut, and searching for “kernel.” Also, the PUP Package updater will automatically download and install new kernels as they become available, selecting the version appropriate for your system.

Should you want to install manually, you can use the rpm command in a terminal window. To make sure a kernel RPM package was downloaded without any errors and to verify its authentication, you can use the rpm command with the -K option (to authenticate the package, you need the public key):

```bash
rpm -K *rpm
```
