
# Chapter 14 • Attacking and Defending Unix

relatively easy to difficult. There is research under way into modifying running kernels that do not permit the loading of modules, and it is merely a matter of time and research before this method becomes the widely accepted means of placing a backdoor on a system. However, host-based IDSs combined with kernels that do not permit the loading of modules effectively raises the bar over the level of 97 percent of intruders.

The majority of operating systems that include host-based intrusion detection are free operating systems. One example of this is EnGarde Linux (www.engardelinux.com). EnGarde Secure Linux provides the Tripwire host-based IDS by default, and also allows management of the IDS via a Web interface. Tripwire is the most prominent of host-based IDSs.

Host-based IDSs must be installed immediately after the system has been installed, patched, and configured. Typically, an IDS such as Tripwire requires the storing of checksums on media that is read-only and can never be written to. Therefore, planning should be made to include a means of mounting and reading from read-only media such as a CD-ROM.

It is generally good practice to install host-based IDSs. It is not only good for system security, but also courteous to staff, both present and future. Inevitably, people will move on to a new job. When this happens, somebody will inevitably have to fill the position that has been vacated. A host-based IDS will help future staff establish the integrity of the host.

# Securing Inherited Systems

When an administrator or security person starts a new job, he inherits lots of responsibilities, including responsibility for systems that were designed and implemented long before their arrival. The integrity and the level of trust of these systems are unknown.

Therefore, the process of determining the level of trust of inherited systems and the security of inherited systems begins. Often, it is impossible to establish any level of trust with inherited systems, and one must ultimately reinstall the operating system and, if possible, the IDS. However, this is not always possible, or even feasible. Business requirements must be evaluated in the context of system security.

# Evaluating Inherited Systems

A number of steps are required to evaluate inherited systems and determine the integrity of the host. Typically this starts with the integrity checking of the host using a host-based IDS, if available. As previously mentioned, this may not always

![](img/729efc56f204a2ebffb8295c3a2dfdfb_790_0.png)

be available. In this circumstance, the best you can hope to establish the integrity of the host with the smallest margin of error possible.

Evaluating the integrity of the host typically involves examining the system for backdoors. After the host has been evaluated, identifying any risks to security is your next order of business. Finally, create a plan to maintain the security of the host after the integrity and risks have been established. We'll discuss how to do this in the following sections.

# Gathering System Information

The evaluation of host integrity on an inherited system is like a verification of the complete integrity of the host, and more about establishing the level of trust of the host. Host integrity is never 100 percent, as another person previously had complete administrative access to the system. Therefore, the idea of host integrity is to ensure, as much as possible, that the system is in fact trustworthy.

Evaluating the integrity of a host usually starting with gathering information about the host. This information usually includes:

- Operating system
- Kernel type (modular or static)
- Installation date (gathered from the maintenance logbook)
- Installed software
- Patch level (from the maintenance logbook, or system itself)
- Type of host-based IDS, if any, and status of last run
- Operational requirements of the host (uptime, etc)

You can glean a number of things from the operating system, such as the availability of tools to perform integrity checks. There are a number of free projects available on the Internet that produce integrity checking tools (however these tools may not work with some operating systems). This may give you an idea of how resource-intensive the verification of integrity will be. This also give you insight into whether or not there are other resources available, such as checksum databases for a specific operating system.

The kernel type will help in realizing the full extent of the integrity of the host. By knowing what type of kernel the system uses, you will have an idea of whether you can trust the lowest level of the operating system, or whether the operating system itself may be apt to produce bad information. In

![](img/729efc56f204a2ebffb8295c3a2dfdfb_791_0.png)

this regard, this will give you an idea of how you need to go about verifying the integrity of the host (whether you can keep the host running, or whether you will need to mount the disk on another system to audit the host).

The installation date of a system is an important fact to know, although it is not critical. Knowing the installation date of a system gives you a good idea of what threats the system has faced since it was initially put in production (such as vulnerabilities, worms, and public exploits).

Installed software is another factor that must be considered. The operating system itself may be secure, and well maintained. However, third-party applications installed on the host may not be in good shape and may present a threat to the integrity of the system. Gathering this information will help you rate the integrity of the host and will be necessary in the securing of the system.

The patch level of the host is necessary in determining which known the system currently faces. This information can be misleading, and you must pay careful attention to a number of factors that come into play. One factor is the system may still have a vulnerability present for which there is no patch available. Another reason is that the system may not have a patch installed for a vulnerability in a particular software package, the vulnerable package may not be installed. This is an example of when a system maintenance logbook proves its worth. From the entry in the logbook, you have an idea of when the patch was installed. With a little work, you can determine when the vulnerability was first disclosed. This gives you an idea of how long an exposure to a particular vulnerability existed before it was patched.

The type of host-based IDS will also help you gather a better understanding of how trustworthy the information you gain from integrity checking is going to be. Knowing this information gives you an idea of the limitations of the IDS. It also helps you know whether or not the data used by the IDS is error-prone, or untrustworthy itself.

Finally, you should know the operational requirements of the system. The operational requirements can be defined as the requirements of the system to meet business goals. This includes the uptime required of the system, such as whether it must be accessible during business hours, or 24/7. Finally, you should know any contingency plans in place, especially in the event that you blow up the host while performing integrity checks, or discover that the system is in fact compromised, and be taken offline.

# Evaluating System Integrity

With the information you have gathered about the system, you can easily make decisions about what steps are necessary to determine the integrity of the host. You can search the Web for automated integrity checking tools or any other available tools that can make your job easier. However, you must first make the decision as to what requirements are necessary.

# The Kernel

A system that uses a modular kernel must always be suspect, even with a host-based IDS in place. Therefore, to establish the integrity of the system, you must use another system that is trusted to verify the host. This process involves mounting the file system of the untrusted host and auditing the contents of the drive. Examine the module loading configuration and determine which modules loaded by the system are in fact valid.

Programs exist to check for the existence of kernel modules and other backdoors. One such program is `chrootkit`. Chrootkit works by checking modules loaded in the kernel, processes in the /proc file system, the promiscuity of net-interfaces, and other tests. While programs as chrootkit are an excellent resource in detecting the presence of various rootkits and backdoors, the program is essentially in a race with attackers that may design a backdoor based on the weaknesses of the program. Therefore, programs as this can only be trusted to some extent.

# Program Integrity and Type of Host-Based IDS

Validating key programs installed on the host involves the use of cryptographic software and patience. The process is roughly the same no matter which method is used: Get MD5 sums of the binaries, and compare them against known, good MD5 sums. This involves the use of host-based intrusion detection system, if available. Knowing the type of host-based IDS installed on the system is convenient, as it allows you to make adequate preparations prior to entering the verification process.

Systems with a host-based IDS installed are easy to verify. The binary used for the host-based IDS is not trusted, therefore you must use the database file of the
