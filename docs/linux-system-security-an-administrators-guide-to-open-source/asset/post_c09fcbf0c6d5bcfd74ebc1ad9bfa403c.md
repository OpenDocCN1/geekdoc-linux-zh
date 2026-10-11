
Perhaps the greatest vulnerability associated with TCFS is the fact that, by default, all encryption/decryption keys are accessible with the user’s password. Dissociating these keys from the user password is possible (as outlined in TCFS Key Management on page 429), but it is very cumbersome, making it unlikely that it will be commonly done. As previously noted, future revisions promise improvement. One high note for TCFS is that it is under active development. So join the TCFS mailing list (see E-Mail Lists on page 433) and make suggestions!

## CFS AND TCFS COMPARISON

TCFS offers a much better-performing implementation than CFS. The implementation is also transparent to users because its resources are accessed through a simple NFS mount (no requirement for a specific mount tied to a special daemon) and could be implemented through the automounter or similar mechanism. On the other hand, TCFS has a significantly weaker method of key generation and, by default, only supports triple DES encryption. TCFS also suffers from very poor documentation.

Perhaps the most significant difference between the two utilities is the administrative burden. CFS is easy to install and once configured is very low maintenance. TCFS is quite difficult to install and requires administrative intervention to manage users and groups and to allow users to create multiple keys.

While both of these utilities have their downsides, they each offer the tremendous benefit of encrypted files and are well worth both putting forth the effort and watching for potential vulnerabilities—consider how vulnerable you are in their absence.

## SECURELY DELETING FILES

A topic somewhat related to securing files via encryption is that of securely deleting files. When you delete a file from the ext2 filesystem, the contents of the file are not removed. Rather the blocks allocated for the file are simply freed for use by the filesystem. Eventually the data will be overwritten when other files require additional disk blocks and the system reuses the blocks from the deleted file. This means that in the interim the data may be available to unscrupulous activity. This includes data that has been temporarily stored in RAM or a disk cache, so this is a pertinent concern regarding CFS and TCFS.

One way to improve upon securely deleting disk files is to use the secure delete attribute on your files as in

```
$ chattr +s secret_file
```

which will cause all of the blocks in the file to be set to 0 upon deletion. This attribute and the chattr command are discussed in detail in File Attributes on page 75 of Chapter 4.

Unfortunately, this technique does not even provide minimal protection against a variety of file recovery techniques. Such techniques are discussed in detail in the article, *Secure Deletion of Data from Magnetic and Solid-State Memory*, by Peter Gutmann (see *Papers* on page 433). This article is available from

http://www.cs.auckland.ac.nz/~pgut001/pubs/secure_del.html

and is well worth the read. In short, Gutmann suggests that the secure removal of data from disk and RAM requires writing over the data blocks many times with alternating patterns. Moreover, to thoroughly remove data from such media requires specialized equipment and may even require the destruction of the disk or RAM. Whether you need to obtain such specialized equipment to erase your data depends on your Security Policy (see Chapter 2). We will mention two user-level programs that make obtaining erased data expensive and difficult.

One utility that more securely deletes files is wipe. It is written and maintained by Berke Durak, copyrighted by the Free Software Foundation (FSF), and distributed under the GPL. You may obtain *wipe* from either `http://gsu.linux.org.tr/wipe/` or `http://alterum.org/berke/wipe/`. *wipe* writes 34 patterns, 8 of which are random, over the target file, directory, or filesystem.

Another utility, *secure_delete*, is available from `http://zsw.base.org/` (then click on “the files”). It is a collection of tools that erase files, filesystems, holes in files or filesystems, swap, and RAM. It uses 38 patterns, 10 of which are random. It is copyrighted by van Hauser. This suite of programs is definitely worth investigating if you are concerned about the CFS and/or TCFS cleartext remnants in swap and RAM.

Both *secure_delete* and *wipe* include Peter Gutmann’s paper in their respective distributions.

## ALTERNATIVES TO CFS AND TCFS

You may wish to use Pretty Good Privacy (PGP), discussed in *An Overview of PGP* on page 45, for the encryption of files. However, it cannot automatically encrypt all files within a directory as CFS or TCFS can. For a small number of encrypted files, however, PGP offers simpler use and administration.

SSH (discussed in detail in Chapter 11) is strongly recommended over ESM.

## SUMMARY

We discussed both the CFS and TCFS utilities for encrypting data on a directorywide basis. We compared the advantages and disadvantages of both tools.

We also briefly discussed some of the tools available to securely delete data files from RAM and disk.

## FOR FURTHER READING

### Papers

- 1. Blaze, Matt, *A Cryptographic File System for Unix*, Proceedings of the 1st ACM Conference on Computer and Communications Security, Fairfax, Virginia, November 1993.
- 2. Gutmann, Peter, *Secure Deletion of Data from Magnetic and Solid-State Memory*, Sixth USENIX Security Symposium Proceedings, San Jose, California, July 1996.

### E-Mail Lists

To subscribe to the CFS list, send an e-mail to

```
cfs-users-request@research.att.com
```

with **subscribe cfs-users** in the body of the message.

To subscribe to the TCFS list, send an e-mail message to

```
major@domo@edu-gw.dia.unisa.it
```

with **subscribe tcfs-list** in the body of the message.

## CHAPTER 16

## We Must Censor!

### Packet Filtering with ipchains

Until this chapter, we have largely discussed host-based security. Granted, such utilities as SSH, CFS, TCFS, **TCP_wrappers**, and *xined* are network or network-capable applications; however, our discussions of those utilities focus on restricting or securing system and local area networking access. In this chapter, we will discuss the Linux network packet-filtering and masquerading capabilities through the use of ipchains. This is a topic that is fundamentally network-centric and generally falls under the auspices of a firewall.

In the context of computing, a firewall is a system that prevents unauthorized network communications to it, from it, and through it. The Linux ipchains is capable of establishing rules that provide a reasonably secure firewall under many circumstances. It can also provide a remarkable level of flexibility in terms of selectively restricting traffic flow to, from, and through the system. Additionally, ipchains can work in conjunction with other software to provide other options not available in ipchains itself. Unfortunately, despite all of its advantages, ipchains can't solve every problem.

Linux ipchains implements a packet-filtering firewall. This means that each network packet may be filtered against a set of rules. This procedure is performed in the kernel. It specifically causes the kernel to analyze each packet for source and destination IP addresses and port numbers or ICMP types and codes. A more intelligent but similar type of firewall is a stateful packet-filtering firewall. The difference between stateful filtering and ipchains is that the stateful filter can keep track of its connections and thereby distinguish packets associated with an established connection and packets that are not. While Linux `ipchains` is incapable of this, there is a wrapper program that can add this functionality on top of `ipchains`. If you need stateful capabilities, check out

`ftp://ftp.interlinx.bc.ca/pub/spf/`

where you will find Brian Murrell's stateful packet-filtering project.

Another type of firewall is a proxy-based firewall. This type of firewall operates as a go-between for services. All network connections destined through the proxy-based firewall terminate at the firewall. Then (if the rules allow) the proxy-based firewall will make a connection to the destination system on behalf of the originating host. The proxy-based firewall thereby manages two separate connections. We will touch on proxy firewalls such as Trusted Information System's Firewall Toolkit (FWTK) and NEC's SOCKSv5. It is common to implement FWTK or SOCKS in conjunction with `ipchains`.

Let's begin our detailed look at `ipchains`.

## PACKET FILTERING

The concept of packet filtering is a fairly simple one. The contents of the headers (see *TCP/IP Networking Overview* on page 28) of each network packet are checked against a series of rules. Each rule includes an action, so that, when a packet matches a rule, the action component of the rule tells the kernel what to do with the packet. In essence, we can censor network packets. In order to implement the inspection of network packets or to filter the packets, there must be software that provides the capability. The modern Linux kernel includes this capability.

The precise mechanism for packet filtering in Linux depends upon the version of the Linux kernel. The packet-filtering implementation for Linux kernels version 2.1.102 and above is `ipchains`. This includes the Red Hat 6.0 distribution (kernel version 2.2.x). By default, kernel versions prior to 2.1.102 implement `ipfwadm`, including the Red Hat 5.2 distribution (kernel version 2.0.3x). The `ipchains` mechanism provides greater flexibility and capability. Therefore, we will discuss that implementation.

If you are using an earlier kernel implementation that does not include `ipchains` and you need to use `ipfwadm`, visit the site

`http://www.xos.n1/linux/ipfwadm/`

for documentation. The syntax and implementation of `ipfwadm` is quite similar to `ipchains` except that `ipchains` includes functionality which is not supported in `ipfwadm`. For kernel version 2.0.34 and later, you may upgrade to `ipchains` with a patch. Visit the site

`http://www.rustcorp.com/linux/ipchains/`
