
Note that the -e option specifies that the argument is a file. The output reflects the fact that the verification failed. Each file's size, MD5 hash, and modification time are different than they were originally. This is no big deal, since each of these files is a configuration file (note the "c") and is likely to change.

If a verification passes, there is no output. For example:

```
# rpm -Vf /sbin/iconfig
#
```

indicates that /sbin/iconfig and all other files in the package containing /sbin/iconfig have not changed since installation.

You may also verify installed packages against the CD. For example, insert the Red Hat distribution CD into your CD-ROM drive and:

```
# mount /mnt/cdrom
# rpm -Vp /mnt/cdrom/RedHat/RPMS/bash-1.14.7-13.i386.rpm
#
```

which verifies that the package, bash-1.14.7-13, loaded on your system matches the one found on the CD.

This capability can assist you in improving your security by verifying the integrity of your packages. See Maximum RPM in the section, RPM Resources on page 28, for further details.

### Checking PGP Signatures with RPM

Some RPM packages will incorporate PGP signatures (PGP is discussed in An Overview of PGP on page 45). If you obtain such an RPM, you may verify the signature with the -k flag. For example, we verify the signature on a Secure Shell (SSH) RPM.

```
# rpm -K ssh-1_2_26-ius_i386.rpm
ssh-1_2_26-ius_i386.rpm: size pgp md5 OK
#
```

Note that the MD5 hash is also verified. If we would like more verbose output, we can add the -v option as in:

```
# rpm -Kv ssh-1_2_26-ius_i386.rpm
ssh-1_2_26-ius_i386.rpm:
Header-Archive size OK: 172248 bytes
Good signature from user "Jan "Yenya" Kasprzak <kas@fi.muni.cz>".
Signature made 1998/07/11 18:13 GMT using 1024-bit key, key ID D3498839

WARNING: Because this public key is not certified with a trusted signature, it is not known with high confidence that this public key actually belongs to: "Jan "Yenya" Kasprzak <kas@fi.muni.cz>".
MD5 sum OK: ebf614babe96926b4c9f9d9fcbba171
#
```

If you are missing the public key required to verify a signature, RPM will tell you; for example:

```
# rpm -K sudo-1.5_7p4-1_src.rpm
sudo-1.5_7p4-1_src.rpm: size (PGP) md5 OK (MISSING KEYS:
PGP#396D16C1)
#
```

Now you have to go off and find the public key. See *An Overview of PGP* on page 45.

### RPM Resources

Unfortunately, at the time of this writing, RPM version 3.0.x is in common use (Red Hat 6.0 incorporates RPM version 3.0.1), but most of the documentation relates to RPM version 2.5.x. Since there are numerous differences, this is somewhat problematic. The RPM 2.5.x documentation is still quite useful, but there are a number of issues which require careful review of the changes. So we have broken out the documentation into two sections, identified by version. Also, join the RPM mailing list, as noted below, for more resources. Despite the fact that it is dated, *Maximum RPM* is the definitive guide to RPM and we highly recommend it.

### Version 2.5.x

On-Line:
/usr/doc/HOWTO/RPM-HOWTO

Book:
3. Bailey, Edward C., *Maximum RPM*, Indianapolis, Indiana, redhat press, 1997.

*Maximum RPM* is also available via the Internet at,
http://www.redhat.com/knowledgebase/zhtml/linuxdocs.html

### Version 3.0.x

You will find a number of documents in the directory on Red Hat 6.0:
/usr/doc/rpm-3.0.1/

### RPM Mailing List

You may join the RPM mailing list by sending an e-mail to `rpm-list-request@redhat.com` with `subscribe` in the body of the e-mail. Subsequently, you may communicate to the list by sending e-mail to `rpm-list@redhat.com`. This is an excellent list and we strongly encourage your participation.

# TCP/IP NETWORKING OVERVIEW

Let's start with a few definitions. A networking model reflects a design or architecture to accomplish communication between different systems. A networking model usually consists of layers. Each layer of a model represents specific functionality. Within the layers of a model, there are usually protocols specified to implement specific tasks. You may think of a protocol as a set of rules or a language. A layer is normally a collection of protocols.

The TCP/IP networking model takes its name from two of its protocols, TCP (the Transmission Control Protocol which lives in the Transport layer) and IP (the Internet Protocol which lives in the Internet layer). Figure 3.1 provides a five-layer² representation of the TCP/IP model.

The middle three layers of the model represent functionality performed internally by the kernel. The Application layer includes commands and daemons. The Hardware layer is comprised of hardware components.

The process of initiating a network communication, like executing telnet hostname, causes the initiator (usually the client) to encapsulate application data, beginning at the top of the model and moving down, for the network transmission. In other words, each layer encapsulates the application data with information used to determine where the packet is supposed to go and which service needs to be invoked to handle the data itself. The receiving system, normally the server, performs the same steps except in reverse (bottom to top), decapsulating the data.

On the left-hand side of Figure 3.1, you see an increasing number of rectangles as you scan down the layers. The area in gray represents the information added to the growing packet by each layer to the right. In the following sections, we will briefly review the information generated by each layer and its purpose.

### The TCP/IP Model Layers

**The Hardware Layer**
The Hardware layer is responsible for exactly that. Hardware. This includes cables, interface cards, and repeaters. It accepts the data passed to it by the Network Interface layer and prefixes the *preamble*, which is a well-known sequence of 64 bits used for synchronization purposes. After prefixing the preamble, it generates a *signal* to be submitted to the media (electrically based cables in most cases). The Hardware layer also imposes the maximum transfer unit (MTU), which is used by the Internet layer to ensure that the Hardware layer does not get *frames*³ that are too large or too small. For Ethernet, the MTU for the frame is 1518 octets, and the minimum frame size is 64 octets.

There are two hardware devices that operate at this layer: repeaters and amplifiers. A repeater is a device with a number of ports (usually four or more) that is capable of receiving signals, filtering out noise (phenomena not related to the communication at hand), and repeating the signals to every port except the ingress (incoming) port. Amplifiers perform the same task, except that they do not filter noise. Consequently, we find repeaters in environments using electrical communications and amplifiers in environments using light-based communications. These devices are also often called *hubs* or *concentrators*.

**The Network Interface Layer**
You may think of the Network Interface layer as a collection of device drivers. Its responsibility is to prepare the data passed to it from the Internet layer for signalling. It does this by prefixing its header (indicated as *NILH*—a 32-bit checksum), computing a cyclic redundancy check (CRC—a 32-bit checksum), appending the CRC to the datagram, and passing this information to the device (interface) for signalling in a frame. In particular, this layer understands *physical* addresses (often referred to as media access control [MAC] addresses). When using Ethernet, this is often called an *Ethernet* address. Physical addresses are local and need to be unique only within a *local network* (defined in the section, *The Internet Layer* on page 32). For Ethernet interface chips, they are 48-bit addresses permanently written into programmable read only memory (PROM).

The Network Interface layer writes both the destination and source physical address into its header. Consequently, it is at this layer that initial decisions are made about whether or not to continue processing an incoming packet up the stack (decapsulate). When generating a frame, the Network Interface layer...

3. The output of the Network Interface layer is called a *frame* when each output varies in size. More formally, when using Ethernet, it should be called an *Ethernet frame*. Fixed-size output, such as that produced by asynchronous transfer mode (ATM), is called a *cell*.
