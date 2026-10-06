# UNIX SYSTEM MANAGEMENT PRIMER PLUS

# Key Pair Length

Most key pairs should be between 1,024 and 2,048 bits in length. Any less would risk key compromise, and any more would add processing time for the additional security.

The next step is to add this public key to root's authorized_keys on each server on which you want to log in as root. The public keys in this file dictate which of the corresponding keys can be used to authenticate as root. When you've finished this step, anyone with access to your freshly created key can run commands on those servers.

```
# ssh server2 id
uid=(root) gid=1(other)
```

The authorized_keys file can contain any number of different public keys that can be used to log in as root, but you should try to minimize the number of keys that have this kind of access. In general, it is best to have a single server with the private key needed to authenticate as root; keeping track of one key on one server is much easier than maintaining many keys on several different servers.

# /root in Red Hat Linux

The previous examples assumed that / was root's home directory. On Red Hat Linux and the BSD family, root's home directory is /root, and therefore root's .ssh directory would be located in /root/.ssh.

Public key authentication may not seem any more secure than the hosts trust mechanism, but the level of security ultimately falls into the hands of the system administrators. The private key is kept well-protected and exists on a bare minimum of machines, the risk is minimal. Any root compromise on the system with the private key can prevent any danger to the other machines; SSH public key authentication is not vulnerable to the IP spoofing and UID guessing that the r-commands are.

# Automating File Synchronization

The file system is at the heart of Unix functionality, containing such things as kernel code, configurations, software, data, and device interfaces. Maintaining individual files on these file systems is not difficult, until your machine count begins to increase. At that point, instead of editing a few files on two or three machines, you have ten, twenty, or even hundreds of these to maintain. A file synchronization mechanism makes the maintenance and distribution of these files easier for system administrators by enabling files on remote servers to be synchronized with a master file repository.

Several tools can help you with this task; among them are rcp, rsync, scp, and rdist. Each of these tools copies files from one place to another; rcp and scp copy individual files and directories you explicitly specify on the command line, while rsync and rdist are best used to