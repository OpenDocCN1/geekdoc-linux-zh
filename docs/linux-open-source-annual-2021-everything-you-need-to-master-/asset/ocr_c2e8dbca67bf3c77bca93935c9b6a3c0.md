# # QEMU and KVM

Dig deeper and build your own virtual machine at command using the power of Linux.

VirtualBox is all well and good, but there are other people who don't like using Oracle software, and in the past extensions (which enabled graphics acceleration and shared clipboards) weren't free licensed, meaning they couldn't be bundled or installed separately.
This is the longer case and most difficult when the required host and guest modules - mismatched (if guest is running), for example - and the host must be installed manually. These can be installed on all platforms - in running VM by installing Guest Additions from the menu. A virtual CD will be inserted and you'll find a link to install such modules, as well as Windows and MacOS.
Anyway, we were supposed to talk about VirtualBox, not providing advice. So, there's free (but not open source)
VMware Player, which allows running a single machine on the desktop and in a user's view which works as much as VirtualBox. However, the virtualisation remained not because people could run clunky desktop operating systems within another clunky desktop operating system,

because powerful servers could house multiple VMs - saving resources, increasing portability and generally making them work. Workstation Pro is VMware's commercial offering, and there are Hyper-V, Xen and other tools that revolutionized infrastructure management. One of them is cheap QEMU (VPA virtual partitions from there) of Linux Debian and Ocean Ubuntu. These are a great way to get what server administration is all about.
When you start doing, you have two choices: KVM and QEMU. KVM is the userspace host and enables the kernel to access the virtualisations of the CPU. QEMU is the userspace utility that thanks to it can emulate virtual hardware for many architectures like Arm, i86/32 and MIPS, and we've already talked about emulation and various architectures so that the actual amount of emulation QEMU has to be reduced to almost zero.
QEMU is a command-line tool, as in our way. Using assistance or building CLIs we won't let you do Using QEMU is just a matter of:

# ## VirtIO

We mentioned that virtIO in the QEMU/KVM journey is to emulate hardware, and we're glad to point out that this is a real advantage. So let's talk about such things. It makes sense to tell the version of the OS that it is, and that the hardware it can see or not. In this way we modify the OS (or in this case its drivers) and have the hypervisor present as a paravirtual controller. The framework KVM uses theses for its paravirtualisation of block devices, video devices, network devices and the increasingly named balloon device (memory management). These drivers need to be installed on the guest, but have been part of the kernel for a long time - so for Linux no guest is required

```
$ qemu-system-x86_64 -qcow2,if -v virtio-net nic,model-virtio -m -enable
```

if, in the guest you run

you will see your VM now has a virtio-powered video. Ethernet and SCSI disk. In order to take advantage of the improved improved video device you'll need to install a desktop environment where you can do:

```
$ sudo apt install ubuntu-gnome-
```

![](bbox=[0.545, 0.665, 0.952, 0.815])

QEMU doesn't look like that, but it's incredibly powerful and enables you to perform destructive actions with no risk of