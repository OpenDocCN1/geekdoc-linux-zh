z/VM" on page 14, the concept of a z/VM user maps to a virtual machine. So, the AUTOLOG1 virtual machine is responsible for starting up other virtual machines (logging on other users) as soon as the z/VM IPL finishes. This is usually done to bring up the TCP/IP virtual machine, for example.

> Note: If the noautolog parameter is not specified when z/VM is loaded (IPL), the AUTOLOG1 virtual machine is started. Because this virtual machine IPLs CMS, the PROFILE EXEC that is found on its A disk is run. This is analogous to the /etc/profile file on Linux and the autoexec.bat file on DOS systems.

> z/OS analogy: The tasks performed by the z/VM AUTOLOG1 user are similar to using START statements in members IEACMDxx and COMMNDxx in the SYS1.PARMLIB concatenation

# The TCPIP user

In z/OS, the TCP/IP stack is managed by the z/OS Communications Server in a separate address space. In z/VM, however, the stack is managed by a virtual machine: the TCPIP virtual machine (defined as the TCPIP user).

# 4.2.4 Dealing with disks

A file hierarchy is run in CMS when a z/VM user logs into the system. It is a different hierarchy than the one used by Linux or z/OS. In fact, there is no hierarchy in CMS, but it does have the triplets concept of file name, file type and file mode. Every file name is formed by these three components, which are described in the following list. You can think of this file system as a flat file system (or sequential) in which you have only one level.

+   - The first parameter, the file name, should be familiar to most users because it is just the name of the file. In CMS, file names are limited to eight characters in length and are not case-sensitive.
+   - The second parameter, file type, is analogous to the file extension of systems such as Linux. In CMS, file types are also limited to 8 characters in length and are not case-sensitive. In an analogy, the file name and file type together form something similar to the z/OS filename.extension (with a space instead of a dot between them) file naming convention of other systems.
+   - The third parameter, the file mode, specifies where the file is located, that is, on which disk mapping it resides. The file mode is one character long and is limited to the characters A-Z. The file mode is what makes the whole filesystem a flat universe because you are limited to having 26 simultaneous places to put your files.