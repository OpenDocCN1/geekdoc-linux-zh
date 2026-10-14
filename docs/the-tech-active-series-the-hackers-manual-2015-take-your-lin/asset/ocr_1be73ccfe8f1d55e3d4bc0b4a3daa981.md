on top of a RAID array which itself is stacked on the block devices of the individual disks or their partitions. Whole device encryption using dm-crypt works like this: it creates a block device on top of your storage medium which encrypts data as it is saved and decrypts it as it is read. You then create a standard filesystem on top of the encrypted block device and it functions just the same as if it had been created on a normal disk partition.

Many distros have an option to install to an encrypted disk, but here we'll look at creating and working with dm-crypt devices directly to see how they work, as opposed to some black magic that's been set up by the installer. Dm-crypt uses the kernel's device mapper subsystem (hence the name) to manage its block devices and the kernel's cryptographic routines to deal with the encryption. This is all handled by the kernel, but we need userspace software to create and manage dm-crypt devices, with the standard tool being cryptsetup. It's probably already installed on your distro – if not, it will definitely be in its main package repositories.

![](bbox=[0.452, 0.106, 0.938, 0.351])

# Encrypting something

*Cryptsetup* can create two types of encrypted devices: plain dm-crypt and LUKS. If you know you need to use plain dm-crypt, you already know far more about disk encryption than we'll cover here, so we'll only look at LUKS, which is the best choice for most uses. Experimenting with filesystems, encrypted or otherwise, risks the data on the disk while you're learning. All examples here use **/dev/sdb**, which we take to be an external or otherwise spare device – do not try things out on your system disk until you're comfortable doing so. All these commands need to be run as root, so log into a terminal as root with *su*, or prefix each command with *sudo*.

Let's start by creating an encrypted device:

```
cryptsetup luksFormat /dev/sdb1
```

This sets up an encrypted partition on **/dev/sdb1** after prompting you for a passphrase. You can open the encrypted device with:

```
cryptsetup luksOpen /dev/sdb1 name
```

This will ask for the passphrase and then create the device in **/dev/mapper** using the name given on the command line. You can then use **/dev/mapper/name** as you would any disk block device:

```
mkfs.ext4 /dev/mapper/name
mount /dev/mapper/name /mnt/encrypted
```

The usual rules about passphrases apply: keep them long and varied, hard to guess but easy to remember. If you lose the passphrase, you lose the contents of the device.

# Keeping the keys safe

A LUKS encrypted device contains eight key slots. Keys are another term for passphrases, so you can assign multiple passphrases to a device, which is useful if you maintain multiple systems and want to have a master passphrase that only you know. When you use *LuksFormat*, the passphrase you give is stored in slot 0. You can then add another with:

```
cryptsetup luksAddKey /dev/sdb1
```

You'll be asked for an existing passphrase and then prompted for the new one. A key can also be the contents of a file instead of a passphrase; the file can contain anything but it's usual to use random data:

```
dd if=/dev/random of=/path/to/keyfile bs=1k count=1
chmod 0400 /path/to/keyfile
cryptsetup luksAddKey /dev/sdb1 /path/to/keyfile
cryptsetup luksOpen --key-file /path/to/keyfile /dev/sdb1
```

It goes without saying that keyfiles should be stored securely, readable only by root and not stored on the encrypted device. Personally, even if a volume is always unlocked by key file, I prefer to also set a very strong passphrase, recorded in a secure place, to guard against the key file ever becoming corrupted or otherwise inaccessible. Keys can also be changed or removed with the luksChangeKey and luksRemoveKey commands.

# More options

So far, we've stuck with the default encryption choices, but cryptsetup accepts --hash and --cipher options. The former sets the hash the passphrase should be hashed, while the latter selects the encryption method. The defaults are usually more than sufficient but you can see the available options by using:

```
cryptsetup --help
```

These options are needed only with LuksFormat. Once the encrypted device has been created, cryptsetup will automatically use the correct settings when opening it. It's wise to stick with popular ciphers and hashes unless you have a very good reason for using something different. A less frequently used method is more likely to harbour unknown deficiencies due to the fewer number of people using it, as happened recently with the Whirlpool hash implementation in the libgcrypt library used by cryptsetup. Fixing the implementation caused problems for those with systems that were already using the broken hashes.

Another reason for sticking to commonplace methods is portability. This doesn't matter for an internal disk, but if you want to use an encrypted disk on another system, then that must have the used hashes and ciphers installed too.

Use cryptsetup luksDump to find out about a LUKS encrypted partition. There are also backup and restore commands to keep a copy of the LUKS information.

# LUKS

Linux Unified Key Setup was created to provide a standard, platform-independent (despite the name) format for storing encryption data on disks. It doesn't specify the encryption methods used, but how information about those methods is stored. It also provides a more robust way of storing keys or passphrases, because the plain dm-crypt method can be susceptible to corruption. The cross-platform nature of LUKS means that it's now possible to access information stored on LUKS encrypted devices from Windows, using FreeOTFE (http://sourceforge.net/projects/freeotfe/files/).