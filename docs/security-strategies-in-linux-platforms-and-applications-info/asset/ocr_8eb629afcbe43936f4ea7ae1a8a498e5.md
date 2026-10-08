# PART 2 Layered Security and Linux

Once these changes are made, run the following command to create the Kerberos database. The directory with the command varies; if it is not in your PATH, look in directories such as /usr/sbin/ and /usr/kerberos/sbin/

```
# kdb5_util create
```

You'll be prompted with information that should match the default realm, along with the master password for the Kerberos database. If you forget that database password, you will have to delete the files in /var/lib/krb5kdc/ or /var/kerberos/krb5kdc/ directories (depending on distribution) before re-creating the database by rerunning this command.

Once the base database is available in the appropriate directory, its time to set up keytab files, which are pairs of Kerberos principals and clients. Once created, Kerberos authentication between the two systems works without a password. To start the process, run the kutil command which starts a kutil prompt. Most commands that you run at prompt are shown in the kutil man page.

At prompt, you can enter user-account information along with encryption keys. For example, the following add command to the kutil prompt adds michael as a Kerberos principal with the -p switch, a unique identity to a Kerberos server can assign tickets. The -k 1 specifies version number 1. The -e rc4-hmac specifies an encryption scheme, created by Ron Rivest. The rc4 stands for Ron's code, version 4. ("The Ron" is a reference to Ron Rivest, one of the developers behind the RSA algorithm for public key cryptography.) It's associated with the hash-based message authentication code (hmac).

```
kutil: add -password -p admin@EXAMPLE.ORG -k 1 -e rc4-hmac
kutil: add -password -p michael@EXAMPLE.ORG -k 1 -e rc4-hmac
```

In a similar fashion, you can set up different forms of encryption. The following commands set up version 1 for the Advanced Encryption Standard with 256 bits (aes256), with message processing using ciphertext text.

```
kutil: add -password -p admin@EXAMPLE.ORG
-k 1 -e aes256-ct
kutil: add -password -p michael@EXAMPLE.ORG
-k 1 -e aes256-ct
```

The keys can be written to a local keytab file. The following commands write it to the michael.keytab file in the local directory.

```
kutil: wkt michael.keytab
```

Once keytab files have been created for all desired users, the next step is to merge keytab files into the /etc/krb5.keytab file. First, the following commands read in keytab files for users michael and into local memory:

```
kutil: read_kt michael.keytab
kutil: read_kt donna.keytab
```