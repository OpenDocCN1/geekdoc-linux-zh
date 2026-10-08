# 33

CHAPTER

# Kernel Administration: Virtualization

The kernel is the operating system, performing core tasks such as managing memory and disk access, as well as interfacing with the hardware that makes up your system. For example, the kernel makes possible such standard Linux features as multitasking and multiuser support. It also handles communications with devices like your CD-ROM or hard disk. Users send requests for access to these devices through the kernel, which then handles the lower-level task of actually sending appropriate instructions to a device. Given the great variety of devices available, the kind of devices connected to a Linux system will vary. When Linux is installed, the kernel is appropriately configured for your connected devices. However, if you add a new device, you may have to enable support for it in the kernel. This involves reconfiguring the existing kernel to support the new device through a procedure that is often referred to as building or compiling the kernel. In addition, new versions of the kernel are continuously made available that provide improved support for your devices, as well as support for new features and increased reliability for a smoother-running system. You can download, compile, and install these new versions on your system.

# Kernel Versions

The version number for a Linux kernel consists of four segments: the major, minor, revision, and security/bug fix numbers. The *major number* increments with major changes in the kernel. This is rarely changed. The *minor number* indicates a major revision of the kernel. The revision number is used for supporting new features. The security/bug number is used for security and bug fixes. New development versions will first appear as release candidates, which will have an rc in the name. As bugs are discovered and corrected, and as new features are introduced, new revisions of a kernel are released. For example, kernel 2.6.21.7 has a major number of 2 and a minor number of 6, with a revision number of 20, and a securit/bug fix number of 7. The release candidate version would have a name like 2.6.22-rc7.

Distributions often add another number that refers to a specific set of patches applied to the kernel, as well as a distribution initial. For example, for Fedora, the kernel is 2.6.21-1.3116.f7, where 3116 is the patch number and b refers to the Fedora 7 distribution.