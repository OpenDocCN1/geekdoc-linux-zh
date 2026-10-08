To check the digital signature of the file, you use the `gpg` command with the `--verify` option. This assumes that the sender has signed the file.

```
$ gpg --verify myfile.asc
```

# **Decrypting a Digital Signature**

You will need to have the signer’s public key to decode and check the digital signature. If you do not, you will receive a message saying that the public key was not found. In this case, you will first have to obtain the signer’s public key. You could access a keyserver that you think may have the public key, or request the public key directly from a Web site or from the signer. Then import the key as described previously.

# **Signing Messages**

You do not have to encrypt a file to sign it. A digital signature is a separate component. You can either combine the signature with a given file or generate one separately. To combine a signature with a file, you generate a new version that incorporates both. Use the `--sign` or `-s` option to generate a version of the document that includes the digital signature. In the following example, the `mydoc` file is digitally signed with the `mydoc.gpg` file containing both the original file and the signature.

```
$ gpg -o mydoc.gpg --sign mydoc
```

If, instead, you want to just generate a separate signature file, you use the `--detach-sig` command. This has the advantage of not having to generate a complete copy of the original file. That file remains untouched. The signature file usually has an extension like `.sig`. In the following example, the user creates a signature file called `mydoc2.sig` for the `mydoc2` file.

```
$ gpg -o mydoc2.sig --detach-sig mydoc2
```

To verify the file using a detached signature, the recipient user specifies both the signature file and the original file.

```
$ gpg --verify mydoc2.sig mydoc2
```

To verify a trusted signature you can use `gpgv`.

You could also generate a clear sign signature to be used in text files. A *clear sign* signature is a text version of the signature that can be attached to a text file. The text file can be further edited by any text editor. Use the `--clearsign` option to create a clear sign signature. The following example creates a clear signed version of a text file called `mynotice.txt`.

```
$ gpg -o mysignature.txt --clearsign mynotice.txt
```

> **NOTE** Numerous GUI front ends and filters are available for GnuPG at www.gnupg.org. GPA (GNU Privacy Assistant) provides a GNOME-based front end to easily encrypt and decrypt files. You can select files to encode, choose the recipients (public keys to use), and add a digital signature if you wish. You can also use GPA to decode encoded files you receive. You can also manage your collection of public keys—the keys in your keyring file.