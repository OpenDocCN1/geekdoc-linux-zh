# VirtualBox

The kitchen-sink approach to features wins it many fans

![](bbox=[0.08, 0.25, 0.47, 0.41])

+   * The virtual networking infrastructure that's available in VirtualBox is one of the virtualisation' most interesting features

# Usability

VirtualBox employs a brief wizard to get users to customise the essential elements of a VM. Post-creation, you can either power it on or tweak the settings for its virtual hardware. The VM settings window houses useful options such as the ability to manually select a paravirtualisation interface for the VM.

# Advanced features

The app is chock-full of features. It can take snapshots of VMs and clone them and you can also import and export virtual appliances with relative ease. VirtualBox can also do port forwarding to let you run servers inside a VM. However, for some of its advanced features, like disk image encryption, you need to rely on the proprietary extensions module.

# Native hardware support

Another area where VirtualBox shines. It supports pass-through mode for SSDs and optical disks and is one of the only options that lets apps inside the VM use the host's 3D hardware. Its USB support lets you access all kinds of peripherals on the host and you can run VMs with high resolutions and spread them over multiple monitors connected to the host.

# Integration with the host OS

With VirtualBox, you can share clipboard and folders that can be configured to mount automatically. Off note is its Seamless Mode in which you can run virtualised applications alongside the ones on the host desktop.

# Overall

With its unique blend of advanced features and user-friendliness, VirtualBox offers enough to satisfy both experienced and inexperienced users alike.

8

# Virt-manager

It's tough at the top, but Red Hat's offering has much to recommend it

![](bbox=[0.55, 0.25, 0.93, 0.41])

+   * While virt-manager primarily creates KVM virtual machines, it can also manage Xen and LXC containers

# Usability

Virt-manager (or Virtual Machine Manager to give it its full title) uses a fairly intuitive wizard to create new virtual machines. The application covers enough ground to give the system tweakers ample room to personalise their VMs while using reasonable defaults to help the first timer sail through. The application's main interface displays a list of all the VMs and if one is running, it'll also display its live resource utilisation statistics.

# Advanced features

The Virt-manager application offers fine-grained control over some pieces of hardware, which will appeal to advanced users. It can clone VMs and migrate them from one host to another and you can also import a QEMU copy-on-write image.

# Native hardware support

Inside the VM, sound works out of the box and the display can scale to full-screen. The virtualisation also supports the ability to attach USB devices including removable drives, webcams and Bluetooth devices connected to the host, and all work inside the guest seamlessly without any issues.

# Integration with the host OS

You can copy and paste text between the VM and the host once you've installed spice-vdagent on the host as well as inside the guest VM. However, you can't move files in the same fashion and unlike VirtualBox, there are no extra guest additions or similar extensions that will enable such features.

# Overall

Virt-manager has all the commonly used features you'd want. These are exposed via an intuitive interface that make the app a charm to use, irrespective of the skill level of the user.

7