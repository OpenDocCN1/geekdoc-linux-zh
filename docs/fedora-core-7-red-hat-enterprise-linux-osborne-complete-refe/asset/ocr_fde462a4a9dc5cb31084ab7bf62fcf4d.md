directory in /usr/src/kernels/version or to the link in /lib/modules/version/source. The following example creates /usr/src/linux as a symbolic link to /usr/src/kernels/2.6.21-1.3116.fc7-686.

```
ln -s /usr/src/kernels/2.6.21-1.3116.fc7-686 /usr/src/linux
```

You can then compile your module or run your script.

If you have more than one kernel installed on your system, be sure to make the /usr/src/linux symbolic link reference the kernel you want to create the module for. Each kernel binary RPM package will include its own source subdirectory with its own kernel headers. These are used for creating modules for its kernel. You cannot mix module and headers for one kernel with another. Be sure kernel-devel package is installed.

# ## Installing New Modules from the Kernel

The source code for your Linux kernel contains an extensive set of modules, of which not all are actually used on your system. The kernel binaries provided by Fedora come with an extensive set of modules already installed. If, however, you install a device for which kernel support is not already installed, you will have to configure and compile the kernel module that provides the drivers for it. This involves using the kernel source code to select the module you need from a list in a kernel configuration tool, and then regenerating your kernel modules with the new module included (see Chapter 33). Then the new module is copied into the module library, installing it on your system. You can also enter it in the /etc/modprobe.conf file with any options, or use modprobe to install it manually.

First, make sure you have installed the kernel source code in the /usr/src/redhat/BUILD directory. If not, simply use the rpm tool to install the kernel source RPM package for Fedora. This can be found with the SRPMS for your distribution. To generate the source code, you then use the rpmbuild command with the kernel spec file and specify the type of architecture you want. Change to the /usr/src/redhat/SPECS directory and run the rpmbuild command with the -bp option (build) and the --target option to specify the architecture. The following command will extract the i686 version of the kernel:

```
rpmbuild -bp --target=i686 kernel-2.6.spec
```

If instead you are using the original source code version of the kernel in the compressed archive from kernel.org, then unpack it in any directory (but do not use /usr/src/linux).

Now change to the kernel directory. For the RPM source package it is in /usr/src/redhat/BUILD/kernel-version/linux/version, where version is the kernel version. Then use the make command with the gconfig or menuconfig argument to display the kernel configuration menus, invoking them with the following commands. The make gconfig command starts an X Window System interface that needs to be run on your desktop from a terminal window.

```
make gconfig
```

Using the menus select the modules you need. Make sure each is marked as a module, clicking the Module check box in gconfig or typing m for menuconfig. Once the kernel is configured, save it and exit from the configuration menus. Then you compile the modules, creating the module binary files with the following command:

```
make modules
```