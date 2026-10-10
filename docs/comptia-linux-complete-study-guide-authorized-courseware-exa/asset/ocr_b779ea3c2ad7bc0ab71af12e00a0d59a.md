# # Signing Messages and Verifying Signatures

As noted earlier, GPG can be used to sign messages so that recipients know they come from you. To do so, use the `--sign` or `--clearsign` option to gpg:

```
```
$ gpg --clearsign original-file
```
```

The `--sign` option creates a new file with the same name as the original, but with `.gpg` appended to the filename. This file is encrypted using your private key, so that it may only be decrypted with your public key. This means that anybody with your public key may read the message, but anybody who can read it knows it’s from you. The `--clearsign` option works similarly, but it leaves the message text unencrypted and only adds an encrypted signature that can only be verified using your public key. The `--clearsign` option creates a file with a name that ends in `.asc`.

If you receive a signed message, you can verify the signature using the `--verify` option to gpg:

```
```
$ gpg --verify received-file
```
```

If any of the keys in your keyring can decode the message or verify the signature, gpg displays a `Good signature` message. To read a message that was encrypted via the `--sign` option, you must decrypt the message via the `--decrypt` option, as described earlier.

# # Summary

Maintaining system security is both important and time-consuming. A great deal of security emphasis is on network security, and for this, configuring your super server and disabling unused servers will go a long way. Attending to passwords and performing miscellaneous tasks to keep your local accounts from becoming security risks are also important security tasks.

Encryption is a hot topic in security. SSH is a protocol and tool that can handle many network encryption tasks by encrypting two-way connections between computers. Typically used as a remote login protocol, SSH can also be used to transfer files or encrypt other protocols. When you want to encrypt data sent to another individual via a tool such as e-mail, you can do so with the help of GPG. This package enables you to encrypt individual files, which can then be attached to or embedded in e-mail messages and decrypted by the recipient.