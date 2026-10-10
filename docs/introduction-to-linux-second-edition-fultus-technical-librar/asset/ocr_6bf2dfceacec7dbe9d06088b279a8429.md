```
gpg --export -a
```

However, as far is this guide is concerned, we assume that you only need your key in order to encrypt and decrypt data for yourself. Read the gpg man pages if you want to know more.

# 9.4.4 Encrypt data

Now you can encrypt a .tar archive or a compressed archive, prior to saving it to a backup medium or transporting it to the backup server. Use the gpg command like this:

```
gpg -e -r (part of) uidarchive
```

The -e option tells gpg to encrypt, the -r option indicates who to encrypt for. Keep in mind that only the user name(s) following this -r option will be able to decrypt the data again. An example:

```
willy@ubuntu:~$ gpg -e -r Willy /var/tmp/home-willy-20060808.tar
```

# 9.4.5 Decrypting files

Using the -d option, you can decrypt files that have been encrypted for you. The data will scroll over your screen, but an encrypted copy will remain on disk. So for file formats other than plain text, you will want to save the decrypted data, so that you can view them with the appropriate program. This is done using the -o option to the gpg command:

```
willy@ubuntu:~$ gpg -d -o /var/tmp/home-willy-decrypt.tar /var/tmp/home-willy-20060808.tar.gpg
```

You need a passphrase to unlock the secret key for user: "Willy De Wandel (Willem) <wdwmwg.vl>" 4096 ELG-E key, ID A3449CF7, created 2006-08-08 (main key ID BF5C3DBB)

```
gpg: encrypted with 4096-bit ELG-E key, ID A3449CF7, created 2006-08-08 "Willy De Wandel (Willem) <wdwmwg.vl>"
```

![](bbox=[0.05, 0.95, 0.1, 1.0])

# No password = no data

If you can not remember your password, the data is lost. Not even the system administrator will be able to decrypt the data. That is why a copy of important keys is sometimes kept in a sealed vault in a bank.

# 9.5 Summary

Here's a list of the commands involving file backup: