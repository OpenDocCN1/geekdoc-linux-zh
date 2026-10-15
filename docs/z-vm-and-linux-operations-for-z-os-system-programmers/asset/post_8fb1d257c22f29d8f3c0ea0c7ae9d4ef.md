
improves security by not requiring the root password to be known by the automation software.

A special capability available with z/VM is **Logon By**. This function enables the system administrator to define a shared virtual machine. When the user enters the shared user ID, the user also provides his or her own user ID and password. In this way, an audit trail is maintained of who is actually logged into a shared user ID, and the problems inherent in sharing passwords are avoided.

Remote access protocols such as rexec, ftp, and nfs, all require the client to authenticate using a z/VM user ID and password. At no time does z/VM trust the claims of an authenticated client. When authenticated, the remote client has the same access rights as the user would have if he or she were logged into the system with a terminal session.

For network applications, z/VM provides a Kerberos server and the programming interfaces that permit programs to take advantage of Kerberos authentication and encryption facilities. Note that the network application suite provided by IBM and the z/VM CP do not use Kerberos authentication. Although anonymous access to specific resources or to a virtual machine can be allowed by z/VM, such access must be explicitly enabled by the z/VM system administrator.

## 6.1.2 User authorization

When logged into the z/VM system, the virtual machine can access various types of resources within the z/VM system, including entire DASD volumes, minidisks, tape drives, network adapters, user files, system files, and so on. The security features of z/VM are designed so that a virtual machine can access only the resources specifically permitted to it.

Those permissions are given by the system administrator so that when the virtual machine is started, it automatically receives access to a certain resource, even if that virtual machine would otherwise be unable to access that resource. Alternatively, permissions are given dynamically by the system administrator or the owner of the resource.

Certain resources are accessible based on privilege class, others require additional authorization. The security facilities provided by z/VM can be enhanced according to any special or specific requirements for the customer’s environment by the addition of an External Security Manager.

Although privileged commands can be used to change a running z/VM system, the system administrator might choose to set system configuration options during system initialization. This is accomplished by updates to the CP system configuration file. Consequently, access to the system configuration file must be tightly controlled.

## 6.1.3 Intrusion detection

As an element of z/VM intrusion detection capabilities, if a logon is denied, the denial is delayed and a security journal entry is made when the number of denials exceeds an installation-defined maximum. When a second maximum is reached, logon to the user ID is disabled, an operator message is issued, and the terminal session is terminated.

Journaling is supported on z/VM. Virtual machine logons and linking to other virtual machine’s minidisks are detected and recorded. Using the recorded information, you can identify attempts to log on to a virtual machine or to link to minidisks that use invalid passwords.

The TCP/IP component of z/VM detects and reports a variety of network intrusions, including SYN flooding, Smurf attacks and the Ping o’ Death.

The z/VM Control Program (CP) defines and assigns virtual processors to the virtual machine. These virtual processors are matched to the physical or logical (if z/VM is running in a logical partition) processors available to the CP. If the operating system running in the virtual machine is capable of using multiple processors, it will dispatch its workload on its virtual processors as though it were running in a dedicated hardware environment. This capability can be extremely useful to test a guest operating system in a multiprocessor mode, even on a uniprocessor system.

## 6.1.4 Virtual processors security

The CP handles dispatching the virtual processors on the available real processors. A real processor can either be dedicated to a single virtual machine or shared among multiple virtual machines. Bear in mind that the CP handles only the processors it controls, so if z/VM is running in an LPAR, the logical processors might in fact be shared with other LPARs.

So, we have virtual machines dispatching their work on one or more virtual processors, which are mapped to one or more logical processors, which can be mapped yet again to one or more physical processors. Do not be concerned because there is no significant security risk if the virtual, logical, or physical processor configuration is changed, or if work is dispatched on different physical processors. The state of a processor is preserved for one virtual machine and restored for another by the z/VM Control Program just as PR/SM™ does for
