
To grant the users Jason and Scott on any remote host access to any account on the local system, add the following to /etc/hosts.equiv.

+ jason scott

For the purposes of this chapter, you can allow access to the root account from a particular host. For example, to allow access from the machine server1, you can add server1 to root's hosts file. If, instead, you added server1 root to /etc/hosts.equiv, you would have allowed root access not just from the remote root user, but from any user on the client.

Now that you can log in as root, you can perform a variety of remote administrative tasks. For example, use these commands to copy a new version of /etc/inetd.conf to another server and restart inetd.

```bash
# rcp /etc/inetd.conf server1:/etc/inetd.conf
# rsh server1 -kill HUP inetd
```

Setting up this access for two or three servers may seem like overkill, but when you are intervening tens or hundreds of servers, the r-commands can be invaluable administrative tools.

# The Security Dangers of r-commands

The Berkeley r-commands were the tools of choice for remote command execution before the advent of the Internet in the early 1990s. But r-commands provide little security—the primary concern in today's publicly accessible networks. Not only is r-command network traffic unencrypted, but of even greater concern is the trust servers place in the clients.

On a server that allows the user to log in from any host, for example, a malicious user could easily install his own system on the same network with a user that has the same UID as the one on the server. That second then would be able to log to the server without a password. This prospect is even scarier if you have several allowances for access as root.

![](img/894492738e879267320b8d6f9a044180_361_0.png)

> Host Restrictions Can Be Compromised
> Even r-command restrictions can be compromised by forging the source address in IP packets. This is called spoofing, and you can read more about it in Chapter 13, "Implementing System Security."

# Using SSH Instead of the r-commands

One solution to the r-command security problem is to use r-commands only on trusted networks. When that isn't possible, you can use SSH, the secure shell. In addition to using an encrypted channel, SSH provides public key authentication, which can be used for password-less logins. OpenSSH, with origins in the OpenBSD operating system, is quickly becoming the most popular SSH server for Unix systems. It is freely available from http://www.openssh.org and comes standard with many versions of Linux.

# Use SSH Whenever Possible, But Remember How to Use the r-commands

Always use SSH instead of the r-commands when possible, especially when running commands remotely to root. The encryption and advanced security mechanisms provide a much more secure environment for performing administrative tasks. However, it is important to remember what the r-commands are and how to use them, as SSH may not always be available, especially on freshly loaded systems.

The details of public key authentication are beyond the scope of this book, but in general, the system employs two asymmetric keys, and one key can decrypt data encrypted by the other key. One of these keys is private and should be kept secret, but the other is public and can be distributed without fear of compromising security.

In traditional symmetric key encryption, the keys used for encryption and decryption are identical. The client uses the private key to generate a signature that cannot be forged by anyone who does not have that key. The server verifies the signature by decrypting it with its copy of the public key, and authentication is complete.

# SSH Can Use hosts Authentication

SSH can also be configured to use hosts authentication, but it is not recommended unless it is implemented with public key authentication. Even though traffic is encrypted, source addresses can still be spoofed, preventing the same problem solved by the Berkeley-r commands.

Setting up public key authentication for root SSH is very easy. You can use OpenSSH 3.1pl (freely available for most versions of Unix) to perform the following setup. First, you need to generate a key pair (public and private key) using ssh-keygen.

```bash
# ssh-keygen -t rsa -b 1024
Generating public/private rsa key pair.
Enter file in which to save the key (~/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in ~/.ssh/id_rsa.
Your public key has been saved in ~/.ssh/id_rsa.pub.
The key fingerprint is:
1a:7e:c0:72:2a:74:41:36:db:1bf:3f:fe:d5:54@server1
```

You have created a 1,024-bit RSA key and stored the key in ~/.ssh/id_rsa and the public key in ~/.ssh/id_rsa. As added, SSH supports a passphrase to encrypt the private key, but because you are using this to facilitate authentication, you used an empty passphrase, keeping the key unencrypted. Due to its sensitive nature, the private key is readable only by root, but the public key is meant for distribution and is stored in a human-readable format.

```text
# id_rsa.pub
ssh-rsa AAAAB3NzaN1yc2AAAAAAAABQAAABAIAYtn8V3prqrQtaMFG0kXM/81YPRLUbJrROvqh/HHQEYWW54KaWbbt+Dw7GsfFRvvkHtrCcVZMMyq04C0sGsjV1APMyq0zcMgy8ltvsVOEFPAH@server1
```

# UNIX SYSTEM MANAGEMENT PLUS

# Key Pair Length

Most key pairs should be between 1024 and 2048 bits in length. Any less would risk compromise, and any more would add processing time for additional security. The next step is to add this public key to root's authorized_keys on each server on which you want to log in. The public keys in this file dictate which of the corresponding keys can be used to authenticate as root. When you've finished this step, anyone with access to your freshly created key can run commands on those servers.

```bash
ssh server2 uid=(root) gid=(other)
```

# /root in Red Hat

The previous examples assumed that /root was root's home directory. On Red Hat Linux and the BSD family, root's home directory is /root, and therefore .ssh directory would be located in /root/.ssh/. Public key authentication may not seem any more secure than the trust mechanism, but the level of security ultimately falls into the hands of the system administrators. The private key is kept well-protected and exists only on a minimum of machines, preventing any danger to the r-commands.

# Automating File Synchronization

The file system is at the heart of Unix functionality, containing such things as kernel code, configurations, data, and device interfaces. Maintaining individual files on these systems is not difficult until your machine count begins to increase. At that point, instead of editing a few files on two or three machines, you have ten, twenty, or even hundreds of files to maintain. A file synchronization mechanism makes the maintenance and distribution of these files easier for system administrators by enabling files on remote servers to be synchronized with a master repository. Several tools can help you with this task; among them are rcp, rsync, scp, and rdist. Each of these tools copies from one place to another; rcp and scp copy individual files and directories you explicitly specify on the command line, while rsync and rdist are best used to

# Copying Files with rcp and scp

scp is a very simple utility that uses the hosts authentication mechanism to copy files to remote systems. Its syntax is follows:

```bash
scp [-rp] source ... destination
```

The source and destination arguments each contain a path and an optional host and username in the following format:

```bash
username@host:path
```

The -r option is used to recursively copy a directory, and -p preserves ownership and permissions on all the files across the copy. As an example, copying /etc/group from server2 to server1 can be accomplished with the following command, run as root on server1:

```bash
server1 rcp server2:/etc/group /etc/group
```

Copying the entire /usr/local/bin directory from server1 to /usr/testing on server2 as the user Adam is as easy as typing this:

```bash
server1 -r /usr/local/bin server2:/adam@usr/testing
```

scp is SSH's replacement for rcp; due to the security concerns with the r-commands, scp should be used instead of rcp when possible. sc has the same syntax as rcp and accepts the same options, along with extras, including -C which enhances compression. This option is extremely useful for transferring large files across slow links like a T1.

![](img/894492738e879267320b8d6f9a044180_364_0.png)

> Real-Example: scp Reduces Bandwidth Usage
> A small company installed a private T1 between its main office and its data center a few miles away. The system administrator periodically received complaints about slow connectivity to the data center, and upon examining utilization graphs from MRTG, discovered that the T1 was at almost 100% utilization for hours during the day. After further investigation, the administrator discovered that a 600MB text file was being periodically copied from the data center using FTP. Since text presses very well, the administrator suggested using scp with the compression option -C. Instead of taking hours, the transfer took ten minutes, giving everyone their back.

# Synchronizing Files with rsync

scp builds on rcp by adding encryption, public key authentication, and compression. Likewise, rsync adds an incremental component to file copying; if the file being copied already exists at the destination path, rsync compares the files in chunks, and only transfers the chunks that have changed. Considering that most changes in large files tend to occur in a few regions, rsync can shave off up to 99% of the time it would take to copy the entire file, which is an important advantage for networks with slow links.
