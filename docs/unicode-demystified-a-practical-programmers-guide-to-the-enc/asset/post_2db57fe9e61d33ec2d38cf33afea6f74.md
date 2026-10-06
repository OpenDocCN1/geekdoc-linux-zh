
# POSIX.3

The POSIX standards developers recognized early in the process that testing systems for conformance to the standards was going to be essential. In the past, standards efforts have suffered from lack of appropriately specified conformance tests or from conflicting standards with different measures of conformance. The POSIX.3 standard specifies general principles for test suites to measure conformance to POSIX standards. A set of assertions (individual items to be tested) is developed for each standard. For POSIX.1, a test methods with more than 2,400 assertions has been adopted as POSIX.3.1. For POSIX.2, a test standards contains almost 10,000 assertions.

GNU/Linux users who are involved in testing or procuring systems that must conform to standards need to be familiar with POSIX.3 and its associated test methods standards. For other GNU/Linux users, these standards have little importance.

# POSIX.4

The POSIX.4 standard, an addition to or modification of the POSIX.1 standard, describes C language interfaces for real-time applications. The standard defines real time as "the ability of the operating system to provide a required level of service in a bounded response time." Real-time systems have historically been implemented as stand-alone systems controlling processes or machines or as embedded systems (such as inside a microwave oven). However, there has always been a need for combined and real-time systems, and the UNIX system has served as the base for many implementations of real-time facilities.

The facilities specified in POSIX.4 are those commonly used by real-time applications, such as semaphores, timers, interprocess communication, shared memory, and so on. Although a few of these and related facilities have been implemented in various UNIX systems, there was no well-established and widely accepted set of UNIX real-time interfaces. The routines specified in POSIX.4 are largely the invention of the POSIX.4 committee and have already been implemented on a number of UNIX systems.

POSIX.4 is structured as a collection of optional extensions to POSIX.1. Thus a system can claim conformance to some parts of the standard and not others but must claim conformance to POSIX.1. This has been a subject of some controversy, as many real-time applications, particularly for embedded systems, do not need the support of an operating system with all the POSIX.1 machinery. GNU/Linux supports some subset of the POSIX.1b interfaces. These interfaces include memory locking (the ability of a process with privileges to lock itself in memory), some portion of synchronous I/O, and multiple selectors. There is considerable interest within the GNU/Linux community in providing the remaining POSIX.1b interfaces.

Most real-time applications have traditionally been implemented as sets of operating, closely coordinated processes. In many cases this cooperation extends to the use of shared data, and one convenient way to do this is to use multiple threads of control in a single process. Support for threads allows a single process to have multiple execution paths active at once, and—on hardware with multiple processors—to execute those paths simultaneously. The original POSIX real-time project included an attempt at standardizing threads. It was so recognized that this was sufficiently complicated to be a separate standard, and a new committee was formed. The resulting POSIX threads standard, POSIX.1c, was adopted in 1995.

# POSIX.5

POSIX.5, an Ada language version of POSIX.1, specifies Ada routines that provide the same functionality as the C routines of POSIX.1. The UNIX system itself is written in C, and C has always been the most widely used programming language on UNIX systems, but the Ada community has always been interested in the UNIX system and in providing a standard way for Ada programs to access UNIX system services. POSIX.5 provides that standard. In principle POSIX.5 provides the exact functionality provided by POSIX.1. This does not mean that there is a precise one-to-one correlation between the interfaces in POSIX.1 and POSIX.5 because differences in the languages make that correlation impossible.

The POSIX.5 working group is tracking changes to POSIX.1 and will keep the Ada version of the standard synchronized with the C version. The POSIX.20 working-group, which works in concert with POSIX.5, is developing an Ada language version of POSIX.4 and POSIX.4a; this will provide Ada programmers with the ability to use standard interfaces for real-time applications on the UNIX system and UNIX-like systems. This is important to the Ada community, as Ada has from its inception been used heavily in the development of real-time systems.

# Security

Since early in its development, the UNIX system has had a simple and relatively effective security paradigm. File access permissions are assigned according to three levels of granularity (owner, group, and other—page 118), and certain actions require privileges. The privileges are monolithic; that is, either a process has all the privileges that the system supports (such as adding users, changing the ownership of files, changing its user ID), or it has none. One user ID is reserved for a privileged user, Superuser.

For most ordinary purposes this paradigm works well.

An important feature of all the POSIX standards is that an abstract privilege model in which privileges are discrete. Each time a POSIX standard describes an action that requires some privilege, the phrase *appropriate privileges* is used. Thus POSIX.2 states that chmod can be used to change the mode of a file by the owner of the file or by a process with appropriate privileges. One model of these privileges is the Superuser model, but there can be others. Thus POSIX allows many security paradigms.

Areas under discussion include user interfaces, program interfaces, and structures to define higher levels of security. Some of the general issues are described following.

# Least Privilege

This is the idea that a process should have only the privileges that are absolutely necessary for its function. The monolithic nature of traditional UNIX system privileges is considered a security hazard. You may recall that in 1988, a worm traveled across the Internet, crippling computers around the world (page 1419). The worm exploited a feature of the sendmail program. Because sendmail has to write to all users' mail files, it must have some privileges. On a classical UNIX system, this means that it has all privileges, and the worm used this fact to acquire all privileges itself.

# Discretionary Access Controls (DACs)

These are additional access restrictions under the control of the creator of an object (such as a file). A typical DAC is an ACL (Access Control List), a list of user IDs permitted access to the file. This acts as an additional restriction to that imposed by the file's mode. See also "File Security" on page 1411.

# Mandatory Access Controls (MACs)

These are like security levels. An object is created at some level, not under the control of its creator, and can be accessed only by processes at the same or a higher level. The level can be determined by the process's user ID or by the nature of the process itself.

# Auditability Mechanism

This covers which types of objects or actions need to be audited and the mechanisms for keeping track of the audit trail. In all areas there is existing practice for UNIX systems; that is, you can find DACs, MACs, partitioned privilege, and audit mechanisms on secure UNIX systems. The goal of POSIX.1e is to standardize practices.

The POSIX.22 committee is addressing similar issues in a distributed environment. Clearly network security adds its own layer of difficulties, including file access on remotely mounted systems.

# Networks

A number of POSIX groups are working on various standards related to networks. The areas that need to be standardized occur at many different levels. Some are visible to users, some to application programs, and some only to the operating system.

The most visible network feature to a user is the availability of remote filesystems. There is a well-established existing practice for this on UNIX systems, via such packages as NFS (page 391) and RFS. The purpose of remote filesystems is to enable hierarchies on remote hosts to behave, to the extent, as if they were mounted on the local host. That is, the presence of the network should be transparent to the user and the user's programs. The POSIX.1 committee is charged with standardizing file access.

There is also existing practice for allowing programs on two different hosts to communicate with each other, much as pipes or FIFOs allow on the same host to communicate. In fact, there are at least two competing approaches: Berkeley sockets and the XTI interface from X/Open. The POSIX.1 committee is trying to resolve the differences between these approaches. Sockets and XTI are referred to as protocol-independent interfaces, as they are above the level of the network protocol, the convention that describes precisely how hosts on the network communicate.
