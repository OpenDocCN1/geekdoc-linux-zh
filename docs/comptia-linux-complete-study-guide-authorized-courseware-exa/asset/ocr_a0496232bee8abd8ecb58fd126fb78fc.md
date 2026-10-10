511

# # Exam Essentials

**Identify the purpose of a super server.** Super servers, such as inetd and xinetd, manage incoming network connections for multiple servers. They can add security and convenience features, and they can help minimize the memory load imposed by seldom-accessed servers.

**Explain the function of super server port access controls.** Super servers or programs called by them (such as TCP Wrappers) can restrict access to ports for the servers they manage. These restrictions occur at a higher level than a firewall’s restrictions, and they apply only to the servers managed by the super server.

**Summarize the tools you can use to identify the servers running on a computer.** The netstat and lsof programs both provide options to list all (or a subset of) the open network connections, as well as programs that are listening for connections. Remote network scanners, such as Nmap, can probe another computer for open network ports. Perusal of local configuration files can also provide clues to what’s running on a computer.

**Describe why SUID and SGID programs are potentially risky.** The set user ID (SUID) and set group ID (SGID) bits tell Linux to run the program as the user or group that owns the file. This is particularly risky when root owns the program file because it essentially elevates all users to root for the purposes of running the file, making bugs in the program more dangerous and raising the possibility of a clever user abusing the program to acquire full root privileges or otherwise wreaking havoc.

**Explain why shadow password files are important.** Shadow passwords store password hashes in a file that can’t be read by ordinary users, thus making it harder for miscreants on the local system to read the hashed passwords and use brute-force attacks to discover other users’ passwords. Modern Linux distributions use shadow passwords by default.

**Explain how to generate a good password.** Ideally, passwords should be random. Failing that, one good approach is to generate a base that’s hard to guess and then modify it by adding digits and punctuation, changing the case of some characters, and changing letter order.

**Explain why SSH is the preferred remote text-mode login tool.** The Secure Shell (SSH) protocol provides encryption for all traffic, including both the password exchange and all subsequent data exchanges, whereas older tools, such as Telnet, do not. This makes SSH much safer (if not 100 percent safe) for the exchange of sensitive data, particularly over untrusted networks such as the Internet.

**Identify the most important SSH configuration file.** The SSH server is controlled through the /etc/ssh/sshd_config file. The SSH client configuration file is /etc/ssh/ssh_config; don’t confuse the two.

**Describe the function of GPG.** GPG enables public-key encryption of individual files or e-mail messages. You can use GPG to encrypt sensitive data for transmission over e-mail or other insecure means.