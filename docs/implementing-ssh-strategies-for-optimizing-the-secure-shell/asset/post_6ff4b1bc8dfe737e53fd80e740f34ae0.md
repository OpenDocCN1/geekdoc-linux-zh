
## Chapter 1 Introduction

introduced to it aside from a casual reference. Advanced users may want to skip to the next chapter. Specifically, this chapter discusses the following topics:

- Differences between SSH1 and SSH2
- Uses of SSH
- Client/server architecture for SSH
- SSH's Encryption Architecture
- Basic miscues with SSH
- Types of SSH clients/servers
- Basic setup of SSH
- Summary of SSH's optimal uses

### Differences between SSH1 and SSH2

SSH version 1 (SSH1) was the first iteration of SSH; however, SSH1 had several limitations, including the use of port forwarding, which led to the second iteration of SSH: SSH version 2 (SSH2). In addition to its limitations, SSH1 had several security issues associated with its cryptography, which also led to the establishment of SSH2.

The differences between SSH1 and SSH2 may seem minor to most end-users; however, the differences are quite significant. SSH1 and SSH2 are two different protocols. SSH2 was completely rewritten from scratch, giving it more security, performance, and flexibility than SSH1. Also, SSH1 and SSH2 encrypt communication differently, which mitigated several of the documented issues with SSH1's encryption methods. SSH1 is not being developed now, whereas SSH2 is becoming the standard when referring to SSH. There are still many implementations of SSH1, but the implementations are becoming fewer and more in favor of SSH2. For the purposes of this book, I do not refer to, use, or demonstrate the use of SSH1. I concentrate solely on the usage and optimization of SSH2. The following is a short list of the advantages of using SSH2 instead of SSH1:

- Significant improvements with security and speed
- Considerably greater flexibility with Secure File Transfer Protocol (SFTP)
- Interoperability with several different public key algorithms, including Diffie-Hellman (see http://www.rsasecurity.com/rsalabs/faq/3-6-1.html for more information on Diffie-Hellman)
- New architecture that requires far less code usage

### Various Uses of SSH

SSH can be used in a variety of ways, depending on your network environment and business requirements. The flexibility that SSH provides in any type of dynamic or static environment gives it a significant advantage over other utilities in the industry, both security-focused utilities, such as IPSEC, and nonsecurity-focused utilities, such as FTP. SSH can be used for multiple users with just a single process (daemon) or service running on the server, with most of the configuration required on the client side. During the course of this book, I explore the various uses of SSH; however, I take the better half of this chapter to describe the different uses of SSH to illustrate its full capabilities:

- Security
- Remote command execution
- Remote file transfer
- Remote network access
- Secure management
- Proxy services

### Security

The implementation of SSH in a trusted or nontrusted environment can protect against many of the security issues with Internet Protocol version 4 (IPv4). IPv4 has been plagued with security issues ranging from poor initial sequence numbers (ISN) in TCP header packets, which leads to session hijacking, to unauthenticated address resolution packets (ARP)s being distributed to the network. The use of SSH not only protects against the common LAN attacks described previously; it guards against the following types of attacks as well:

- **Spoofing of IP addresses.** A remote device, usually an operating system, can change its IP address and pretend to be a different source, usually a trusted source.
- **Data modification.** As data is passed through corporate networks and the Internet, any intermediary can modify the data while it is in transit.
- **ARP pollution.** This occurs when incorrect ARP packets to redirect and capture sensitive data are distributed.
- **Session hijacking.** This occurs when individuals guess or predict the ISN in TCP headers, gaining control of Telnet and RSH sessions.
- **Clear-text data.** This occurs when critical or sensitive clear-text data, such as usernames, passwords, and commands, is intercepted.

The preceding list is not exhaustive, as SSH can protect against many other attacks, which may be direct or indirect. Another reason SSH is so popular is its ability to protect against network sniffing on both Local Area Networks (LANs) and Wide Area Networks (WANs). That feature allows network administrators and server administrators to manage and connect to remote systems without the risk of losing sensitive information to unauthorized users. Figure 1.1 shows a Telnet packet between two entities in clear-text:

Notice in Figure 1.1 that the username is in the clear-text, “kusrum,” and the password is also in the clear-text, “password.” The session can be captured by any type of network sniffer, as long as the session is in clear-text. Some of the most common and vulnerable connections that often get targeted for sensitive information such as passwords are Telnet, FTP, POP3, SMTP, IMAP, SNMP, and HTTP. Figure 1.2 shows an SSH packet between the same two entities used in Figure 1.1.

Notice in Figure 1.2 that none of the information is in clear-text or comprehensible, thus being encrypted. This connection mirrors the Telnet connection (remote command line execution), but with significantly greater security over the password and the username “kusrum.”

SSH provides the following three key security features:

- **Encryption.** SSH encrypts all communication with a variety of cipher algorithms to choose from.
- **Two-factor authentication.** SSH can require a username / password or public key for authentication. In addition, these two options can be used together for two-factor authentication.
- **Integrity.** SSH can create a digital signature of the data transferred from one entity to another, ensuring that the data has not been modified or tampered with in any way.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_34_0.png)

Figure 1.1 Telnet packet between two entities in clear-text.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_35_0.png)

**Figure 1.2** Contents of SSH packet.

### Remote Command Line Execution

SSH offers the ability to execute commands on a remote entity, which can be an operating system or a network device. In the Unix world, SSH gives the remote user the shell listed in the passwd file of the /etc directory; however, the communication is still encrypted over the wire. For example, based on the following Unix passwd file:

```
root::x:0:0:/root:/bin/bash
ksum::x:4:101:Kusum:/home/Kusum:/bin/bash
shreya::x:4:102:shreya:/home/shreya:/bin/bash
sudhanshu::x:4:103:sudhanshu:/home/sudhanshu:/bin/csh
sangeeta::x:4:104:sangeeta:/home/sangeeta:/bin/bash
jgnesh::x:4:105:jgnesh:/home/jgnesh:/bin/bash
kanchan::x:4:106:kanchan:/home/kanchan:/bin/bash
Katie::x:4:107:Katie:/home/Katie:/bin/csh
amit::x:4:108:amit:/home/amit:/bin/bash
rohan::x:4:109:rohan:/home/rohan:/bin/bash
anand::x:4:110:anand:/home/anand:/bin/bash
amlee::x:4:111:amlee:/home/amlee:/bin/sh
neeraja::x:4:112:neeraja:/home/neeraja:/bin/sh
jumdnj1::x:4:113:Jumdnj1:/home/Jumdnj1:/sbin/nologin
```

root gets a bash shell, sudhanshu gets a C shell, neeraja gets a Korn shell, and the user [umdnj1] is not allowed to log in, since the shell allocated to [umdnj1]'s account is nologin, despite making a valid SSH connection. The SSH daemon running on the Unix server would query the information from the passwd file in order to process usernames for authentication. SSH does not use its own username and passwords for authentication; it uses the operating system’s username and password information, which makes the process a lot easier to use. The result would be that valid accounts with an appropriate shell in the passwd file would be authenticated and given the correct shell, while being encrypted with SSH.

The process works a bit differently in the Windows world, but the result is still the same. Since Windows does not have different shell options, all SSH users would be given a command prompt (cmd.exe) or some form of the command prompt itself. Similar to the Unix world, SSH services in Windows use the existing password database (the SAM or ntds.dit files) for authentication.

### Remote File Transfer

Remote file transfer is similar to remote command line execution. SSH offers the ability to retrieve and send files to and from a remote entity. Remote file transfer actually comes in two forms in the Unix world. SSH offers Secure Copy Protocol (SCP) in some installations of SSH1 and SSH2, or Secure File Transfer Protocol (SFTP), in most installations of SSH2. In the Windows world, only SFTP exists. Both SCP and SFTP provide similar, if not the same, function, which is to put and get files from a remote entity in a secure fashion. SFTP uses the existing SSH daemon on Unix and the existing SSH service on Windows. There is no extra step required to enable secure file transfer; it is automatically enabled on most versions of SSH2. Many SSH clients also come packaged with SCP or SFTP clients; therefore, the use and execution of the additional functionality is very straightforward. Furthermore, there are SCP/SFTP clients only, such as PuTTY, which are discussed in Chapter 3. But several installations of SSH clients have some type of file transfer utility included.

Similar to the Telnet session described previously, most SCP or SFTP installations are able to protect against the weaknesses of their counterpart: clear-text communication of FTP. Figure 1.3 shows an FTP packet between two entities in clear text.

```
220 Microsoft FTP Service
USER kusum
331 Password required for kusum.
PASS divyedi
```

![](img/c99d6f526a5f9fa62f2c34daada85ad7_36_0.png)
