
such as Ettercap. The incremental improvements to SSH-1, such as SSH 1.3 and 1.5, are vulnerable. SSH servers that offer SSH version 1.99 support SSH version 1 and version 2.

Do not let your SSH clients request SSH-1. Do not let your SSH servers offer SSH-1.

OpenSSH has removed support for SSH-1, so if you have an old embedded device that only speaks SSH-1, you’ll need to manage it with PuTTY or, better still, spend a couple dollars to replace that device with something built this millennium.¹

SSH-2 is the modern standard. The protocol is designed so that vulnerabilities can be quickly addressed as they are discovered. Our constantly-increasing computing power makes today’s strong encryption tomorrow’s security risk, so SSH-2 is designed so that its algorithms and protocols can be upgraded in place.

Protocols such as SCP and SFTP (Chapter 7) are built atop SSH.

## What Isn’t In This Book?

This book is meant to familiarize you with SSH, and help you reach a minimum level of competence with OpenSSH and PuTTY. This means eliminating passwords, restricting your SSH services to the minimum necessary privileges, and using SSH as a transport for common management tools. You will be able to easily copy files over SSH, manage server keys with minimal fuss, use digital certificates to permit only approved keys on your network, and a few other tricks.

This book is not intended as a comprehensive SSH tome. It doesn’t cover integrating SSH with Kerberos, or SecurID, or hooking your SSH install into Google authenticator, or using your SSH agent as an authentication source for third-party programs. These are all interesting topics, but very platform specific, and might well change before you finish reading this book. Sysadmins interested in authentication options might find my book PAM Mastery (Tilted Windmill Press, 2016) useful.

## What Is In This Book?

Chapter 0 is this introduction.

Chapter 1, “Encryption and Keys,” gives basic information about encryption and how SSH uses it.

Chapter 2, “Common Configuration,” covers configuration syntax used throughout the OpenSSH server and client.

Chapter 3, “The OpenSSH Server,” discusses configuring the OpenSSH server sshd. This chapter orients you on configuring sshd, but more specific examples appear throughout this book.

Chapter 4, “Host Key Verification,” covers a frequently overlooked but vital part of using any SSH client: verifying server keys. This topic is so vital that it needs its own chapter, even before our first discussion of SSH clients.

Chapter 5, “SSH Clients,” discusses two popular SSH clients, OpenSSH’s ssh(1) for Unix-like systems and PuTTY for Windows.

Chapter 6, “Copying Files Over SSH,” covers moving files across the network using SSH as a transport, with the SCP (secure copy) and SFTP (SSH file transfer) protocols.

Chapter 7, “SSH Keys,” walks you through creating a personal key pair (public and private cryptographic key). Key pairs make authentication more secure. When combined with agents they eliminate the need to routinely type passwords but don’t degrade SSH security.

Chapter 8, “X Forwarding,” will teach you how to display graphics over your SSH connections while minimizing risk.

Chapter 9, “Port Forwarding,” covers using SSH as a generic TCP/IP proxy, letting you redirect arbitrary network connections through the network to remote machines.

Chapter 10, “Keeping SSH Sessions Open,” covers ways to keep SSH sessions running despite the firewalls and proxy servers and unreliable ISPs that want to shut them down after minutes or hours.

Chapter 11, “Key Distribution,” tells systems administrators how to automatically distribute host keys and improve security while eliminating the need for users to manually compare host key fingerprints. We also cover issues in distributing user public keys across large cloud systems.

Chapter 12, “Automation,” discusses ways to use SSH as a transport for automated tools and tightly–controlled user tasks, as well as creating single-purpose user keys.

Chapter 13, “OpenSSH VPNs,” demonstrates how to use OpenSSH to create an encrypted tunnel between two sites.

Chapter 14, “Certificate Authorities,” guides you through creating a certificate authority to permit only authorized user keys to log on to your network.

That’s enough blather! Let’s get to work.

¹ A few Linux distributions deliberately ship an SSH client that supports SSH-1. That’s on them.

## Chapter 1: Encryption, Algorithms, and Keys

OpenSSH encrypts traffic. What does that mean, and how does it work? I give a detailed explanation in my book PGP & GPG (No Starch Press, 2006), but here’s the brief version.

Encryption transforms readable *plaintext* into unreadable *ciphertext* that attackers cannot understand. *Decryption* reverses the transformation, producing readable text from apparent gibberish. An *encryption algorithm* is the exact method for performing this transformation. Most children discover the code that substitutes numbers for letters, so that A equals one, B equals two, Z equals 26, and so on. This is a simple encryption algorithm. Modern computer-driven encryption algorithms work on chunks of text at a time and perform far more complicated transformations.

Most encryption algorithms use a *key*; a chunk of text, numbers, symbols, or data used to encrypt messages. A key can be chosen by the user or randomly generated. (People habitually choose easily-guessed keys, so OpenSSH doesn’t even give users an option to create your own.) The encryption algorithm uses the key to encrypt the text, making it more difficult for an outsider to decrypt. Even if you know the encryption algorithm, you cannot decrypt the message without the secret encryption key.

Think of the encryption algorithm as a type of lock, and the key is a specific key. Locks come in many different types: house doors, bicycles, factories, and so on. Each uses a certain type of key—your door key is probably the wrong shape to fit into any vehicle ignition. But even a key of the proper type won’t work in the wrong lock. Your front door key unlocks your front door, and only your front door. Encryption keys work similarly.

### Algorithm Types

Encryption algorithms come in two varieties, symmetric and asymmetric.

A *symmetric algorithm* uses the same key for both encryption and decryption. Symmetric algorithms include, but are not limited to, the Advanced Encryption Standard (AES) and ChaCha20, as well as older but now insecure algorithms like 3DES and Blowfish. A child’s substitution code is a symmetric algorithm. Once you know that A equals one and so on, you can encrypt and decrypt messages. Symmetric algorithms (more sophisticated than simple substitution) can be very fast and secure, so long as only authorized people have the key. And that’s the problem: an outsider who gets the key can read your messages or replace them with his own. You must protect the key. Sending a key unencrypted across the Internet is like standing on the playground shouting, “A is one, B is two.” Anyone who hears the key can read your private message.

An *asymmetric algorithm* uses different keys for encryption and decryption. You encrypt a message with one key, and then decrypt it with another. This works because the keys are very large numbers, and multiplying very large numbers is much easier than figuring out how to divide them. (There are very good explanations out on the Internet, if you want the details.) Asymmetric encryption became popular only with the wide availability of computers that can handle the very difficult math, and is much, much slower and more computationally expensive than symmetric encryption.

Having two separate keys creates interesting possibilities. Make one key public. Give it away. Broadcast it to the entire world. Keep the other key private, and protected at all costs. Anyone who has the public key can encrypt a message that only someone who knows the private key can read. Someone who has the private key can encrypt a message and send it out into the world. Anyone can use the public key to decrypt that message, but the fact that the public key can decrypt the message assures recipients that the message sender had the private key. This is the basis of *public key encryption*. The public key and its matching private key are called a *key pair*. Again, think of the lock on your front door. The lock itself is public; anyone can touch it. The key is private. You must have both to get into your home. (You can learn more by researching Diffie-Hellman key exchange.)

### How SSH Uses Encryption

Symmetric encryption is fast, but offers no way for hosts to securely exchange keys. Asymmetric encryption lets hosts exchange public keys, but it’s slow and computationally expensive. How can you efficiently encrypt the session between two hosts that have never previously communicated?

Every SSH server has a key pair. Whenever a client connects, the server and the client use this key pair to negotiate a temporary key pair shared only between these two hosts. The client and the server both use this temporary key pair to derive a symmetric key that they will use to exchange data during this session, as well as related keys to provide connection integrity. If the session runs for a long time or exchanges a lot of data, the computers will intermittently negotiate a new temporary key pair and new symmetric key. The SSH protocol is more complicated than this, and includes safeguards to prevent many different cryptographic attacks, but cryptographic key exchange is the heart of the protocol.

SSH supports many symmetric and asymmetric encryption algorithms. The client and server negotiate mutually agreeable algorithms at every connection.
