
Table 16-1: GPG Commands and Options

| GPG Commands | Description |
|---|---|
| `--edit-key name` | Edits your keys. Use commands to perform most key operations such as `sign` to sign a key or `passwd` to change your passphrase. |
| `--sign-key name` | Signs a public key with your private key. Same as `sign` in `--edit-key`. |
| `--delete-key name` | Removes a public key from the public keyring. |
| `--delete-secret-key name` | Removes private and public keys from both the secret and public keyrings. |
| `--gen-revoke` | Generates a revocation certificate for your own key. |
| `--export [names]` | Exports a specified key from your keyring. With no arguments, exports all keys. |
| `--send-keys [names]` | Exports and sends specified keys to a keyserver. The option `--keyserver` must be used to give the name of this keyserver. |
| `--import [files]` | Imports keys contained in files into your public keyring. |

| GPG Options | Description |
|---|---|
| `-a, --armor` | Creates ASCII armored output, ASCII version of encrypted data. |
| `-o, --output file` | Writes output to a specified file. |
| `--default-key name` | Specifies the default private key to use for signatures. |
| `--keyserver site` | The keyserver to look up public keys not on your keyring. Can also specify the site to send your public key to. `host -l pgp.net | grep www.keys` will list the keyservers. |
| `-r, --recipient names` | Encrypts data for the specified user, using that user's public key. |
| `--default-recipient names` | Specifies the default recipient to use for encrypting data. |

## GnuPG Setup:gpg

Before you can use GnuPG, you will have to generate your private and public keys. On the command line (terminal window), enter the `gpg` command with the `--gen-key` command. The `gpg` program will then prompt you with different options for creating your private and public keys. You can check the `gpg` Man page for information on using the `gpg` program.

```
gpg --gen-key
```

## Creating Your Key

You are first asked to select the kind of key you want. Normally, you would just select the default entry, which you can do by pressing the ENTER key. Then you choose the key size, usually the default 1024. You then specify how long the key is to be valid-usually, there is no expiration. You will be asked to enter a user ID, comment, and e-mail address. Press ENTER to be prompted for each in turn. These elements, any of which can be used as the key's name, identify the key. You use the key name when performing certain GPG tasks such as signing a key or creating a revocation certificate. For example, the following elements create a key for the user richlp with the comment "author" and the e-mail address richlp@turtle.mytrek.com:

```
Richard Petersen (author) <richlp@turtle.mytrek.com>
```

You can use any unique part of a key's identity to reference that key. For example, the string "Richard" would reference the preceding key, provided there are no other keys that have the string "Richard" in them. "richlp" would also reference the key, as would "author". Where a string matches more than one key, all the matched ones would be referenced.

## Protecting Your Key

The gpg program will then ask you to enter a passphrase, used to protect your private key. Be sure to use a real phrase, including spaces, not just a password. gpg then generates your public and private keys and places them in the .gnupg directory. The private keys are kept in a file called secring.gpg in your .gnupg directory. The public key is placed in the pubring.gpg file, to which you can add the public keys of other users. You can list these keys with the --list-keys command.

In case you later need to change your keys, you can create a revocation certificate to notify others that the public key is no longer valid. For example, if you forget your password or someone else discovers it, you can use the revocation certificate to tell others that your public key should no longer be used. In the next example, the user creates a revocation certificate for the key richlp and places it in the file myrevoke.asc:

```
gpg --output myrevoke.asc --gen-revoke richlp
```

## Making Your Public Key Available

For other users to decrypt your messages, you have to make your public key available to them. They, in turn, have to send you their public keys so that you can decrypt any messages you receive from them. In effect, enabling encrypted communications between users involves all of them exchanging their public keys. The public keys then have to be verified and signed by each user who receives them. The public keys can then be trusted to safely decrypt messages.

If you are sending messages to just a few users, you can manually e-mail them your public key. For general public use, you can post your public key on a keyserver, which anyone can then download and use to decrypt any message they receive from you. The OpenPGP Public Keyserver is located at www.keyserver.net, which is listed in your .gnupg/options file. You can send directly to the keyserver with the --keyserver option and --send-key command. The --send-key command takes as its argument your e-mail address. You need to send to only one keyserver, as it will share your key with other keyservers automatically.

```
gpg --keyserver search.keyserver.net --send-key chris@turtle.mytrek.com
```

If you want to send your key directly to another user, you should generate an armored text version of the key that you can then e-mail. You do this with the --armor and --export options, using the --output option to specify a file to place the key in. The --armor option will generate an ASCII text version of the encrypted file so that it can be e-mailed directly, instead of as an attached binary. Files that hold an ASCII encoded version of the encryption normally have the extension .asc, by convention. Binary encrypted files normally use the extension .gpg. You can then e-mail the file to users you want to send encrypted messages.

```
# gpg --armor --export richlp@turtle.mytrek.com --output richlp.asc
# mail -s 'mypubkey' george@rabbit.mytrek.com < richlp.asc
```

Many companies and institutions post their public key files on their Web sites, where they can be downloaded and used to verify encrypted software downloads or official announcements.

Note Some commands and options for GPG have both a long and short form. For example, the --armor command can be written as -a, --output as -o, --sign as -s, and --encrypt

## Obtaining Public Keys

To decode messages from other users, you will need to have their public keys. They can either send them to you or you can download them from a keyserver. Save the message or Web page containing the public key to a file. You will then need to import, verify, and sign the key. Use the file you received to import the public key to your **pubring** file. In the following example, the user imports George's public key, which he has received as the file **georgekey.asc**.

```
gpg --import georgekey.asc
```

All Linux distribution sites have their own public keys available for download. You should, for example, download the Red Hat public key, which can be accessed from the Red Hat site on its security resources page (**www.redhat.com**). Click the Public Encryption Key link. From there, you can access a page that displays just the public key. You can save this page as a file and use that file to import the Red Hat public key to your keyring. (Your Red Hat distribution also places the Red Hat public key in the **/usr/share/doc/rpm4-1** directory with versions for both GPG and PGP encryption, **RPM-GPG-KEY** and **RPM-PGP-KEY** files.) In the following example, the user saved the page showing just the Red Hat public key as **myredhat.asc**, and then imported that file:

```
gpg --import myredhat.asc
```

Note You can remove any key, including your own private key, with the --delete-key and --delete-secret-key commands.

## Validating Keys

To manually check that a public key file was not modified in transit, you can check its fingerprint. This is a hash value generated from the contents of the key, much like a modification digest. Using the --fingerprint option, you can generate a hash value from the key you installed, then contact the sender and ask them what the hash value should really be. If they are not the same, you know the key was tampered with in transit.

```
gpg --fingerprint george@rabbit
```

You do not have to check the fingerprint to have gpg operate. This is just an advisable precaution you can perform on your own. The point is that you need to be confident that the key you received is valid. Normally
