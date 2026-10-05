+   Remote management and provisioning tools

# Modular structure of the operating system

The Linux kernel has, by design, a modular structure. This means that the kernel is not one monolithic binary. Instead, it consists of a central smaller kernel binary with various kernel modules. The kernel modules can be loaded when needed. Some of the modules have to be loaded at boot, because these need to read file systems or other peripheral hardware.

Not only is the kernel module, but the application framework around the kernel has a modular construction as well. The applications such scripting engines (Perl, PHP, and Python) or editors (gedit, and vi) are not integrated into the operating system and can be replaced by others or new versions or less independently.

The modular nature of Linux means that updates or patches only affect a small part of the system, for example, either a single application binary or a library within the application framework or a single kernel module. This modularity is the main reason that an update or a patch almost does not require a reboot on Linux.

# Update mechanism

The update mechanism for Linux does not need to be central to the system. What we mean by this is that updating or patching is not destructive to the system state (in other words, a reboot), it can be done while others applications are running. Unless the update or patch impacts the core kernel or a running application, it can be done online.

This means that the mechanism that checks for new updates can be scheduled regularly and can be allowed to implement the changes automatically.

# Inherent support for remote access

The Linux operating system has inherent remote access through TCP/IP, like UNIX operating systems. This is a really powerful tool for systems management, because all management tasks can be done remotely, and since the advent of the secure socket layer can be done securely using SSH.

Remote access to the client is useful for two types of administrative tasks:

+   Remote execution of administrative programs or scripts
Access to the client from a central location to give support on the client

# Remote execution

Remote execution is used to execute applications or scripts from a central location, for example, to force all clients to update a virus scanner or fetch

Chapter 2. The case for migration 35