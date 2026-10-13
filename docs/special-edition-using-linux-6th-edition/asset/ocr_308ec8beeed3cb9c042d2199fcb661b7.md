Following is the command that is used to generate key pairs:

```
```text
gpg --gen-key
```
```

Listing 25.1 is a sample key generation session for the fake user Sherman T. Potter, whose machine is rumble.fish.net.

# LISTING 25.1  GENERATING A KEY PAIR

```
```text
[stp@rumble stp]$ gpg --gen-key
gpg (GnuPG) 1.0.1; Copyright (C) 1999 Free Software Foundation, Inc.
This program comes with ABSOLUTELY NO WARRANTY.
This is free software, and you are welcome to redistribute it
under certain conditions. See the file COPYING for details.

gpg: /home/stp/.gnupg: directory created
gpg: /home/stp/.gnupg/options: new options file created
gpg: you have to start GnuPG again, so it can read the new options file
[stp@rumble stp]$ gpg --gen-key
gpg (GnuPG) 1.0.1; Copyright (C) 1999 Free Software Foundation, Inc.
This program comes with ABSOLUTELY NO WARRANTY.
This is free software, and you are welcome to redistribute it
under certain conditions. See the file COPYING for details.

gpg: /home/stp/.gnupg/secring.gpg: keyring created
gpg: /home/stp/.gnupg/pubring.gpg: keyring created
Please select what kind of key you want:
    (1) DSA and ElGamal (default)
    (2) DSA (sign only)
    (4) ElGamal (sign and encrypt)
Your selection?
DSA keypair will have 1024 bits.
About to generate a new ElG-E keypair.
              minimum keysize is 768 bits
                 default keysize is 1024 bits
        highest suggested keysize is 2048 bits
What keysize do you want? (1024)
Requested keysize is 1024 bits
Please specify how long the key should be valid.
             0 = key does not expire
            <n> = key expires in n days
           <n>w = key expires in n weeks
           <n>m = key expires in n months
           <n>y = key expires in n years
Key is valid for? (0)
Key does not expire at all
Is this correct (y/n)? y

You need a User-ID to identify your key; the software constructs the user id
from "Real Name, Comment and Email Address in this form:
    "Heinrich Heine (Der Dichter) <heinrich@duesseldorf.de>"

Real name: Sherman T. Potter
Email address: stp@fish.net
Comment:
You selected this USER-ID:
    "Sherman T. Potter <stp@fish.net>"
```
```