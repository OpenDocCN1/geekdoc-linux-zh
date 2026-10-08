![](bbox=[0.11, 0.12, 0.19, 0.22])

At this point, you can click the New, Edit, and Delete buttons if you want to modify the default disk partitions. You should modify the default partitions only if you're an experienced Unix or Linux user and understand the concept of using multiple partitions. We recommend that unless you feel really lucky or are very experienced, you let Red Hat do the work here.

**9. Click the Next button.**

**10. The Boot Loader Configuration window appears, as shown in Figure 3-2. The defaults should work just fine for you, so click Next.**

The boot loader helps start your operating system when you start your computer; if you create a dual boot computer, the boot loader allows you to select one operating system or another. The standard Red Hat Linux boot loader is GRUB, a powerful system that can do more than just load an operating system. However, the GRUB default options should be all you need (and a description of its advanced features are beyond the scope of this book).

If your computer has an NIC (network interface card), Red Hat detects it and the Network Configuration window appears, as shown in Figure 3-3. You should proceed to Step 1 in the next section and configure your network. However, if you don't have an Ethernet NIC or are using a wireless device that Red Hat doesn't detect, the installation process skips the network configuration and continues at Step 7 in the following section.

![](bbox=[0.23, 0.54, 0.87, 0.93])

**Figure 3-1:** The Disk Setup window displays the partitions to be created.