By contrast, if RPM cannot find the appropriate key to verify the signature of a package, you will get this warning:

```
warning: V3 DSA signature: NOKEY, key ID 0352860f
```

GnuPG signatures are digital signatures that are very hard to forge. Signatures are created with a unique secret key and can be verified by their recipient using a public key. A digital signature timestamps a document so that if anyone tries to tamper or modify it, the verification of the signature will fail.

# Red Hat GNU Privacy Guard (GPG) Keys

To install Red Hat's GPG keys on your installed system, issue the following command:

```
# rpm --import /usr/share/rhn/RPM-GPG-KEY
```

or, use the following, to install them from CD-ROM (make sure you've got the right one in the drive):

```
# rpm --import /mnt/cdrom/RPM-GPG-KEY
```

These commands will install Red Hat's public GPG keys onto your system. You can also import other vendors, GnuPG keys in much the same way; just change the name of the file to the one that they've supplied to you.

To display a list of all GnuPG keys installed for RPM package verification on your system, issue the following command:

```
# rpm -qa gpg-pubkey*
gpg-pubkey-db42a60e-37ea5438
```

This will return a list of results. If you've installed the Red Hat key, you should see the following listed amongst them:

```
gpg-pubkey-db42a60e-37ea5438
```

We can get even more complete details of a Red Hat GPG key by executing the following command:

```
# rpm -qi gpg-pubkey-db42a60e-37ea5438
```

In the above command, note that gpg-pubkey-db42a60e-37ea5438 is the name of the Red Hat GnuPG key, gathered from the output of the command rpm -qa gpg-pubkey*.