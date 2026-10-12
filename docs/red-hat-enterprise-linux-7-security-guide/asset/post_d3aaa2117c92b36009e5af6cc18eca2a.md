
## WARNING

Protecting access to single user mode with a password by editing the SINGLE parameter in the `/etc/sysconfig/init` file is not recommended. An attacker can bypass the password by specifying a custom initial command (using the `init=` parameter) on the kernel command line in GRUB 2. It is recommended to password-protect the GRUB 2 boot loader, as described in the Protecting GRUB 2 with a Password chapter in *Red Hat Enterprise Linux 7 System Administrator's Guide*.

- **2. Preventing Access to the GRUB 2 Console** — If the machine uses GRUB 2 as its boot loader, an attacker can use the GRUB 2 editor interface to change its configuration or to gather information using the `cat` command.
- **3. Preventing Access to Insecure Operating Systems** — If it is a dual-boot system, an attacker can select an operating system at boot time, for example DOS, which ignores access controls and file permissions.

Red Hat Enterprise Linux 7 includes the GRUB 2 boot loader on the Intel 64 and AMD64 platform. For a detailed look at GRUB 2, see the Working With the GRUB 2 Boot Loader chapter in *Red Hat Enterprise Linux 7 System Administrator's Guide*.

### 4.2.5.1. Disabling Interactive Startup

Pressing the `i` key at the beginning of the boot sequence allows you to start up your system interactively. During an interactive startup, the system prompts you to start up each service one by one. However, this may allow an attacker who gains physical access to your system to disable the security-related services and gain access to the system.

To prevent users from starting up the system interactively, as root, disable the PROMPT parameter in the `/etc/sysconfig/init` file:

```
PROMPT=no
```

## 4.2.6. Protecting Hard and Symbolic Links

To prevent malicious users from exploiting potential vulnerabilities caused by unprotected hard and symbolic links, Red Hat Enterprise Linux 7 includes a feature that only allows links to be created or followed provided certain conditions are met.

In case of hard links, one of the following needs to be true:

- The user owns the file to which they link.
- The user already has read and write access to the file to which they link.

In case of symbolic links, processes are only permitted to follow links when outside of world-writable directories with sticky bits, or one of the following needs to be true:

- The process following the symbolic link is the owner of the symbolic link.
- The owner of the directory is the same as the owner of the symbolic link.

This protection is turned on by default. It is controlled by the following options in the `/usr/lib/sysctl.d/50-default.conf` file:

```
fs.protected_hardlinks = 1
fs.protected_symlinks = 1
```

To override the default settings and disable the protection, create a new configuration file called, for example, `51-no-protect-links.conf` in the `/etc/sysctl.d/` directory with the following content:

```
fs.protected_hardlinks = 0
fs.protected_symlinks = 0
```

## NOTE

Note that in order to override the default system settings, the new configuration file needs to have the `.conf` extension, and it needs to be read *after* the default system file (the files are read in lexicographic order, therefore settings contained in a file with a higher number at the beginning of the file name take precedence).

See the `sysctl.d(5)` manual page for more detailed information about the configuration of kernel parameters at boot using the sysctl mechanism.

# 4.3. SECURING SERVICES

While user access to administrative controls is an important issue for system administrators within an organization, monitoring which network services are active is of paramount importance to anyone who administers and operates a Linux system.

Many services under Red Hat Enterprise Linux 7 are network servers. If a network service is running on a machine, then a server application (called a *daemon*), is listening for connections on one or more network ports. Each of these servers should be treated as a potential avenue of attack.

## 4.3.1. Risks To Services

Network services can pose many risks for Linux systems. Below is a list of some of the primary issues:

- **Denial of Service Attacks (DoS)** – By flooding a service with requests, a denial of service attack can render a system unusable as it tries to log and answer each request.
- **Distributed Denial of Service Attack (DDoS)** – A type of DoS attack which uses multiple compromised machines (often numbering in the thousands or more) to direct a coordinated attack on a service, flooding it with requests and making it unusable.
- **Script Vulnerability Attacks** – If a server is using scripts to execute server-side actions, as Web servers commonly do, an attacker can target improperly written scripts. These script vulnerability attacks can lead to a buffer overflow condition or allow the attacker to alter files on the system.
- **Buffer Overflow Attacks** – Services that want to listen on ports 1 through 1023 must start either with administrative privileges or the CAP_NET_BIND_SERVICE capability needs to be set for them. Once a process is bound to a port and is listening on it, the privileges or the capability are often dropped. If the privileges or the capability are not dropped, and the application has an exploitable buffer overflow, an attacker could gain access to the system as the user running the daemon. Because exploitable buffer overflows exist, crackers use automated tools to identify systems with vulnerabilities, and once they have gained access, they use automated rootkits to maintain their access to the system.

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_45_0.png)

## NOTE

The threat of buffer overflow vulnerabilities is mitigated in Red Hat Enterprise Linux 7 by ExecShield, an executable memory segmentation and protection technology supported by x86-compatible uni- and multi-processor kernels. ExecShield reduces the risk of buffer overflow by separating virtual memory into executable and non-executable segments. Any program code that tries to execute outside of the executable segment (such as malicious code injected from a buffer overflow exploit) triggers a segmentation fault and terminates.

ExecShield also includes support for No eXecute (NX) technology on AMD64 platforms and Intel® 64 systems. These technologies work in conjunction with ExecShield to prevent malicious code from running in the executable portion of virtual memory with a granularity of 4KB of executable code, lowering the risk of attack from buffer overflow exploits.

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_45_1.png)

## IMPORTANT

To limit exposure to attacks over the network, all services that are unused should be turned off.

## 4.3.2. Identifying and Configuring Services

To enhance security, most network services installed with Red Hat Enterprise Linux 7 are turned off by default. There are, however, some notable exceptions:

- **cups** – The default print server for Red Hat Enterprise Linux 7.
- **cups-lpd** – An alternative print server.
- **xinetd** – A super server that controls connections to a range of subordinate servers, such as gssftpd and telnet.
- **sshd** – The OpenSSH server, which is a secure replacement for Telnet.

When determining whether to leave these services running, it is best to use common sense and avoid taking any risks. For example, if a printer is not available, do not leave cups running. The same is true for portreserve. If you do not mount NFSv3 volumes or use NIS (the ypsbind service), then rpcbind should be disabled. Checking which network services are available to start at boot time is not sufficient. It is recommended to also check which ports are open and listening. Refer to Section 4.4.2, “Verifying Which Ports Are Listening” for more information.

## 4.3.3. Insecure Services

Potentially, any network service is insecure. This is why turning off unused services is so important.

Exploits for services are routinely revealed and patched, making it very important to regularly update packages associated with any network service. See Chapter 3, *Keeping Your System Up-to-Date* for more information.

Some network protocols are inherently more insecure than others. These include any services that:

- **Transmit Usernames and Passwords Over a Network Unencrypted** – Many older protocols, such as Telnet and FTP, do not encrypt the authentication session and should be avoided whenever possible.
- **Transmit Sensitive Data Over a Network Unencrypted** – Many protocols transmit data over the network unencrypted. These protocols include Telnet, FTP, HTTP, and SMTP. Many network file systems, such as NFS and SMB, also transmit information over the network unencrypted. It is the user's responsibility when using these protocols to limit what type of data is transmitted.

Examples of inherently insecure services include **rlogin**, **rsh**, **telnet**, and **vsftpd**.

All remote login and shell programs (**rlogin**, **rsh**, and **telnet**) should be avoided in favor of **SSH**. See *Section 4.3.11,* “Securing SSH” for more information about **sshd**.

**FTP** is not as inherently dangerous to the security of the system as remote shells, but **FTP** servers must be carefully configured and monitored to avoid problems. See *Section 4.3.9,* “Securing FTP” for more information about securing FTP servers.

Services that should be carefully implemented and behind a firewall include:

- auth
- nfs-server
- smb and nbm (Samba)
- yppasswdd
- yperv
- ypfxrd

More information on securing network services is available in *Section 4.4,* “Securing Network Access” .

## 4.3.4. Securing rpcbind

The **rpcbind** service is a dynamic port assignment daemon for RPC services such as NIS and NFS. It has weak authentication mechanisms and has the ability to assign a wide range of ports for the services it controls. For these reasons, it is difficult to secure.

> **NOTE**
>
> Securing **rpcbind** only affects NFSv2 and NFSv3 implementations, since NFSv4 no longer requires it. If you plan to implement an NFSv2 or NFSv3 server, then **rpcbind** is required, and the following section applies.

If running RPC services, follow these basic rules.
