+   You need to compile support for a hardware device into the kernel rather than loading it as a module.
+   You want to use an updated version of the Linux kernel to add new features or fix a security problem that was discovered with your current version.

For any of these reasons, you can recompile the Linux kernel from source code, creating a new kernel. The file vmlinuz-2.6.5-1.358 contains the Linux kernel that is used when you start your system. It is usually located in the / directory or in the /boot directory.

When you create a new kernel from source code, that kernel is stored in a subdirectory of /usr/src/linux (based on the kernel version number you are working with). Creating a new kernel involves three steps:

+   1. Make certain the kernel source code and supporting packages are installed on your system.
+   2. Configure which features you want the new kernel to have.
+   3. Execute the commands to compile the source code with the features you selected.

# Installing Kernel Source Code

Before recompiling the kernel, you must have several packages installed on your system, such as the source code itself, the compiler, and numerous supporting packages. In Red Hat Linux and Fedora, the source code is in a single (175 MB) rpm named kernel-source. You can use the rpm command with the -q option to see if this package is installed:

```
# rpm -q kernel-source
```

If this package is not installed, you can use the rpm command to install it, but you will probably see that other supporting packages are needed before you can install the kernel-source package. For this reason, the kernel source code was indicated in Chapter 8 as a category that was recommended for installation. If you need to install the kernel source code after installing Linux, use the rpm command to install whatever additional packages are needed, then install the kernel-source package.

![](bbox=[0.12, 0.88, 0.18, 0.97])

> You can always download raw source code (not in an rpm-format software package) from www.linuxhq.com.

Once the source code is installed, you can explore the source code files in the directory /usr/src/linux-2.6.5-1.358. When you recompile the source code to create a new kernel file, you are not changing the version of the kernel. You are only changing the features that are activated in the kernel. After you recompile the kernel, the timestamp on the kernel you create is different than the kernel that was installed by default on your system.