One of the most rewarding experiences that Linux provides is that of creating your own working kernel. Other proprietary systems restrict you to using the kernel or core element of the operating system as it comes installed. However, because the entire Linux system is open-sourced, you can view the text that comprises the foundation of Linux and thus compile it anew and create a new kernel. With each succeeding release of a newer, more stable kernel, the Linux operating system becomes that much more dynamic and responsive.

This chapter covers the steps required to build a new kernel as well as the following subjects:

+   ◆ Understanding the difference between default and customized kernels
+   ◆ Locating the most recent Linux kernel
+   ◆ Distinguishing stable source code from developmental source code
+   ◆ Choosing the right options for your machine
+   ◆ Compiling the actual code
+   ◆ Inserting modules into running kernels
+   ◆ Patching existing kernels
+   ◆ Troubleshooting bad kernel installs

# ## Defining the Linux Kernel

The Linux kernel is what runs the Linux operating system. Under most Red Hat installs, the kernel itself is located in the `/boot` directory and is called *vmlinuz*. Because the core of the Linux kernel is always in memory, the smaller the kernel, the faster your system will run. Rather than booting up the machine with every possible device driver preloaded, Linux loads only those drivers required by your machine. If you are compiling your own kernel, you can state exactly what drivers you want loaded or reduce the number of unnecessary devices recognized by your machine.