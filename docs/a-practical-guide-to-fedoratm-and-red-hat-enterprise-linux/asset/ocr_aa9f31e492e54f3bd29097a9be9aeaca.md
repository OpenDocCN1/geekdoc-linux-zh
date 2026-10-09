Before you can start building a new kernel, you must download, install, and prep the source code. You also need to build a configuration file that describes the new kernel you want to build. This chapter describes the steps involved in completing these tasks.

# # **DOWNLOADING, INSTALLING, AND PREPPING THE KERNEL SOURCE CODE**

This section describes how to download kernel source code on the local system. If you want to download code that has not been customized (patched) by Fedora/RHEL, visit kernel.org/pub. This section also covers prepping and installing the kernel source code. See “Configuring and Compiling the Linux Kernel” on page 584 for information on how to proceed after you have downloaded, installed, and prepped the kernel source code.

# ## PREREQUISITES

Install the following packages:

+   • rpmdevtools
+   • yum-utils (installed with the default system)
+   • ncurses-devel (used to configure the kernel using `make menuconfig`)
+   • libglade2-devel (used to configure the kernel using `make gconfig`)

# Compiling a kernel takes a lot of disk space

> TIP Make sure you have enough disk space before you compile a kernel. When you compile a default kernel, it occupies approximately 3.5 gigabytes. This disk space must be available on the filesystem in which you compile the kernel.

# ## MORE INFORMATION

+   **LOCAL** The kernel package includes the latest documentation, some of which might not be available in other documents. You might wish to review the README files included within the source code directories and the relevant files in the Documentation subdirectory.

+   **HOWTO** Detailed, somewhat dated, generic guide to installing and configuring the Linux kernel: *Linux Kernel-HOWTO*

+   **WEB** Kernel source code: kernel.org
+   Secure Boot: fedoraproject.org/wiki/SecureBoot#Questions_and_Answers and `jwboyer.livejournal.com/46149.html`
+   All builds of all packages for multiple architectures plus source code: koji.fedoraproject.org