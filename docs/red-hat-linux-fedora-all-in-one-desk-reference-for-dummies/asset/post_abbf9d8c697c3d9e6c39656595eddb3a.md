
commands. But what if the Linux kernel refused to execute instructions from any data area? Poof! — no more buffer overflows! That's exactly what the latest Linux kernel does: It protects against the common buffer overflow type of vulnerabilities by making many parts of a program's memory (including the stack where temporary variables are stored) not executable. This feature of the Linux kernel is called exec-shield.

The best part about exec-shield is that you don't have to fix the applications that have the buffer overflow problem. All you have to do is turn on the feature. To make the process even easier, Red Hat Linux enables exec-shield by default.

Some programs may have trouble working correctly when exec-shield is enabled. If you have to turn off exec-shield, log in as root and type the following command from a terminal window:

```
echo 0 > /proc/sys/kernel/exec-shield
```

That command sets the exec-shield kernel option to 0. The exec-shield option can take one of three values — 0, 1, and 2. Think of these values as four different levels of security. Table 2-2 summarizes the meaning of the four values of exec-shield. Red Hat Linux sets exec-shield to 1 by default.

Table 2-2 Four Levels of Security Using Exec Shield

| This Value of exec-shield | Has This Meaning |
|---|---|
| 0 | exec-shield is always disabled. |
| 1 | exec-shield is enabled for programs compiled with the newest version of gcc compiler. |
| 2 | exec-shield is always enabled. |

![](img/a7eec43a54473e95dc5ea333fecf1bd7_568_0.png)

To set exec-shield to its default value, type:

```
echo 1 > /proc/sys/kernel/exec-shield
```

## Encrypting and Signing Files with GnuPG

Red Hat Linux comes with the GNU Privacy Guard (GnuPG or, simply GPG) encryption and authentication utility. With GPG, you can create your public and private key pair, encrypt files using your key, and also digitally sign a message to authenticate that it's really from you. If you send a digitally signed message to someone who has your public key, the recipient can verify that it was you who signed the message.

## Understanding public key encryption

The basic idea behind public key encryption is to use a pair of keys — one private and the other public — that are related but can't be used to guess one from the other. Anything encrypted with the private key can be decrypted only with the corresponding public key, and vice versa. The public key is for distribution to other people while you keep the private key in a safe place.

You can use public key encryption to communicate securely with others; Figure 2-1 illustrates the basic idea. Suppose Alice wants to send secure messages to Bob. Each of them would generate public and private key pairs, after which they'd exchange their public keys. Then, when Alice wants to send a message to Bob, she simply encrypts the message using Bob's public key and sends the encrypted message to him. Now the message is secure from any eavesdropping because only Bob's private key can decrypt the message — and only Bob has that key. When Bob receives the message, he uses his private key to decrypt the message and read it.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_569_0.png)

Figure 2-1: Bob and Alice can communicate securely with public key encryption.

At this point, you should stop and think and say “Wait a minute!” How does Bob know the message really came from Alice? What if someone else uses Bob's public key and sends a message as if it came from Alice? This is where digital signature comes in.

## Understanding digital signatures

The purpose of digital or electronic signatures is the same as pen-and-ink signatures, but how you sign digitally is completely different. Unlike pen-and-ink signatures, your digital signature depends on the message you're signing. The first step in creating a digital signature is to apply a mathematical function on the message and reduce it to a fixed-size message digest (also called hash or a fingerprint). No matter how big your message is, the message digest is always around 128 or 160 bits, depending on the hashing function.

The next step is to apply public key encryption. Simply encrypt the message digest with your private key, and you get the digital signature for the message. Typically, the digital signature is appended to the end of the message, and voila! — you get an electronically signed message.

What good does the digital signature do? Well, anyone who wants to verify that the message is indeed signed by you takes your public key and decrypts the digital signature. What they get is the message digest (the encrypted hash) of the message. Then they apply the same hash function to the message and compare the computed hash with the decrypted value. If the two match, then no one has tampered with the message. Because your public key was used to verify the signature, the message must have been signed with the private key known only to you. So the message must be from you!

In the theoretical scenario of Alice sending private messages to Bob, Alice can digitally sign her message to make sure that Bob can tell that the message is really from her. Figure 2-2 illustrates the use of digital signature along with normal public key encryption.

Here's how Alice sends her private message to Bob with the assurance that Bob can really tell it's from her:

- 1. Alice uses software to compute the message digest of the message and then encrypts the digest using her private key. This is her digital signature for the message.
- 2. Alice encrypts the message, (again, using some convenient software and *Bob's public key*.
- 3. She sends both the encrypted message and the digital signature to Bob.
- 4. Bob decrypts the message using his private key.
- 5. Bob decrypts the digital signature using Alice's public key. This gives him the message digest.

Figure 2-2:
Alice can digitally sign her message so that Bob can tell it's really from her.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_571_0.png)

- 6. Bob computes the message digest of the message and compares it with what he got by decrypting the digital signature.
- 7. If the two message digests match, Bob can be sure that the message really came from Alice.

## Using GPG

GPG includes the tools you need to use public key encryption and digital signatures. What you use is the gpg command. You can learn to use GPG gradually as you begin using encryption. I show you some of the typical tasks you may perform with GPG.

## Generating the key pair

The first thing you have to do is generate your own private-public key pair. Type the following command in a terminal window to generate the key pair:

```
gpg --gen-key
```

If this is your first time with gpg, it creates a .gnupg directory in your home directory and a file named options in that directory. Then gpg exits with a message that asks you to run gpg again. Now you can rerun the command. The steps for generating the key pairs go like this:

- 1. **Type the gpg --gen-key command again.**
- You should see a message like this:
- 2. **Press Enter for the default choice because it's good enough.**
- GPG then prompts you for the key size (the number of bits).
- 3. **Again, press Enter to accept the default value of 1024 bits.**
- GPG asks you when the keys should expire. The default is to never expire.
- 4. **If the default is what you want (and why not?), press Enter.**
- 5. **When GPG asks if you really want the keys to never expire, press y to confirm.**
- GPG prompts you for your name, then your e-mail address, and finally a comment so that the key pair can be associated with your name.
- 6. **Type each piece of requested information and press Enter.**
- 7. **When GPG gives you a chance to change the information or confirm it as is, confirm by typing o and then pressing Enter.**
- GPG next prompts you for a passphrase that will be used to protect your private key.
- 8. **Type a long phrase that includes lower- and uppercase letters, numbers, and punctuation marks — the longer the better — and then press Enter.**
- Careful though; pick a passphrase that you can easily remember.
- GPG generates the keys. It may ask you to perform some work on the PC so that the random number generator can generate enough random numbers for the key-generation process.

```
Please select what kind of key you want:
(1) DSA and ElGamal (default)
(2) DSA (sign only)
(5) RSA (sign only)
Your selection?
```

## Exchanging keys

To communicate with others, you have to give them your public key. You also have to get public keys from those who may send you a message (or someone who might sign a file and you want to verify the signature). GPG keeps the public keys in your key ring. To list the keys in your key ring, type

```
gpg --list-keys
```
