**New software interfaces** You may find that a newer kernel provides improved features for programs run on the computer. For instance, the device filesystem mentioned in “Using the New Kernel” is a kernel feature.

Upgrading the kernel requires upgrading your kernel source code, which requires some additional work. In many cases, it’s simpler to recompile your existing source code. On the other hand, unless you track developments very closely, you can’t be sure that the latest kernel source code doesn’t fix an important bug; so if you’re going to recompile your kernel, you might want to perform the additional steps needed to upgrade to the latest version.

> **Note**  
> FreeBSD development is broken into two branches: the STABLE branch and the CURRENT branch. Most FreeBSD systems are in the STABLE branch, which means that they’re fully released, nonbeta software. The CURRENT branch is devoted to prerelease beta-test software. As a general rule, you shouldn’t try to use a CURRENT kernel unless you’re desperate for a new feature it implements or you want to contribute to kernel development. The following directions update your kernel to the latest within your system’s version and development branch.

# Installing a New Kernel

You can obtain a new FreeBSD kernel tree in several different ways. The method described here is closely related to the method described in Chapter 11 for updating the FreeBSD ports tree. In fact, you should review Chapter 11’s “Installing and Updating the Ports System” section before proceeding.

To install a new kernel, follow these steps:

+   1. Follow the directions in Chapter 11 concerning the installation and configuration of the CVSup package, but do *not* type the `cvsup` command to update the system.
+   2. Edit the `/etc/cvsupfile` file. The directions in Chapter 11 specified commenting out any lines that begin with `src.` To update the kernel source code, though, you must ensure that the file *includes* a line that reads as follows, to update the kernel source code:
+   
+      ```
+      src-sys
+      ```
+   3. If you don’t want to update source code other than the kernel (such as the ports system that’s updated in Chapter 11’s instructions), comment out the lines in `/etc/cvsupfile` that relate to those items.
+   4. Type the following command to update the kernel source code:
+   
+      ```
+      # /usr/local/bin/cvsup -g -L 2 /etc/cvsupfile
+      ```