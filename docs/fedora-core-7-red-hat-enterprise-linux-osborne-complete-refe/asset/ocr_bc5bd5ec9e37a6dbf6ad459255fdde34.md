If you are sending messages to just a few users, you can manually e-mail them your public key. For general public use, you can post your public key on a keyserver, which anyone can then download and use to decrypt any message they receive from you. A keyserver can be accessed using e-mail, LDAP, or the HTTP Horowitz Keyserver Protocol (HKP). The OpenPGP Public Keyserver project is located at pks.sourceforge.net. Several public keyservers are available. http://subkeys.pgp.net is listed in your .gnupg/gpg.conf file, though commented out. You can send directly to the keyserver with the --keyserver option and --send-key command. The --send-key command takes as its argument your e-mail address. You need to send to only one keyserver, as it will share your key with other keyservers automatically.

```
gpg --keyserver search.keyserver.net --send-key chris@turtle.mytrek.com
```

If you want to send your key directly to another user, you should generate an armored text version of the key that you can then e-mail. You do this with the --armor and --export options, using the --output option to specify a file to place the key in. The --armor option will generate an ASCII text version of the encrypted file so that it can be e-mailed directly, instead of as an attached binary. Files that hold an ASCII-encoded version of the encryption normally have the extension .asc, by convention. Binary encrypted files normally use the extension .gpg. You can then e-mail the file to users to whom you want to send encrypted messages.

```
# gpg --armor --export richlp@turtle.mytrek.com --output richlp.asc
# mail -s 'mypublickey' george@rabbit.mytrek.com < richlp.asc
```

Many companies and institutions post their public key files on their Web sites, where they can be downloaded and used to verify encrypted software downloads or official announcements.

> **NOTE** *Some commands and options for GPG have both long and short forms. For example, the --armor command can be written as -a, --output as -o, --sign as -s, and --encrypt as -e. Most others, like --export, have no short form.*

# Obtaining Public Keys

To decode messages from other users, you will need to have their public keys. Either they can send them to you or you can download them from a keyserver. Save the message or Web page containing the public key to a file. You will then need to import, verify, and sign the key. Use the file you received to import the public key to your *pubring* file. In the following example, the user imports George’s public key, which he has received as the file *georgekey.asc*.

```
gpg --import georgekey.asc
```

All Linux distribution sites have their own public keys available for download. You should, for example, download the Red Hat public key, which can be accessed from the Red Hat site on its security resources page (**www.redhat.com**). Click the Public Encryption Key link. From there, you can access a page that displays just the public key. You can save this page as a file and use that file to import the Red Hat public key to your keyring. (Your Red Hat distribution also places the Red Hat public key in the /usr/share/doc/rpm4-1 directory with versions for both GPG and PGP encryption, **RPM-GPG-KEY** and **RPM-PGP-KEY**.