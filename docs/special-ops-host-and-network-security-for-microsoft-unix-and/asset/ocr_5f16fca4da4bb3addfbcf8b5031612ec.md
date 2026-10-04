# Untrusted Local Access

Hosts that require granting untrusted users access to the system have special requirements. An untrusted user can be defined as one that is not administrative staff, or does not have legitimate administrative access to the host. This type of configuration typically occurs in servers designed for shell users.

Restrictive environments in combination with multiple layers of access control are required to protect hosts. Typically, a combination of pseudo-environments such as virtual machines or chroot environments are used with other items as restricted shells, file-system level access controls, and other utilities. The decision to support this type of server should be made during the design phase and the restrictive environment to be used for this should already be planned. During post-installation configuration, additional layers of access control should be applied to limit the impact on hosts in the event that the environment is circumvented.

# Kernel Security

A system is only as secure as the weakest component. Therefore, it is necessary to secure the system from the lowest level to the highest. This includes making kernel configuration changes to enable additional security features for various parts of the system such as networking, and making the kernel itself resistant to attack.

Kernel modules are a convenient feature of modern Unix operating systems. A module can be plugged into and removed from a running kernel to provide enhanced functionality when needed, and can lighten the load on system resources when not needed. However, the functionality of kernel modules can also be abused.

Kernel modules are, for most part, the facto method of back-dooring a system. Modules replace or alter system calls from the kernel, and essentially force the kernel to lie to administrators at the lowest level within the system. When a kernel module has been loaded, it is impossible to trust the integrity of the system. Systems that supply the kernel source code and permit the rebuilding of the kernel without module support should have the kernel recompiled.

Kernels also typically offer features that provide enhanced security. For example, the Sun Solaris kernel has a plethora of network configuration options that provide additional security measures for the host and users. We will not detail these features here, but will give additional information about them when we discuss implementation-specific details.