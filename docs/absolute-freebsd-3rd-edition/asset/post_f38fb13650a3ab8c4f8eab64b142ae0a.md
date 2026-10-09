
## Finalizing Setup

Now that you have an installed system, let's do some fine-tuning. Diskless clients need third-party packages and assorted configuration files. The easiest and safest way to finish setting up your client is through using the chroot(8) program, which locks you into a subdirectory of the filesystem. By using chroot(8) on the NFS server, you can get read-write access to the filesystem almost exactly as it will exist on the diskless client.

```
# chroot /diskless/1
```

Yes, /etc still has hierarchical overrides, but other parts of the system exist exactly as the diskless client sees them. Any changes you make while chrooted will be coherent to the client.

### Installing Packages

Use pkg(8) to install software on a diskless client. Use the -c flag to specify the diskless root directory and have pkg(8) chroot into it.

```
# pkg -c /diskless/l/ install pkg
```

You now have the package tools, database, and repository information on your diskless client.

```
# pkg -c /diskless/l/ install sudo
```

Install any software you need this way.

## SSH Keys

Perhaps the most annoying thing about diskless clients is the host's SSH keys. In normal operation, every host needs unique SSH keys. If you're running on a private network, you might decide to have all the diskless clients share the same SSH key. You might decide to have each host autogenerate new SSH keys at boot time. As /etc exists on tmpfs, those keys will vanish at shutdown, but users will quickly grow accustomed to the “host key has changed” messages. That’s not something you want users to grow accustomed to, though.

Establishing persistent, unique host keys for each diskless client, however, isn’t hard. Create a /conf directory for each host.

```
# mkdir -p /diskless/l/conf/198.51.100.101/etc/ssh
# cd /diskless/l/conf/198.51.100.101/etc/ssh
```

In this directory, create the SSH keys for each algorithm your version of SSH uses. While ssh-keygen(1) includes the -A flag to autogenerate missing keys, it places those keys in /etc/ssh. That won’t work for your diskless userland or even in a chroot. You’ll need to create those keys the old-fashioned way.

```
# ssh-keygen -N "" -qt algorithm -f ssh_host_algorithm_key
```

You’ll need to substitute the name of the cryptographic algorithm twice, in lowercase. For example, here’s how you’d create a DSA SSH key:

```
# ssh-keygen -N "" -qt dsa -f ssh_host_dsa_key
```

Today, OpenSSH creates keys for RSA, ECDSA, and ED25519. Create each of those. Key creation is easily scriptable. See /etc/rc.d/sshd for examples.

Diskless clients let you easily run thousands of nearly identical machines. Now let's look at protecting just one.

## Storage Encryption

FreeBSD supports two different disk encryption methods, GBDE and GELI. Both tools work very differently, support different cryptographic algorithms, and are designed for different threat models. People talk about encrypting disks all the time, but you rarely hear discussions of what disk encryption is supposed to protect the disk from.

*GBDE, or Geom-Based Disk Encryption*, has specific features for high-security environments where protecting the user is just as important as concealing the data. In addition to a cryptographic key provided by the user, GBDE uses keys stored in particular sectors on the hard drive. If either key is unavailable, the partition can't be decrypted. Why is this important? If a secure data center (say, in an embassy) comes under attack, the operator might have a moment or two to destroy the keys on the hard drive and render the data unrecoverable. If the bad guys have a gun to my head and tell me to "enter the passphrase or else," I want the disk system to say, `The passphrase is correct, but the keys have been destroyed.` I don't want a generic error saying, `cannot decrypt disk.` In the first situation, I still have value as a blubbering hostage; in the latter, either I'm dead or the attackers get unpleasantly creative.[^3]

GELI is much more flexible, but it won't protect me from bodily harm the way GBDE might. If someone might steal my laptop for the confidential documents on it, or if an untrusted system user might snoop my swap space to steal secrets, GELI suffices. GELI doesn't try to protect my person, just my data. As I won't take any job that poses a higher than average risk of exposure to firearms (keeping in mind that I live in Detroit), that's perfectly fine with me. GELI also uses FreeBSD's cryptographic device driver, which means that if your server has a hardware cryptographic accelerator, GELI takes advantage of it transparently.

I should mention that people lose more data to encryption misconfiguration or lost keys than to laptop theft. When I hear someone say, “I’ve encrypted my whole hard drive!” I have a nearly psychic vision of the future where that same person is saying, “I’ve lost access to everything on my hard drive!” More often than not, I’m correct. Consider carefully whether you really, truly *need* disk encryption. If you do need it, also back your files up. Those government spoaks aren’t going to crack the encryption on your laptop. They’re going to wait for you to decrypt it yourself—and then they’ll break in.

If you want to encrypt your laptop, use the FreeBSD installer to do so. You should still read this section so you understand how the disk encryption works, but if the installer wants to do the work for you, let it. We’ll walk through using GELI to encrypt a disk partition on /dev/dad0, storing the cryptographic keys on the USB storage device mounted on /media. You might find it more sensible to use a filesystem in a file (see Chapter 13) as an encrypted partition. Very few people actually need to encrypt their entire hard drive, and in certain circumstances, doing so might raise suspicions. I have enough trouble explaining to airport security why my computer “looks so weird.” In their minds, a boot prompt that says, Insert cryptographic key and enter cryptographic passphrase is only one step away from This man is a dangerous lunatic who requires a very thorough body cavity search. If you really do need to encrypt certain documents, chances are they total only a few megabytes. That’s a perfect application for a filesystem in a file or a flash drive.

Note that you must load the *geom_eli.ko* kernel module before working with GELI.

### Generating and Using a Cryptographic Key

GELI lets you use a key file and/or a passphrase as cryptographic keys for an encrypted device. We’ll use both. To generate your cryptographic key file, use dd(1) to grab a suitable amount of data from /dev/random and write it to a file. Remember, /media is where our USB device is mounted. If you really want to protect your data, create your key directly on the USB device and don’t leave it on your filesystem where a hypothetical intruder could recover it. (Even deleting the file still leaves remnants that a skilled attacker could conceivably extract.)

```
# dd if=/dev/random of=/media/da0p1.key bs=64 count=1
1+0 records in
1+0 records out
64 bytes transferred in 0.000149 secs (429497 bytes/sec)
```

The 64 bytes of data constitute a 512-bit key. You can increase the size of the key if you like, at the cost of extra processor overhead when accessing the encrypted filesystem. Don’t forget that your passphrase also increases key complexity.

To assign a passphrase to the key, use geli init. The -s flag tells geli(8) the desired sector size on the encrypted filesystem; 4,096 bytes, or 4KB, is usually a decent sector size for this application. The -k indicates the key file. You must also specify the device to be encrypted.

```
# geli init -s 4096 -K /media/da0p1.key /dev/da0p1
Enter new passphrase:
Reenter new passphrase:
```

A passphrase is much like a password except that it can contain spaces and be of any length. If you really want to protect your data, I recommend using a passphrase that is several words long, contains nonalphanumeric characters, and is not a phrase in your native language.

Now that you have a key, attach it to the device to be encrypted.

```
# geli attach -k /media/da0p1.key /dev/da0p1
Enter passphrase:
```

GELI now knows that /dev/da0p1 is an encrypted disk and that the file /media/da0p1.key contains the key file. Once you enter the passphrase, you can access the decrypted contents of the encrypted disk at the new device node, /dev/da0p1.el. Of course, you need a filesystem to put any data on that disk.

[^3]: Footnote reference from original text.
