# Encrypting and Signing Files with GnuPG 551

5. Type a long phrase that includes lower- and uppercase letters, numbers, and punctuation marks — the longer the better — and then press Enter.

Careful tough; pick a passphrase that you can easily remember.

GPG generates the keys. It may ask you to perform some work on the PC so that the random number generator can generate enough random numbers for the key-generation process.

# Exchanging keys

To communicate with others, you have to give them your public key. You also have to get public keys from those who may send you a message (or someone might sign a file and you want to verify the signature). GPG keeps public keys in your key ring. To list the keys in your key ring, type

```
gpg --list-keys
```

To send your public key or place it on a Web site, you have to export the key to a file. The best way is to put the key in what GPG calls ASCII-armored format with a command like this:

```
gpg --armor --export naba@comcast.net > nabakey.asc
```

This command saves your public key in an ASCII-armored format (it basically looks like garbled text) in the file named nabakey.asc. Of course, you replace the e-mail address with your e-mail address (the one you used when you created the key) and the output filename

After you export the public key to a file, you can mail that to others or place it on a Web site for others.

When you import a key from someone else, you typically get it in an ASCII-armored format as well. For example, if you have a fedora@redhot.com GPG public key in a file fedorak.asc, I import it into my key ring with the following command:

```
gpg --import fedorak.asc
```

Use the gpg --list-keys command to verify that the key is in your key ring. For example, here is what I see when I type gpg --list-keys on my system:

```
gpg: see http://www.gnupg.org/faq.html for more information
/home/naba1024/gnupg/pubring.gpg

pub 1024/0192123 2004-04-15 Naba Barkakati <naba@comcast.net>
sub 1024/601AE988 2004-04-15
```