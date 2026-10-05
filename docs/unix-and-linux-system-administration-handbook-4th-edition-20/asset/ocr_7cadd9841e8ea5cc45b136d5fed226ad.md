# Key pair generation

libraries directly from openssl. If you take the latter route, you'll have to recompile BIND with cryptographic support turned on (use the --with-opens option to ./configure). If you do not do this, dnssec-keygen will complain. However, it will still be working for generating TSIG keys, since those don't require OpenSSL is so old that it has security vulnerabilities.

Two separate workflows are involved in using signed zones: one that creates keys and signs zones, and a second that serves the contents of those signed zones. These duties need not be implemented on the same machine. In fact, it is better to quarantine the private key and the CPU-intensive signing process on a machine that is not publicly accessible from the Internet. (Of course, the machine that serves the data must be visible to the Internet.)

The first step in setting DNSSEC is to organize your zones files so that all data files for a zone are in a single directory. The tools that manage DNSSEC expect this organization.

Next, enable DNSSEC on your servers with the named.conf options

```
options {
  dnssec-enable yes;
}
```

for authoritative servers and

```
options {
  dnssec-enable yes;
dnssec-validation yes;
}
```

for recursive servers. The dnssec-enable option tells your authoritative servers to include DNSSEC record set signatures in their responses when answering queries from DNSSEC-aware servers. The dnssec-validation option makes named verify the legitimacy of signatures it receives in from other servers.

# Key pair generation

You generate two key pairs for each zone you want to sign: a zone-signing (ZSK) pair and a key-signing (KSK) pair. Each pair consists of a public key and a private key. The KSK's private key signs the ZSK and creates a secure entry point for the zone. The ZSK's private key signs the zone's resource records. The public keys are then published to allow other sites to verify your signatures.

The BIND commands

```
$ dnssec-keygen -a RSASHA1 -b 1024 -n ZONE example.com
Kexample.com.+005+23301
$ dnssec-keygen -a RSASHA1 -b 2048 -n ZONE -f KSK example.com
Kexample.com.+005+00682
```