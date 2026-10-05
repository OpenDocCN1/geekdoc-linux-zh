# Chapter 17 DNS: The Domain Name System

source addresses alone. TSIG can secure zone transfers from a master server
its slaves, and in BIND can secure dynamic updates.

The TSIG signature on a message authenticates the peer and verifies that the data
has not been tampered with. Signatures are checked at the time a packet is re-
cieved and not discarded; they are not cached and do not become part of the
DNS data.

TSIG uses symmetric encryption. That is, the encryption key is the same as the
deryption key. This single key is called the “shared secret.” The TSIG specifica-
tion allows multiple encryption methods. BIND implements MD5, SHA-1, SHA-
224, and SHA-256. NSD implements the same set but without SHA-224. Using a
different key for each pair of servers that want to communicate securely.

TSIG is much less expensive computationally than public key cryptography,
because it requires manual configuration, it is only appropriate for a local network
on which the pairs of communicating servers is small. It does not scale
to the Global Internet.

# Setting up TSIG for BIND

First, BIND’s dnssec-keygen utility to generate a shared-secret host key for
two servers, master and slave:1:

```
$ dnssec-keygen -a HMAC-MD5 -b 128 -n HOST master-slave1
```

The -b 128 flag tells dnssec-keygen to create a 128-bit key. We use 128 bits here
to keep the keys short enough to fit on our printed pages. In real life, you
might want to use a longer key; 512 bits is the maximum allowed.

This command produces two files: Master-slave1.157+09068.private and
Master-slave1.157+09068.key. The 157 stands for the HMAC-MD5 algo-
rith, and the 09068 is a number used as a key identifier in case you have multi-
keys for the same pair of servers.26

Both files include the same key, in different formats. The .private key file looks
like this:

```
Private-key-format: v1.2
Algorithm: 157 (HMAC_MD5)
Key: jxopeb+Ac71Mm2vc9R9g==
```

and the .key file like this:

```
master-slave1. IN KEY 512 3 157 jxopeb+Ac71Mm2vc9R9g==
```

Note that dnssec-keygen has added a dot to the end of the key names in both
filenames and the contents of the .key file. The motivation for this is
that dnssec is used for DNSSEC keys that are added to zone files,
the key names must be fully qualified domain names and must end in a

26. The number looks random, but it is really just a hash of the TSIG key.