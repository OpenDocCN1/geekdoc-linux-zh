You may already recognize the algorithms used to verify package integrity:

+   - **rsa** Named for its creators, Rivest, Shamir, and Adleman, it's a public key encryption algorithm.
+   - **sha1** A 160-bit message digest Secure Hash Algorithm; a cryptographic hash function.
+   - **md5** Message Digest 5, a cryptographic hash function.
+   - **pgp** PGP, as implemented in Linux by GPG.

# File Verification

The verification of an installed package compares information about that package with information from the RPM database on a system. The --verify (or -v) switch checks the size, MD5 checksum, permissions, type, owner, and group of each file in the package. Verification can be done in a number of ways. Here are a few examples:

+   - Verify all files. Naturally, this may take a long time on your system. (Of course, the rpm -Va command performs the same function.)
+   - Verify all files within a package against a downloaded RPM.
+   - Verify a file associated with a particular package.

```
# rpm --verify -a
```

```
# rpm --verify -p vsftpd-2.2.2-6.el6.i686.rpm
```

```
# rpm --verify --file /bin/ls
```

If the integrity of the files or packages is verified, you will see no output. Any output means that a file or package is different from the original. There's no need to panic if certain changes appear; after all, administrators do edit configuration files. There are eight tests. If there's been a change, the output is a string of up to eight failure code characters, each of which tells you what happened during each test. If you see a dot (.), that test passed. The following example shows /bin/vi with an incorrect group ID assignment:

```
# rpm --verify --file /bin/vi
```

```
.....G  /bin/vi
```

Table 7-4 lists the failure codes and their meanings.