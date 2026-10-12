# # Upgrading with a Kernel RPM

Fedora Core software updates, including new versions of kernels, come in the form of RPM files. To download and install the kernel RPMs, follow these steps:

+   1.  **Use a Web server to download the kernel RPM files from a Fedora Core download site** (I explain the details in the next section).
+       
+       If you want to rebuild the kernel, you have to download the `kernel-source` RPM corresponding to the new version of the kernel.
+   
+   2.  **Install the RPMs by using the `rpm -i` command.**
+   
+   3.  **Create a new, initial RAM disk by running the `/sbin/mkinitrd` command.**
+   
+   4.  **Reconfigure GRUB to boot the new kernel.**
+   
+   5.  **Try out the new kernel by rebooting the system.**

I further describe these steps in the next few sections.

# ## Downloading new kernel RPMs

Fedora Core software updates are distributed in the form of RPMs — packages — from one of the mirror sites listed at `fedora.redhat.com/download/mirrors.html`. The updates are organized into directories according to Fedora Core version numbers. For example, any updates for Fedora Core 1 for 32-bit Intel x86 systems reside in the `fedora/linux/core/updates/1/i386/` directory (for Fedora Core 2 updates, just replace the 1 with a 2 in that pathname). Use a Web browser such as Mozilla to visit a mirror site and download any kernel RPMs available at that site. Another way to get the new kernel RPM is through the normal update process using Up2date or Yum (see Chapter 4 of this minibook for more on how to use Up2date and Yum).

# ## Installing the kernel RPMs

To install the kernel and the modules, follow these steps:

+   1.  **Log in as root.**
+   
+   2.  **Use the `cd` command to change the directory to where the RPM files (the ones you download from a Fedora Core download server) are located.**
+   
+   3.  **Type the following command to install the kernel RPM:**
+       
+       `rpm -ivh kernel*.rpm`