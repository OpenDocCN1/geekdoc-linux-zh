
LZMA2 with the 7z format. It also comes with a plugin for a FAR manager and can be integrated with Windows. Some other features of 7-zip are AES-256 encryption.

## Dm-crypt

Dm-crypt is another tool used to encrypt the files and folders stored at the disk level. It does this by encrypting portable containers, disks and partitions. This tool was developed to address reliability and vulnerability issues found in the tool cryptoloop. It can also be used to back up large volumes of data of different forms.

## eCryptfs

eCryptfs is an open-source and free collection of software and tools you can use to encrypt data on disks used in Linux. This tool works like the GnuPG tool, and it implements a POSIX-compliant layer of encryption on the files and systems. This is a part of the Linux kernel and comes installed with most Linux distros. Every version after the Linux 2.6.19 version comes with this tool. eCryptfs is easy for beginners to use since it helps you encrypt partitions and directories without worrying about the file system.

## Cryptsetup

Cryptsetup is a tool or application used to enable users to encrypt various files using a DMCrypt, a kernel module with an emphasis on the Linux Unified Key Setup (LUKS) design. This key has become a standard encryption technique used in the Linux hard drive because it is compatible with every distro available on Linux. This design also ensures that data can be migrated or transported through the network smoothly by securing the information through passwords and other encryption methods.

# Chapter Eight

## Using Cryptsetup to Setup Encrypted Filesystems and Swap Space

A Linux Foundation Certified Engineer or LFCE is trained and has the knowledge to handle Linux network services. He will be trained to install, troubleshoot and manage network services in these systems. He also deals with the maintenance, design, and implementation of the architecture used in Linux systems. If you are a certified LFCE, you can do everything out there to manage the data and files stored in the system or network.

The objective of encryption is to ensure you have only trusted people accessing your information, especially sensitive data. This is the best way to protect the data from being used by hackers in case of any data leak. You can also use this method to protect the data from being stolen or lost from your hard disk or machine.

In simple words, the objective of encryption is for you to use a lock to access the information on your system or server. This is done to ensure the information only is available when you run the system. You can ensure any unauthorized users cannot unlock the system. This means if a person tries to look at the content on the disk, he will not find any information on the files.

In this chapter, we will look at how you can use the dm-crypt to set up an encrypted file system in your server. The term dm-crypt is short for device-mapper and cryptographic. This is the standard tool used for encrypting data in the kernel. It is important to note that the dm-crypt tool can only be used at a block-level. You can use it to encrypt the entire device, loop device, or partition.

### Using a Drive, Loop Device, or Partition for Encryption

Before you perform encryption on your drive, you need to backup all the files on the drive, partition, or loop device before you wipe the data in the chosen space. It is important for you to do this before you proceed further. You also need to wipe the data from the device used, and to do this, we will use the dd command. We can also perform these actions using different tools, such as shred. We will now create a partition on the device, /dev/sdb1, using the command `# dd if=/dev/urandom of=/dev/sdb bs=4096`.

### Testing the Encryption

Before we see how we can use cryptsetup to encrypt files, we need to ensure the kernel is compiled of the encryption you use. To do this, you can write the following command: `# grep -i config_dm_crypt /boot/config-$(uname -r)`. You need to ensure the kernel module dm-crypt is set up correctly to ensure the files and systems can be encrypted in the server and network.

### Installing cryptsetup

Cryptsetup is a tool used to create, configure, access and manage any encrypted files on the server or network. You can do this using dm-crypt. Run the following commands to install the tool on your system:

```bash
# aptitude update && aptitude install cryptsetup   # [On Ubuntu]
# yum update && yum install cryptsetup             # [On CentOS]
# zypper refresh && zypper install cryptsetup     # [On openSUSE]
```

### Setting the Encrypted Partition

The cryptsetup using Linux Unified Key Setup (LUKS) as the default operating mode, so this means you can stick to it. You can set the partition along with the passphrase using the command: `# cryptsetup -y luksFormat /dev/sdb1`

In the above command, you can run the cryptsetup using some of the default parameters. If you do not know what these parameters are, you can list them using the command: `# cryptsetup --version`. Using the list of parameters on your screen, you can determine if you want to change the key, cipher, or hash parameters. If you want to change them, you need to add the symbol ‘-’ before the parameter and add a flag to it. You can then change the parameter which you take from the file /proc/crypto. You then need to open the partition you have created for LUKS. You will be asked to enter the passphrase you used previously. If your authentication passes, you will see that the partition is encrypted in the server or system. This will be present inside /dev/mapper using the following name: `# cryptsetup luksOpen /dev/sdb1 my_encrypted_partition`.

We will now save the partition using the format ext4. To do this, run the following command: `# mkfs.ext4 /dev/mapper/my_encrypted_partition`. This will allow you to create a mount point in your partition, which will help you mount the partition encrypted in the partition. You can also use the commands below to determine if the mount operation is successful:

```bash
# mkdir /mnt/enc
# mount /dev/mapper/my_encrypted_partition /mnt/enc
# mount | grep partition
```

If you are done reading from or writing to the file system you have encrypted, you need to unmount it using the following command: `# umount /mnt/enc`. Once you do this, you can close the LUKS partition using the following command: `# cryptsetup luksClose my_encrypted_partition`.

### Testing Encryption

Now that you have encrypted the file, you need to check if the partition or swap you have encrypted is safe.

- **Step One:** The first thing you need to do is enter the LUKS partition you have created. To do this, run the command: `# cryptsetup luksOpen /dev/sdb1 my_encrypted_partition`
- **Step Two:** Now, enter the passphrase you entered to encrypt the file
- **Step Three:** The next thing to do is to mount the partition using the following command: `# mount /dev/mapper/my_encrypted_partition /mnt/enc`
- **Step Four:** You need to create a dummy file in the mount point using the command: `# echo "This is Part 3 of a 12-article series about the LFCE certification" > /mnt/enc/testfile.txt`
- **Step Five:** You also need to verify if you can access and use the files you have created in the mount point using the command: `# cat /mnt/enc/testfile.txt`
- **Step Six:** To unmount the system, you need to enter the command: `# umount /mnt/enc`
- **Step Seven:** Now that this is done, you can close the partition using the command: `# cryptsetup luksClose my_encrypted_partition`
- **Step Eight:** When you try to mount the file in the regular file system, it will indicate an error. If it does, you have done the right thing to encrypt the partition

### Adding Additional Layers of Security

You can also encrypt the swap space in the server to add another layer of security. When you enter a passphrase on your server to encrypt the partition in the server, it will be stored in the RAM when you switch your system on. If any hacker wants to use this key, he can easily decrypt this information in the data. It is especially easy to do this when it comes to a laptop since the partitions of a RAM are maintained, even during their hibernation sessions, in the swap layers or sections of the memory.

If you want to avoid leaving a copy of the accessible to a hacker, you need to encrypt this swap layer or partition using the process mentioned below:

- **Step One:** Create a partition or separation in the RAM, which will be used as the swap. You need to maintain the right size and use the encryption mechanism mentioned earlier. You can name this section as swap if you need to
- **Step Two:** Once you set this partition, you need to activate the swap using the following commands:

```bash
# mkswap /dev/mapper/swap
# swapon /dev/mapper/swap
```

- **Step Three:** You should now change the entry of the swap in the file: /etc/fstab. To do this, use the following command: /dev/mapper/swap

| none | swap | sw | 0 0 |
| :--- | :--- | :--- | :--- |

- **Step Four:** The last thing you need to do is to save the file down and reboot the server. To do this, run the following command: swap /dev/sdd1 /dev/urandom swap

When you reboot the system, you can verify if the swap space is active or not using the following command: `# cryptsetup status swap`.
