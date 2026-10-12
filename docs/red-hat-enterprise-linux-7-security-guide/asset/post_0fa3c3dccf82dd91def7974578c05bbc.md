
## 4.14.2. Adding New Certificates

To add a certificate in the simple PEM or DER file formats to the list of CAs trusted on the system, copy the certificate file to the `/usr/share/pki/ca-trust-source/anchors/` or `/etc/pki/ca-trust/source/anchors/` directory. To update the system-wide trust store configuration, use the `update-ca-trust` command, for example:

```bash
# cp ~/certificate-trust-examples/Cert-trust-test-ca.pem /usr/share/pki/ca-trust-source/anchors/
# update-ca-trust
```

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_143_0.png)

**NOTE**

While the Firefox browser is able to use an added certificate without executing `update-ca-trust`, it is recommended to run `update-ca-trust` after a CA change. Also note that browsers, such as Firefox, Epiphany, or Chromium, cache files, and you might need to clear the browser's cache or restart your browser to load the current system certificates configuration.

## 4.14.3. Managing Trusted System Certificates

To list, extract, add, remove, or change trust anchors, use the `trust` command. To see the built-in help for this command, enter it without any arguments or with the `--help` directive:

```bash
$ trust
usage: trust command <args>...

Common trust commands are:
    list        List trust or certificates
    extract     Extract certificates and trust
    extract-compat Extract trust compatibility bundles
    anchor      Add, remove, change trust anchors
    dump        Dump trust objects in internal format

See 'trust <command> --help' for more information
```

To list all system trust anchors and certificates, use the `trust list` command:

```bash
$ trust list
pkcs11:id=%d2%87b4%e3%df%37%2793%55%f6%56%ea%81%e5%36%cc%8c%1e%3f%bd;type=cert
        type: certificate
        label: ACCVRAIZ1
        trust: anchor
        category: authority

pkcs11:id=%a6%b3%e1%2b%2b%49%b6%d77%3%aa%94%f5%01%e7%73%65%4c%ac%50;type=cert
        type: certificate
        label: ACEDICOM Root
        trust: anchor
        category: authority
...
[Output has been truncated]
```

All sub-commands of the `trust` commands offer a detailed built-in help, for example:

```bash
$ trust list --help
usage: trust list --filter=<what>

  --filter=<what>      filter of what to export
                       ca-anchors     certificate anchors
                       blacklist      blacklisted certificates
                       trust-policy   anchors and blacklist (default)
                       certificates   all certificates
                       pkcs11:object=xx a PKCS#11 URI
  --purpose=<usage>    limit to certificates usable for the purpose
                       server-auth    for authenticating servers
                       client-auth    for authenticating clients
                       email          for email protection
                       code-signing   for authenticating signed code
                       1.2.3.4.5...   an arbitrary object id
  -V, --verbose        show verbose debug output
  -q, --quiet         suppress command output
```

To store a trust anchor into the system-wide trust store, use the `trust anchor` sub-command and specify a *path* to a certificate, for example:

```bash
# trust anchor path.to/certificate.crt
```

To remove a certificate, use either a *path* to a certificate or an ID of a certificate:

```bash
# trust anchor --remove path.to/certificate.crt
# trust anchor --remove "pkcs11:id=%AABB%CC%DD%EE;type=cert"
```

## 4.14.4. Additional Resources

For more information, see the following man pages:

- `update-ca-trust(8)`
- `trust(1)`

## 4.15. USING MACSEC

Media Access Control Security (MACsec, IEEE 802.1AE) encrypts and authenticates all traffic in LANs with the GCM-AES-128 algorithm. MACsec can protect not only IP but also Address Resolution Protocol (ARP), Neighbor Discovery (ND), or DHCP. While Ipsec operates on the network layer (layer 3) and SSL - TLS on the transport layer (layer 4), MACsec operates in the data link layer (layer 2). Combine MACsec with security protocols for other networking layers to take advantage of different security features that these standards provide.

See the *MACsec: a different solution to encrypt network traffic* article for more information about the architecture of a MACsec network, use case scenarios, and configuration examples.

For examples how to configure MACsec using `wpa_supplicant` and `NetworkManager`, see the *Red Hat Enterprise Linux 7 Networking Guide*.

## 4.16. REMOVING DATA SECURELY USING SCRUB

The `scrub` utility sets patterns on special files or disk devices to make retrieving data more difficult. Using `scrub` is faster than writing random data on a disk. This process provides high availability, reliability, and data protection.

To start using the `scrub` command, install the `scrub` package:

```bash
~]# yum install scrub
```

The `scrub` utility operates in one of the following basic modes:

### Character or Block Device

The *special file* corresponding to a whole disk is scrubbed and all data on it, is destroyed. This is the most effective method.

```bash
scrub [OPTIONS] special file
```

### File

A regular file is scrubbed and only the data in the file is destroyed.

```bash
scrub [OPTIONS] file
```

### Directory

With the -X option, a directory is created and filled with files until the file system is full. Then, the files are scrubbed as in file mode.

```bash
scrub -X [OPTIONS] directory
```

### Example 4.7. Scrubbing a Raw Device

To scrub a raw device **/dev/sdf1** with default National Nucluar Security Administration (NNSA) patterns, enter the following command:

```bash
~]# scrub /dev/sdf1
scrub: using NNSA NAP-14.1-C patterns
scrub: please verify that device size below is correct!
scrub: scrubbing /dev/sdf1 1995650048 bytes (~1GB)
scrub: random |...................................................|
scrub: random |...................................................|
scrub: 0x00   |...................................................|
scrub: verify  |...................................................|
```

### Example 4.8. Scrubbing a File

1. Create a *1MB* file:

```bash
~]$ base64 /dev/urandom | head -c $[ 1024*1024 ] > file.txt
```

2. Show the file size:

```bash
~]$ ls -lh
total 1.0M
-rw-rw-r--. 1 username username 1.0M Sep 8 15:23 file.txt
```

3. Show the contents of the file:

```bash
~]$ head -1 file.txt
Jn9paTEveB/IYsbn091huJdw+0jJkhwCIBUsxLXlAyB8uItotUINHKKUeS/7bCRKDQgEP+yJm8VQgL
```

4. Scrub the file:

```bash
~]$ scrub file.txt
scrub: using NNSA NAP-14.1-C patterns
scrub: scrubbing file.txt 1048576 bytes (~1024KB)
scrub: random |....................................................|
scrub: random |....................................................|
scrub: 0x00 |....................................................|
scrub: verify |....................................................|
```

5. Verify that the file contents have been scrubbed:

```bash
~]$ cat file.txt
SCRUBBED!
```

6. Verify that the file size remains the same:

```bash
~]$ ls -lh
total 1.0M
-rw-rw-r--. 1 username username 1.0M Sep 8 15:24 file.txt
```

For more information on `scrub` modes, options, methods, and caveats, see the `scrub(1)` man page.

# CHAPTER 5. USING FIREWALLS

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_147_0.png)

**NOTE**

To expand your expertise, you might also be interested in the Red Hat Server Hardening (RH413) training course.

## 5.1. GETTING STARTED WITH FIREWALLD

A firewall is a way to protect machines from any unwanted traffic from outside. It enables users to control incoming network traffic on host machines by defining a set of firewall rules. These rules are used to sort the incoming traffic and either block it or allow through.

`firewalld` is a firewall service daemon that provides a dynamic customizable host-based firewall with a D-Bus interface. Being dynamic, it enables creating, changing, and deleting the rules without the necessity to restart the firewall daemon each time the rules are changed.

`firewalld` uses the concepts of *zones* and *services*, that simplify the traffic management. Zones are predefined sets of rules. Network interfaces and sources can be assigned to a zone. The traffic allowed depends on the network your computer is connected to and the security level this network is assigned. Firewall services are predefined rules that cover all necessary settings to allow incoming traffic for a specific service and they apply within a zone.

Services use one or more *ports* or *addresses* for network communication. Firewalls filter communication based on ports. To allow network traffic for a service, its ports must be *open*. `firewalld` blocks all traffic on ports that are not explicitly set as *open*. Some zones, such as *trusted*, allow all traffic by default.

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_147_1.png)

Figure 5.1. The Firewall Stack

### 5.1.1. Zones

`firewalld` can be used to separate networks into different zones according to the level of trust that the user has decided to place on the interfaces and traffic within that network. A connection can only be part of one zone, but a zone can be used for many network connections.
