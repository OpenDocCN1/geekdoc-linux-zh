# Evaluating System Integrity

With the information you have gathered about the system, you can easily make decisions about what steps are going to be necessary to determine the integrity of the system.You can search the Web for automated integrity checking tools or by any other available tools or information that can make your job easier. However, you must first make the decision as to what requirements are necessary.

# The Kernel

A system that uses a modular kernel must always be suspect, even with a host-based IDS in place. Therefore, to establish the integrity of the system, you must use another system that is trusted to verify the host. This process involves mounting the file system of the untrusted host and auditing the contents of the drive. Examine the module loading configuration and determine which kernel modules loaded by the system are in fact valid.

Programs exist to check for the existence of kernel modules and other backdoors. One such program is `chrootkit`. Chrootkit works by checking modules loaded in the kernel, processes in the /proc file system, the promiscuity of net-interfaces, and other tests. While programs as chrootkit are an excellent resource in detecting the presence of various rootkits and backdoors, the program is essentially in a race with attackers that may design a backdoor based on the weaknesses of the program. Therefore, programs as this can only be trusted to some extent.

Once the integrity of the kernel and modules loaded by the kernel has been verified, check the integrity of installed binaries on the host. This is preferably done with the file system mounted on the trusted host. If necessary, it can be done on the host audited, although additional steps are necessary.

# Program Integrity and Type of Host-Based IDS

Validating key programs installed on the host involves the use of cryptographic software and patience. The process is roughly the same no matter which method is used: Get MD5 sums of the binaries, and compare them against known, good MD5 sums. This involves the use of host-based intrusion detection system, if available. Knowing the type of host-based IDS installed on the system is convenient, as it allows you to make adequate preparations prior to entering the verification process.

Systems with a host-based IDS installed are easy to verify. The binary used for the host-based IDS is not trusted, therefore you must use the database file of the