
you can accept most keys from public servers or known sites as valid, though it is easy to check their posted fingerprints. Once assured of the key's validity, you can then sign it with your private key. Signing a key notifies gpg that you officially accept the key.

To sign a key, you use the gpg command with the --sign-key command and the key's name.

```
gpg --sign-key george@rabbit
```

Alternatively, you can edit the key with the --edit-key command to start an interactive session in which you can enter the command sign to sign the key and save to save the change. Signing a key involves accessing your private key, so you will be prompted for your passphrase. When you are finished, leave the interactive session with the quit command.

Normally, you would want to post a version of your public key that has been signed by one or more users. You can do the same for other users. Signing a public key provides a way to vouch for the validity of a key. It indicates that someone has already checked it out. Many different users could sign the same public key. For a key that you have received from another user, and that you have verified, you can sign and return the signed version to that user. Once you have signed the key, you can generate a file containing the signed public version. You can then send this file to the user. This process builds a Web-of-Trust where many users vouch for the validity of public keys.

```
gpg -a --export george@rabbit --output georgesig.asc
```

The user would then import the signed key and export it to a keyserver.

## Tip

If you want to start over from scratch, you can just erase your .gnupg directory, though this is a drastic measure, as you will lose any keys you have collected.

## Using GnuPG

GnuPG encryption is currently supported by KMail and exmh mail clients. You can also use the GNU Privacy Assistant (GPA), a GUI front end, to manage GPG tasks. You can use the gpg command to manually encode and decode messages, including digital signatures if you wish. As you perform GPG tasks, you will need to reference the keys you have using their key names. Bear in mind that you only need a unique identifying substring to select the key you want. GPG performs a pattern search on the string you specify as the key name in any given command. If the string matches more than one key, all those matching will be selected. In the following example, the "Sendmail" string selects matches on the identities of two keys.

```
# gpg --list-keys "Sendmail"
pub 1024R/CC374F2D 2000-12-14
    Sendmail Signing Key/2001 <sendmail@Sendmail.ORG>
pub 1024R/E35C5635 1999-12-13
    Sendmail Signing Key/2000 <sendmail@Sendmail.ORG>
```

## Encrypting Messages

The gpg command provides several options for managing secure messages. The e option encrypts messages, the a option generates an armored text version, and the s option adds a digital signature. You will need to specify the recipient's public key, which you should already have imported into your pubring file. It is this key that is used to encrypt the message. The recipient will then be able to decode the message with their private key. Use the --recipient or -r option to specify the name of the recipient key. You can use any unique substring in the user's public key name. The e-mail address usually suffices. You use the d option to decode received messages. In the following example, the user encrypts (e) and signs (s) a file generated in armored text format (a). The -r option indicates the recipient for the message (whose public key is used to encrypt the message).

```
gpg -e -s -a -o myfile.asc -r george@rabbit.mytrek.com myfile
# mail george@rabbit.mytrek.com < myfile.asc
```

You can leave out the ASCII armor option if you want to send or transfer the file as a binary attachment. Without --armor or -a options, gpg generates an encoded binary file, not an encoded text file. A binary file can be transmitted through e-mail only as an attachment. As noted previously, ASCII armor versions usually have an extension of .asc, whereas binary version use .gpg.

## Decrypting Messages

When the other user receives the file, they can save it to a file named something like myfile.asc and then decode the file with the -d option. The -o option will specify a file to save the decoded version in. GPG will automatically determine if it is a binary file or an ASCII armor version.

```
gpg -d -o myfile.txt myfile.asc
```

To check the digital signature of the file, you use the gpg command with the --verify option. This assumes that the sender has signed the file.

```
gpg --verify myfile.asc
```

## Decrypting a Digital Signature

You will need to have the signer's public key to decode and check the digital signature. If you do not, you will receive a message saying that the public key was not found. In this case, you will first have to obtain the signer's public key. You could access a key server that you think may have the public key, or request the public key directly from a Web site or from the signer. Then import the key as described previously.

## Signing Messages

You do not have to encrypt a file to sign it. A digital signature is a separate component. You can either combine the signature with a given file or generate one separately. To combine a signature with a file, you generate a new version that incorporates both. Use the --sign or -s option to generate a version of the document that includes the digital signature. In the following example, the mydoc file is digitally signed with mydoc.gpg file containing both the original file and the signature.

```
gpg -o mydoc.gpg --sign mydoc
```

If, instead, you want to just generate a separate signature file, you use the --detach-sig command. This has the advantage of not having to generate a complete copy of the original file. That file remains untouched. The signature file usually has an extension like .sig. In the following example, the user creates a signature file called mydoc2.sig for the mydoc2 file.

```
gpg -o mydoc2.sig --detach-sig mydoc2
```

To verify the file using a detached signature, the recipient user specifies both the signature file and the original file.

```
gpg --verify mydoc2.sig mydoc2
```

You could also generate a clear sign signature to be used in text files. A clear sign signature is a text version of the signature that can be attached to a text file. The text file can be further edited by any text editor. Use the --clearsign option to create a clear sign signature. The following example creates a clear signed version of a text file called mynotice.txt.

```
gpg -o mysignnotice.txt --clearsign mynotice.txt
```

Note Numerous GUI frontends and filters available for GNU PG at www.gnupg.org. GPA (GNU Privacy Assistant) provides a GNOME-based frontend to easily encrypt and decrypt

## Tip

Steganography is a form of encryption that hides data in other kinds of objects, such as images. You can use JPEG Hide and Seek software (JPHS) to encode and retrieve dct

![](img/32a48d8db4c23e6e2eb70d1e5034c976_372_0.png)

## ABC Amber CHM Converter Trial version

Please register to remove this banner.

http://www.processestext.com/abchm.html

## Checking Software Package Digital Signatures

One very effective use for digital signatures is to verify that a software package has not been tampered with. It is possible that a software package could be intercepted in transmission and some of its system-level files changed or substituted. Software packages from your distribution, as well as those by reputable GNU and Linux projects, are digitally signed. The signature provides modification digest information with which to check the integrity of the package. The digital signature may be included with the package file or posted as a separate file. You use the gpg command with the --verify option to check the digital signature for a file.

Tip Red Hat will install the Red Hat public key in the RPM documentation directory in a file called RPM-GPG-KEY. /usr/share/doc/rpm-4.1. Red Hat uses this key to check RPM packages during installation.

## Importing Public Keys

First, however, you will need to make sure that you have the signer's public key. The digital signature was encrypted with the software distributor's private key. That distributor is the signer. Once you have that signer's public key, you can check any data you receive from them. In the case of a software distributor, once you have their public key, you can check any software they distribute. To obtain the public key, you can check a key server or, more likely, check their Web site. As noted previously, you can download the Red Hat public key from the Red Hat Web site security resources page or use the version installed in the RPM documentation directory. Once you have obtained the public key, you can add to your keyring with the --import option, specifying the name you gave to the downloaded key file (in this case, myredhat.asc):

```bash
# gpg --import redhat.asc
gpg: key CBA29BF9: public key imported
gpg: Total number processed: 1
gpg: imported: 1 (RSA: 1)
```

To download from a keyserver instead, you use the --keyserver option and the keyserver name.

To import the Red Hat public key from the RPM directory, you would specify the RPM-GPG-KEY file. This is the key provided by the Red Hat distribution on your CD-ROMs. Though used during installation, the key has to be imported to verify packages again after they have been installed.

```bash
rpm --import /usr/share/doc/rpm-4.1/RPM-GPG-KEY
```

## Validating Public Keys

You can use the --fingerprint option to check a key's validity if you wish. If you are confident that the key is valid, you can then sign it with the --sign-key command. In the following example, the user signs the Red Hat key, using the string "Red Hat" in the key's name to reference it. The user is also asked to enter his passphrase to allow use of his private key to sign the Red Hat public key.

```bash
# gpg --sign-key "Red Hat"
pub 1024R/CBA29BF9 created: 1996-02-20 expires: never trust: -/q
(1). Red Hat Software, Inc. <redhat@redhat.com>
pub 1024R/CBA29BF9 created: 1996-02-20 expires: never trust: -/q
Fingerprint: 6D 9C BA DF D9 60 52 06 23 46 75 4E 73 4C FB 50
Red Hat Software, Inc. <redhat@redhat.com>

Are you really sure that you want to sign this key
with your key: "Richard Petersen (author) <richlp@turtle.mytrek.com>"
Really sign? yes
You need a passphrase to unlock the secret key for
```
