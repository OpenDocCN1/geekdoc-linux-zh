# Using DNS Security Extensions

DNS Security Extensions (DNSSEC), a set of security extensions to the DNS protocol, provides data integrity and authentication by using cryptographic digital signatures. It provides for the storage of public keys in the DNS and their use for verifying transactions. DNSSEC still isn't widely deployed, but BIND 9 does support it for interserver transactions (zone transfers, NOTIFY, recursive queries, dynamic updates). It is worth configuring the *transaction signature (TSIG)* if your slaves also run BIND 9. We briefly discuss using TSIG for authenticated zone transfers here.

To begin, we use `dnssec-keygen`, as we did with `rndc`, to generate a shared secret key. This key is stored on both the master and slave servers. As before, we extract the Key: data from the `.private` file. The following command creates a 512-bit host key named `transfer`:

```
```
$ dnssec-keygen -a hmac-md5 -b 512 -n host transfer
```
```

Next we set up matching key statements in `named.conf` for both the master and slave servers (similar to the contents of the `/etc/rndc.key` file created earlier). Remember not to transfer the secret key from one machine to the other over an insecure channel. Use `ssh`, `sftp` (secure FTP), or something similar. Remember also that the shared secrets shouldn't be stored in world-readable files. The statements, identical on both machines, would look something similar to this:

```
```
key transfer {
    algorithm "hmac-md5";
    secret "...";    # Key from .private file
};
```
```

Finally, we set up a `server` statement on the master to instruct it to use the key we just created when communicating with the slave, and to enable authenticated zone transfers with the appropriate `allow-transfer` directives:

```
```
server 192.0.2.96 {
    key { transfer; };
};
```
```

The BIND 9 ARM contains more information on TSIG configuration and DNSSEC support in BIND.