# Part II: Ubuntu for Desktop Users

For more information about KVM, the following:

+   - Qumranet's KVM wiki (www.linux-kvm.org/page/Main_Page): Provides overiew information and documentation/HOWTOs for using KVM on various Linux distributions.
- Ubuntu Kernel Virtual Machine (https://help.ubuntu.com/community/KVM): Ubuntu community documentation on installing and using KVM, creating virtual machines of different types, and so on
- KVM on Ubuntu (www.michaeldolan.com/1030): One user's experience with installing KVM on Ubuntu 7.10. This is a nice hands-reference, which doesn't go into any detail about network setup.

# Installing KVM and Related Packages

The software required to use KVM is located in a single package, the qemu-kvm package. You can install this package using your favorite package management tool, as described in Chapter 19. The qemu-kvm package does not include the kernel modules that must be loaded in order to run a virtual machine under KVM—the kvm, ko and qemu-processor,ko modules (where processor is either amd or intel) are always provided and installed as part of the standard Ubuntu Linux kernel. However, these kernel modules are not loaded by default on a standard Ubuntu or Ubuntu system—the qemu-kvm package includes the /etc/init.d/startup and shutdown script, which loads the kvm module and the appropriate module for your processor.

The qemu-kvm package depends on several other packages, such as the bridge utilities (bridge-utilities), IP routing (iproute), SDL (Simple DirectMedia Layer) video (lib11sd.2), and VGA BIOS (vgabios) packages, as well as more standard packages for sound, compression, and so on.

Once the qemu-kvm package is installed, it is quite easy to create a virtual machine and associated disk, install your operating system of choice, and run the virtual machine. The next few sections explain how to manually create a filesystem for a KVM virtual machine, and how-manually installing an operating system into it.

# Creating a Disk for a KVM Virtual Machine

In order to create and use a virtual machine, you must first create a virtual hard disk for use by that virtual machine. This hard disk can be an existing logical volume or physical partition on your system, or a file in any filesystem that you can access. Using a file for a virtual disk for your machine has two primary advantages:

+   - File-based virtual machines can easily be moved or cloned to another computer system that supports KVM by simply copying the file to the other machine.