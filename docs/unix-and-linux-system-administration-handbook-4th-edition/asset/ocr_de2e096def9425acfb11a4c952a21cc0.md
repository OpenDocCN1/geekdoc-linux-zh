As with access control lists, the *key-id* must be defined with a key statement before it is used. To associate the key with a particular server, just include *key-id* in the keys clause of that server’s server statement. The key is used both to verify requests from that server and to sign the responses to those requests.

The shared secret is sensitive information and should not be kept in a world-readable file. Use an include statement to bring it into the **named.conf** file.

# The trusted-keys statement

In theory, DNSSEC parent zones authenticate their child zones’ public keys, allowing signatures to be chain-authenticated all the way back to the DNS root. In practice, the root and top-level domains do not yet support DNSSEC, so some other method of validating a zone’s public keys is needed.

The trusted-keys statement is a brute-force way of telling **named**, “The proper public key for zone XXX.com is YYY,” thus bypassing the usual DNSSEC mechanisms for obtaining and verifying zone keys. Such a declaration is sometimes known as a “trust anchor.” It’s intended for use when a zone is signed but its parent zone is not.

Of course, XXX.com must be important enough to you site to merit this special treatment, and you must have some secure, out-of-band way to determine the proper value of the key. There’s no magic way to get the correct key; the foreign zone’s administrator has to read it to you over the telephone or send it to you in some other way that can be authenticated. An HTTPS secure web page is often used for this purpose. You must go through the whole process again whenever the key changes.

The format of the trusted-keys statement is

```
trusted-keys {
    domain flags protocol algorithm key;
    domain flags protocol algorithm key;
    ...
}
```

Each line represents the trust anchor for a particular domain. The *flags*, *protocol*, and *algorithm* are nonnegative integers. The *key* is a base-64-encoded string matching the DNSKEY resource record used to sign the zone.

DNSSEC is covered in more detail starting on page 648.

# The server statement

**named** can potentially talk to many servers, not all of which are running current software and not all of which are even nominally sane. The server statement tells **named** about the characteristics of its remote peers. The server statement can override defaults for a particular server; it’s not required unless you want to configure keys for zone transfers.