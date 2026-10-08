
To check the digital signature of the file, you use the `gpg` command with the `--verify` option. This assumes that the sender has signed the file.

```bash
$ gpg --verify myfile.asc
```

## Decrypting a Digital Signature

You will need to have the signer’s public key to decode and check the digital signature. If you do not, you will receive a message saying that the public key was not found. In this case, you will first have to obtain the signer’s public key. You could access a keyserver that you think may have the public key, or request the public key directly from a Web site or from the signer. Then import the key as described previously.

## Signing Messages

You do not have to encrypt a file to sign it. A digital signature is a separate component. You can either combine the signature with a given file or generate one separately. To combine a signature with a file, you generate a new version that incorporates both. Use the `--sign` or `-s` option to generate a version of the document that includes the digital signature. In the following example, the `mydoc` file is digitally signed with the `mydoc.gpg` file containing both the original file and the signature.

```bash
$ gpg -o mydoc.gpg --sign mydoc
```

If, instead, you want to just generate a separate signature file, you use the `--detach-sig` command. This has the advantage of not having to generate a complete copy of the original file. That file remains untouched. The signature file usually has an extension like `.sig`. In the following example, the user creates a signature file called `mydoc2.sig` for the `mydoc2` file.

```bash
$ gpg -o mydoc2.sig --detach-sig mydoc2
```

To verify the file using a detached signature, the recipient user specifies both the signature file and the original file.

```bash
$ gpg --verify mydoc2.sig mydoc2
```

To verify a trusted signature you can use `gpgv`.

You could also generate a clear sign signature to be used in text files. A *clear sign* signature is a text version of the signature that can be attached to a text file. The text file can be further edited by any text editor. Use the `--clearsign` option to create a clear sign signature. The following example creates a clear signed version of a text file called `mynotice.txt`.

```bash
$ gpg -o mysignature.txt --clearsign mynotice.txt
```

> **NOTE** Numerous GUI front ends and filters are available for GnuPG at www.gnupg.org. GPA (GNU Privacy Assistant) provides a GNOME-based front end to easily encrypt and decrypt files. You can select files to encode, choose the recipients (public keys to use), and add a digital signature if you wish. You can also use GPA to decode encoded files you receive. You can also manage your collection of public keys—the keys in your keyring file.

> **Tip** Steganography is a form of encryption that hides data in other kinds of objects, such as images. You can use JPEG Hide and Seek software (PJHS) to encode and retrieve data in a JPEG image (*jphide* and *jpseek*). See linuxu01.gwgud.de/alatham/stego.html for more details.

## Checking Software Package Digital Signatures

One very effective use for digital signatures is to verify that a software package has not been tampered with. It is possible that a software package could be intercepted in transmission and some of its system-level files changed or substituted. Software packages from your distribution, as well as those by reputable GNU and Linux projects, are digitally signed. The signature provides modification digest information with which to check the integrity of the package. The digital signature may be included with the package file or posted as a separate file. You use the **gpg** command with the **--verify** option to check the digital signature for a file.

> **Tip** Fedora and Red Hat will install the Red Hat public key in the RPM documentation directory in a file called **RPM-GPG-KEY**.\$usr/share/doc/rpm-4.4.2. Fedora and Red Hat use this key to check RPM packages during installation. The version number will change with future RPM releases.

### Importing Public Keys

First, however, you will need to make sure that you have the signer’s public key. The digital signature was encrypted with the software distributor’s private key. That distributor is the signer. Once you have that signer’s public key, you can check any data you receive from them. In the case of software repositories like Fedora, **rpm.livna.org**, or **freshrpms.net**, you will be asked to install their public key the first time you try to install any software from their site. Once the key is installed, you do not have to install it again. With Yum, this is usually just a prompt to install the key, requesting a y or n confirmation, or a dialog requesting an OK click. Repositories like Livna and **freshrpms.net** will include their keys with their Yum configuration packages. You can also, if you wish, download and install them manually from their Web sites.

In the case of a software distributor, you can download their public key from their Web site or from their keyserver. Once you have their public key, you can check any software they distribute.

As noted previously, you can download the Red Hat public key from the Red Hat Web site security resources page or use the version installed in the **RPM** documentation directory. Once you have obtained the public key, you can add to your keyring with the **-import** option, specifying the name you gave to the downloaded key file (in this case, **myredhat.asc**):

```bash
# gpg --import redhat.asc
gpg: key CBA29BF9: public key imported
gpg: Total number processed: 1
gpg: imported: 1 (RSA: 1)
```

To download from a keyserver instead, you use the **--keyserver** option and the keyserver name.

To import the Red Hat public key from the RPM directory, you would specify the **RPM-GPG-KEY** file. This is the key provided by the Red Hat distribution on your DVD-ROM or CD-ROMs. Though used during installation, the key has to be imported to verify packages again after they have been installed.

```bash
# rpm --import /usr/share/doc/rpm-4.2.2/RPM-GPG-KEY
```

### Validating Public Keys

You can use the **--fingerprint** option to check a key's validity if you wish. If you are confident that the key is valid, you can then sign it with the **--sign-key** command. In the following example, the user signs the Red Hat key, using the string "Red Hat" in the key's name to reference it. The user is also asked to enter his passphrase to allow use of his private key to sign the Red Hat public key.

```bash
# gpg --sign-key "Red Hat"
# gpg 1024R/CBA29BF9  created: 1996-02-20  expires: never  trust: -/g
(1)  Red Hat Software, Inc. <redhat@redhat.com>
# gpg 1024R/CBA29BF9  created: 1996-02-20  expires: never  trust: -/g
Fingerprint: 6D 9C BA DF D9 60 52 06 23 46 75 4E 73 4C FB 50
Red Hat Software, Inc. <redhat@redhat.com>
# gpg Are you really sure that you want to sign this key
with your key: "Richard Petersen (author) <richlp@turtle.mytrek.com>"
Really sign? yes
You need a passphrase to unlock the secret key for
user: "Richard Petersen (author) <richlp@turtle.mytrek.com>"
1024-bit DSA key, ID 73F0A73C, created 2001-09-26
Enter passphrase:
# gpg
```

### Checking RPM Packages

RPM packages from any Yum repository such as Fedora will check the public key automatically. Should you download an RPM package separately, you can check the package manually. Once you have the software provider's public key, you can check any RPM software packages for Fedora or Red Hat with the **rpm** command and **-K** option. The following example checks the validity of the xcdroast software packages:

```bash
# rpm -K xcdroast-0.98alpha9-1.i386.rpm
xcdroast-0.98alpha9-1.i386.rpm: md5 OK
```

Many software packages in the form of compressed archives, **.tar.gz** or **.tar.bz2**, will provide signatures in separate files that end with the **.sig** extension. To check these, you use the **gpg** command with the **--verify** option. For example, the most recent Sendmail package is distributed in the form of a compressed archive, **.tar.gz**. Its digital signature is provided in a separate **.sig** file. First you would download and install the public key for Sendmail software obtained from the Sendmail Web site (the key may have the year as part of its name).

```bash
# gpg --import sendmail2006.asc
```

You should then sign the Sendmail public key that you just imported. In this example, the e-mail address was used for the key name.

```bash
# gpg --sign-key sendmail@Sendmail.ORG
```

You could also check the fingerprint of the key for added verification.
