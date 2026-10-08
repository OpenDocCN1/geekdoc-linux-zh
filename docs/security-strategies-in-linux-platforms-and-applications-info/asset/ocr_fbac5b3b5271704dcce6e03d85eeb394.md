# CHAPTER 2 | Basic Components Linux Security

While the developers behind Linux distributions use the same patches, test their changes on all their target systems. There's often a lag between the release of a security patch and the release of an updated kernel customized for a distribution. On the other hand, developers compile the resulting kernel for you. All you need to install it on your system.

# Distribution-Specific Linux Kernels

For most users, it's best to stick with the binary kernel released for a Linux distribution. That distribution-specific kernel has been compiled and built with the intended hardware in mind, and in many cases has been labeled as such. For example, the standard kernel for Ubuntu's Server Edition has a name with -server extension, such as vlinux-2.6.31-14-server. If the kernel is not needed, it may be optimized for certain purposes—for example, high availability or database systems.

When security issues appear with a Linux kernel, most popular Linux distributions release updates fairly quickly. They do the work to compile the kernel for you. Your compiled kernel packages will even automatically update Linux boot loaders. All you need to do is download and install the updated kernel.

# Custom Linux Kernels

If you choose to customize a Linux kernel, you'll need to get into its nuts and bolts. In Chapter 10, you'll discover that the Linux kernel is quite customizable. A standard Red Hat Enterprise kernel includes about 3000 different kernel options. If you want to preview some of these options, look for a config file in the /boot directory of a Linux system. It is a text file. These options are divided in a number of categories. One standard customization is shown in Figure 2-1.

![](bbox=[0.042, 0.615, 0.958, 0.895])