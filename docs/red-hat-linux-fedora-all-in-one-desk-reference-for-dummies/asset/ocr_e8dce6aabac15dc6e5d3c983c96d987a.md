GPG displays a message and prompts you on the level of key verification you have performed:

```
```
gpg: Warning: using insecure memory!
gpg: please see http://www.gnupg.org/faq.html for more information

gpg: checking the trustdb
gpg: checking at depth 0 signed=0 ot=-/q/n/f/u/=0/0/0/0/1
pub 1024D/DB42A60E created: 1999-09-23 expires: never trust: -/-
sub 2048g/9616302 created: 1999-09-23 expires: never
(1). Red Hat, Inc <security@redhat.com>

pub 1024D/DB42A60E created: 1999-09-23 expires: never trust: -/-
Fingerprint: CA20 8686 2B06 90FC 65F6 ECC4 2191 80CD B842 A60E

Red Hat, Inc <security@redhat.com>

How carefully have you verified the key you are about to sign actually belongs to the person named above? If you don't know what to answer, enter "0".

(0) I will not answer. (default)
(1) I have not checked at all.
(2) I have done casual checking.
(3) I have done very careful checking.

Your selection?
```
```

After you answer and press Enter, GPG asks for confirmation and then prompts you for your passphrase. After that GPG signs the key.

![](bbox=[0.1, 0.63, 0.2, 0.73])

Because the key verification and signing is a potential weak link in GPG, be careful about what keys you sign. By signing a key, you basically say that you trust the key to be from that person or organization.

# Signing a file

You find it useful to sign files if you send out a file to someone and want to assure the recipient that no one has tampered with the file and that it was you who sent the file. GPG makes it very easy to sign a file. You can compress and sign a file named message with the following command:

```
```
gpg -o message.sig -s message
```
```

To verify the signature, type

```
```
gpg --verify message.sig
```
```

To get back the original document, simply type

```
```
gpg -o message --decrypt message.sig
```
```