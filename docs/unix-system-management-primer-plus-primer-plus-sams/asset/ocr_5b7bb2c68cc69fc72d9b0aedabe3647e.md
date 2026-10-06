# 38 UNIX SYSTEM MANAGEMENT PRIMER PLUS

New userid: "Joe User <joeuser@example.com>".
New signature from keyID 0XA38C5D0 on userid Joe User <joeuser@example.com>

Added :

+   - new key(s)
- new signatures(s)
- new user ID(s)

# Listing Your Key Ring Contents

You can list the contents of your key ring by typing ppg -kv. Some people have many email addresses, and you can use this command if you forget under which person's key was registered in your key ring.

Nancy now sign Joe's public key, which verifies that the public key is Joe's. Otherwise PGP constantly warns you that the public key has not been proven to belong to Joe. ppg -ks signs the keys, as follows:

```
bash ppg -ks joeuser@example.com
Pretty Good Privacy(tm) Version 6.5.8
(c) 1999 Network Associates Inc.
Uses the RSAREF(tm) Toolkit, which is copyright RSA Data Security, Inc.
Export of this software may be restricted by the U.S. government.
```

A secret key to make a signature.
You specified no user ID to select your secret key, using default signing key set, otherwise the default user ID and will be the most recently added key on your secret keyring.
Key for user ID: Joe User <joeuser@example.com>
1024-bit DSS key 0XA38C5D0, created 2002/04/20

```
Key fingerprint = 0A 16 68 8B FD D9 0F 01 ID EF 08 AD 12 53 64 6E C
```

READFULLY: Based on your direct first-hand knowledge, you absolutely certain that you are prepared to solemnly certify that the above public key actually belongs to the user specified by the above user ID (y/N)? y
You need a phrase to unlock your secret key.
Key for user ID "nancy@example.com"
Enter pass phrase:
Passphrase is good

Finally, Nancy now can encrypt a file with Joe's public key using ppg -ea (the a is necessary to store the encrypted file in ASCII format for email transport). The syntax of ppg -ea is as-follows:

ppg -ea file userid [other users]
If If Nancy wants to encrypt each message, the command to encrypt it with Joe's public-key would look like this:

```
bash ppg -ea message joeuser@example.com
Pretty Good Privacy(tm) Version 6.5.8
(c) 1999 Network Associates Inc.
```