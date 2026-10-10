make This is the heart of the matter. This builds the executable kernel image and all kernel modules. Not surprisingly, this takes a while. The resulting compressed kernel image is arch/$(ARCH)/boot/zimage.

The following step requires root user privileges.

make modules_install INSTALL_MOD_PATH=/export/rootfs. Copies the modules to $(INSTALL_MOD_PATH)/lib/modules/<kernel_version> where <kernel_version> is the string identifying the specific kernel you are building. Note that when building for the target board, you must explicitly specify the root file system. Otherwise, the modules will go into /lib/modules of your workstation's file system. Strictly speaking, this step is not necessary in this case, because none of the modules are required to boot the kernel.

That is it. Note, incidentally, that the build process is recursive. Every subdirectory in the kernel source tree has its own Makefile dealing with the source files in that directory. The top level Makefile recursively invokes all of the sub Makefiles.

The process for building a kernel for your workstation differs in a couple of details. Do make modules_install without the INSTALL_MOD_PATH argument, and then execute this step, also as root:

make install. This does several things. It copies the kernel executable, called vmlinuz for x86 builds, to /boot along with System.map, the linker map file. It adds a new entry to /boot/grub/grub.conf, so the GRand Unified Bootloader can offer the new kernel as a boot option. Finally, it creates an initial ramdisk, initrd, in /boot.

# Workstation Digression

Before we move on to loading and testing our new kernel, the last two items mentioned above deserve a passing explanation. Most workstation installations these days incorporate a boot loader called GRUB (GRand Unified Bootloader) to select the specific kernel or alternate operating system to boot. There is a very good reason for having the ability to boot multiple kernel images. Suppose you build a new kernel and it fails to boot properly. You can always go back and boot a known working image, and then try to figure out what went wrong in your new one. If you are curious, have a look at the file /boot/grub2/grub.cfg on your workstation. You will need to be root user to get into the grub2 directory.

Most Linux kernels are set up to use initrd, which is short for initial ramdisk. An initial ramdisk is a very small Linux file system loaded into RAM by the boot loader and mounted as the kernel boots, before the main root file system is mounted. The usual reason for using initrd is that some kernel modules need to be loaded before mounting the root partition. Usually, these modules are required to support the file system used by the root partition, ext3 for example, or perhaps the controller that the hard drive is attached to, such as SCSI or RAID.