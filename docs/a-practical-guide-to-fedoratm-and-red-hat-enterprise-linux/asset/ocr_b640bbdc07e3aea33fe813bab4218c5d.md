When Sam gets the file he decrypts it, sending the output (the decrypted file) to memoC. Because the file was encrypted using Sam's public key, Sam must provide his private key to decrypt it. At the bottom of the output, `gpg` confirms that Max's signature is good.

```
$ gpg --output memoC_memoC.gpg

You need a passphrase to unlock the secret key for:
user: "Sam Smith (Sam the Great) <sam@example.com>"
2048-bit RSA key, ID 5698A710, created 2013-10-03 (main key ID D26C84B3)
Enter passphrase:

`gpg`: encrypted with 2048-bit RSA key, ID 5698A710, created 2013-10-03
"Sam Smith (Sam the Great) <sam@example.com>"
`gpg`: Signature made Thu 03 Oct 2013 12:50:51 PM PDT using RSA key ID 643E62B8
`gpg`: Good signature from "Max Wild <max@example.com>"
```

# # SIGNING A PUBLIC KEY

If you trust that a public key belongs to the person it says it belongs to, you can sign that key to make it more trustworthy. The more people who sign a key, the more trustworthy it becomes.

A key ID identifies a key. You can use the `gpg --list-key` option to list the IDs of all the keys on your keyring. The following output shows that Sam's key is 2,048 bits long, uses RSA encryption (R), and has a key ID of D26C84B3.

```
$ gpg --list-key
/home/max/.gnupg/pubring.gpg
-

pub   2048R/D26C84B3 2013-10-03
uid          Sam Smith (Sam the Great) <sam@example.com>
sub   2048R/5698A710 2013-10-03
```

Before you sign a key, make sure it belongs to the person it says it belongs to. Download the key from several sources (e.g., keyservers). Each key has a unique fingerprint that you can use to identify that key. Use the `gpg --fingerprint` option followed by the key ID to display the fingerprint of a key and compare the fingerprints.

```
[max@gugava -]$ gpg --fingerprint D26C84B3
pub   2048R/D26C84B3 2013-10-03
        Key fingerprint = 036A DE6E D653 3769 B243 A9EF 286A C3E0 D26C 84B3
uid          Sam Smith (Sam the Great) <sam@example.com>
sub   2048R/5698A710 2013-10-03
```

Check that the fingerprint is correct by comparing it to one supplied by the person who owns it. Use a keyserver, the phone, or a printout, not email, to verify the fingerprint. Once you are sure you have a valid key you can sign it using the `gpg --sign-key` option followed by the key ID you have just verified. Following, Max signs the copy of Sam's public key that is on Max's keyring.