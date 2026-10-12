# Chapter 11

# Configuring the Kernel

# IN THIS CHAPTER

+   - Understanding the need for kernel upgrades
+   - Preparing for a kernel upgrade
+   - Installing a new kernel
+   - Compiling a custom kernel from the source
+   - Patching a kernel's source code
+   - Setting up the kernel with `kernelcfg`

Linux is probably the only operating system that develops a new kernel fairly often. Generally speaking, you can expect a new kernel from Red Hat every two to three months. This should tell you how heavy developmental efforts are in this platform. In this chapter, you learn to upgrade, configure, compile, and install custom kernels.

Linux runs on many hardware architectures, such as x86 (Intel), PowerPC, Alpha, and Sparc, among others. It is practically impossible to discuss kernel issues for all platforms in a single chapter, and therefore I assume that, like a majority of Red Hat Linux users, you have an x86 (Intel)-based system. However, if you are running Red Hat Linux on a system based on the mighty Alpha processor, you can find useful kernel-related information at www.alphalinux.org/. Also, for all architectures, you can go to www.kernel.org/.