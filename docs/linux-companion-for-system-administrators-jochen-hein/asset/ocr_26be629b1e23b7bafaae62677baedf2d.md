# 434 NETWORK APPLICATIONS

considered marginal. Today this subject is much more important than it used to be.

In many programs, passwords are transmitted in clear text. Examples for this telnet and ftp. When a connection is established in a local network, you can use a packet sniffer like tcpdump to protocol the entire session including the login. Remedy can be brought by methods such as one-way passwords (as S/Key), but the whole connection is still transmitted in clear text, including further passwords.

The r programs, for example login and rsh, can be configured by means of the files /etc/hosts.equiv (system-wide) or ~.hosts in such a way that no password is required. This method of authentication is, however, not particularly safe and can, for example, be hoodwinked by IP or DNS sniffing. Here login programs have the option -x for encryption of the session by DES.

This can be replaced by the ssh package which contains (nearly) all r programs in a more secure version. This begins with the programs ssh and rsh and login and ends with a more agreeable version of rcp, scp. These programs are set up on your network, you can quietly delete the (unsafe) r programs from your system without noticing any change.

The s programs are based on a series of key methods. Each computer has a host key which exists in one and private variation. Computers can authenticate each other by encrypting a challenge with the public key of the other computer and sending it to that computer. Only this computer can decrypt and answer the challenge and send it back (encrypted).

Furthermore, a session key is generated for the encryption of each session. This key is not stored on the hard disk, but only in RAM. For security reasons, this key is periodically discarded and generated fresh.

Besides the host-based authentication, users can define their own confidential relationships that allow logging without password. However, we will install and configure the programs. We will first consider a series of computers under unique administration. Formerly, the file /etc/hosts.equiv was used in a computer pool, so users could switch between different computers by login.

As already known from many other programs, the ssh package is compiled with ./configure and make and installed with install (in /usr/local); this can be changed by means of the option -prefix in configure. This automatically creates a host key (by means of ssh-keygen). If you install the programs on a shared disk (/usr/local is shared via NFS, you must manually create a pair of keys for each computer.