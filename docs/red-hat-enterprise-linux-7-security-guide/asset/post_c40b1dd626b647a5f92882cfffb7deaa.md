
| Event Type | Explanation |
| :--- | :--- |
| **DEV_ALLOC** | Triggered when a device is allocated. |
| **DEV_DEALLOC** | Triggered when a device is deallocated. |
| **EOE** | Triggered to record the end of a multi-record event. |
| **EXECVE** | Triggered to record arguments of the `execve(2)` system call. |
| **FD_PAIR** | Triggered to record the use of the `pipe` and `socketpair` system calls. |
| **FEATURE_CHANGE** | Triggered when an Audit feature changed value. |
| **FS_RELABEL** | Triggered when a file system relabel operation is detected. |
| **GRP_AUTH** | Triggered when a group password is used to authenticate against a user-space group. |
| **GRP_CHAUTHTOK** | Triggered when a group account password or PIN is modified. |
| **GRP_MGMT** | Triggered to record user-space group account attribute modification. |
| **INTEGRITY_DATA** [b] | Triggered to record a data integrity verification event run by the kernel. |
| **INTEGRITY_HASH** [b] | Triggered to record a hash type integrity verification event run by the kernel. |
| **INTEGRITY_METADATA** [b] | Triggered to record a metadata integrity verification event run by the kernel. |
| **INTEGRITY_PCR** [b] | Triggered to record Platform Configuration Register (PCR) invalidation messages. |
| **INTEGRITY_RULE** [b] | Triggered to record a policy rule. |
| **INTEGRITY_STATUS** [b] | Triggered to record the status of integrity verification. |
| **IPC** | Triggered to record information about a Inter-Process Communication object referenced by a system call. |
| **IPC_SET_PERM** | Triggered to record information about new values set by an `IPC_SET` control operation on an IPC object. |
| **KERN_MODULE** | Triggered to record a kernel module name on load or unload. |
| **KERNEL** | Triggered to record the initialization of the Audit system. |
| **KERNEL_OTHER** | Triggered to record information from third-party kernel modules. |
| **LABEL_LEVEL_CHANGE** | Triggered when an object's level label is modified. |
| **LABEL_OVERRIDE** | Triggered when an administrator overrides an object's level label. |
| **LOGIN** | Triggered to record relevant login information when a user logs in to access the system. |
| **MAC_CHECK** | Triggered when a user space MAC (Mandatory Access Control) decision is made. |
| **MAC_CIPSOV4_ADD** | Triggered when a Commercial Internet Protocol Security Option (CIPSO) user adds a new Domain of Interpretation (DOI). Adding DOIs is a part of the packet labeling capabilities of the kernel provided by NetLabel. |
| **MAC_CIPSOV4_DEL** | Triggered when a CIPSO user deletes an existing DOI. Adding DOIs is a part of the packet labeling capabilities of the kernel provided by NetLabel. |
| **MAC_CONFIG_CHANGE** | Triggered when an SELinux Boolean value is changed. |
| **MAC_IPSEC_EVENT** | Triggered to record information about an IPSec event, when one is detected, or when the IPSec configuration changes. |
| **MAC_MAP_ADD** | Triggered when a new Linux Security Module (LSM) domain mapping is added. LSM domain mapping is a part of the packet labeling capabilities of the kernel provided by NetLabel. |
| **MAC_MAP_DEL** | Triggered when an existing LSM domain mapping is deleted. LSM domain mapping is a part of the packet labeling capabilities of the kernel provided by NetLabel. |
| **MAC_POLICY_LOAD** | Triggered when a SELinux policy file is loaded. |
| **MAC_STATUS** | Triggered when the SELinux mode (enforcing, permissive, off) is changed. |
| **MAC_UNLBL_ALLOW** | Triggered when unlabeled traffic is allowed when using the packet labeling capabilities of the kernel provided by NetLabel. |
| **MAC_UNLBL_STCADD** | Triggered when a static label is added when using the packet labeling capabilities of the kernel provided by NetLabel. |
| **MAC_UNLBL_STCDEL** | Triggered when a static label is deleted when using the packet labeling capabilities of the kernel provided by NetLabel. |
| **MMAP** | Triggered to record a file descriptor and flags of the `mmap(2)` system call. |
| **MQ_GETSETATTR** | Triggered to record the `mq_getattr(3)` and `mq_setattr(3)` message queue attributes. |
| **MQ_NOTIFY** | Triggered to record arguments of the `mq_notify(3)` system call. |
| **MQ_OPEN** | Triggered to record arguments of the `mq_open(3)` system call. |
| **MQ_SENDRECV** | Triggered to record arguments of the `mq_send(3)` and `mq_receive(3)` system calls. |
| **NETFILTER_CFG** | Triggered when Netfilter chain modifications are detected. |
| **NETFILTER_PKT** | Triggered to record packets traversing Netfilter chains. |
| **OBJ_PID** | Triggered to record information about a process to which a signal is sent. |
| **PATH** | Triggered to record file name path information. |
| **PROCTITLE** | Gives the full command-line that triggered this Audit event, triggered by a system call to the kernel. |
| **RESP_ACCT_LOCK**$^{[c]}$ | Triggered when a user account is locked. |
| **RESP_ACCT_LOCK_TIME**$^{[c]}$ | Triggered when a user account is locked for a specified period of time. |
| **RESP_ACCT_REMOTE**$^{[c]}$ | Triggered when a user account is locked from a remote session. |
| **RESP_ACCT_UNLOCK_TIME**$^{[c]}$ | Triggered when a user account is unlocked after a configured period of time. |
| **RESP_ALERT**$^{[c]}$ | Triggered when an alert email is sent. |
| **RESP_ANOMALY**$^{[c]}$ | Triggered when an anomaly was not acted upon. |
| **RESP_EXEC**$^{[c]}$ | Triggered when an intrusion detection program responds to a threat originating from the execution of a program. |
| **RESP_HALT**$^{[c]}$ | Triggered when the system is shut down. |
| **RESP_KILL_PROC**$^{[c]}$ | Triggered when a process is terminated. |
| **RESP_SEBOOL**$^{[c]}$ | Triggered when an SELinux Boolean value is set. |
| **RESP_SINGLE**$^{[c]}$ | Triggered when the system is put into single-user mode. |
| **RESP_TERM_ACCESS**$^{[c]}$ | Triggered when a session is terminated. |
| **RESP_TERM_LOCK**$^{[c]}$ | Triggered when a terminal is locked. |
| **ROLE_ASSIGN** | Triggered when an administrator assigns a user to an SELinux role. |
| **ROLE_MODIFY** | Triggered when an administrator modifies an SELinux role. |
| **ROLE_REMOVE** | Triggered when an administrator removes a user from an SELinux role. |
| **SECCOMP** | Triggered when a SECUre COMPuting event is detected. |
| **SELINUX_ERR** | Triggered when an internal SELinux error is detected. |
| **SERVICE_START** | Triggered when a service is started. |
| **SERVICE_STOP** | Triggered when a service is stopped. |
| **SOCKADDR** | Triggered to record a socket address. |
| **SOCKETCALL** | Triggered to record arguments of the `sys_socketcall` system call (used to multiplex many socket-related system calls). |
| **SYSCALL** | Triggered to record a system call to the kernel. |
| **SYSTEM_BOOT** | Triggered when the system is booted up. |
| **SYSTEM_RUNLEVEL** | Triggered when the system's run level is changed. |
| **SYSTEM_SHUTDOWN** | Triggered when the system is shut down. |
| **TEST** | Triggered to record the success value of a test message. |
| **TRUSTED_APP** | The record of this type can be used by third party application that require auditing. |
| **TTY** | Triggered when TTY input was sent to an administrative process. |
| **USER_ACCT** | Triggered when a user-space user authorization attempt is detected. |
| **USER_AUTH** | Triggered when a user-space user authentication attempt is detected. |
| **USER_AVC** | Triggered when a user space AVC message is generated. |
| **USER_CHAUTHTOK** | Triggered when a user account password or PIN is modified. |
| **USER_CMD** | Triggered when a user space shell command is executed. |
| **USER_END** | Triggered when a user space session is terminated. |
| **USER_ERR** | Triggered when a user account state error is detected. |
| **USER_LABELED_EXPORT** | Triggered when an object is exported with an SELinux label. |
| **USER_LOGIN** | Triggered when a user logs in. |
| **USER_LOGOUT** | Triggered when a user logs out. |
| **USER_MAC_POLICY_LOAD** | Triggered when a user space daemon loads an SELinux policy. |
| **USER_MGMT** | Triggered to record user space user account attribute modification. |
| **USER_ROLE_CHANGE** | Triggered when a user's SELinux role is changed. |
| **USER_SELINUX_ERR** | Triggered when a user space SELinux error is detected. |
| **USER_START** | Triggered when a user space session is started. |
| **USER_TTY** | Triggered when an explanatory message about TTY input to an administrative process is sent from user space. |
| **USER_UNLABELED_EXPORT** | Triggered when an object is exported without SELinux label. |
| **USER_CONFIG** | Triggered when a user space system configuration change is detected. |
| **VIRT_CONTROL** | Triggered when a virtual machine is started, paused, or stopped. |
| **VIRT_MACHINE_ID** | Triggered to record the binding of a label to a virtual machine. |
| **VIRT_RESOURCE** | Triggered to record resource assignment of a virtual machine. |
