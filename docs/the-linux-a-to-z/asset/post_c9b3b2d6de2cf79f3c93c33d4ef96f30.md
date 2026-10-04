
where type is the filesystem type (e.g. msdos, ext2, iso9660, nfs, etc.), device is the name of the device special file which holds the filesystem to be mounted (e.g. /dev/fd0, /dev/hdb1, etc.) and directory is the position in the current directory hierarchy where the new filesystem is to go.

When you have finished using it, a filesystem can be unmounted again with the command umount, which has the format:

```
umount directory
```

In the case of a floppy disk filesystem, it is particularly important for you to umount it before you remove the disk from the drive. This is because there may be some filesystem data stored in memory which has not yet been written to the floppy, and the umount command will arrange to flush this data to disk.

The mount and umount commands can only be used by root.

An example mount command to mount our /dev/hda1 DOS partition under the Linux directory /mnt would be:

```
# mount -t msdos /dev/hda1 /mnt
```

You will then need to copy the files loadlin.exe and loadlinx.exe into the DOS partition. In the Slackware distribution these two files are packed into a .zip file in the /root directory. Unpacking them and performing the copy can be done as follows:

```
# cd /root
# unzip loadlin*.zip
# cp /root/LOADLIN/LOADLIN.EXE /mnt/dos
# cp /root/LOADLIN/LOADLINX.EXE /mnt/dos
```

If you don't have the unzip command under Linux, then you could always copy the .zip file to a DOS directory and unpack it with pkunzip.

You can now copy the compressed Linux kernel image to the DOS partition with the command:

```
# cp /usr/src/linux/arch/i386/boot/zImage /mnt/vmlinuz
```

and all should be ready for a reboot.

Once the machine is booted into DOS you should be able to boot Linux just by using the command:

```
c:\> loadlin c:\vmlinuz root=/dev/hda3 ro
```

## Users

Many Linux machines will operate as stand alone boxes, with only a single user (you!) and no connection to the outside world. In a situation like that it seems strange to be thinking about user accounts and system administrator duties – it’s just a PC for goodness sake!

However, you should try not to think in this way. Whether you are on a single-user private PC at home or on a 200-user fully Internet connected service machine in a large institution, if you have a root account on the machine you should always treat it with respect; you should consider yourself to be in the role of a caretaker rather than a god. When you work on the machine it should be with two separate hats, one labeled ordinary user which you should use for all your ordinary day to day work and for as many of the system administrator functions as can be done without a system privileged account, and another hat labeled caretaker which you only wear when absolutely necessary and for as short a period of time as is required to perform your task. I cannot emphasize enough that if you have a root account on a machine, especially one where other users are involved, then yours is a position of trust and responsibility. A position not to be taken lightly, and certainly not one to be taken with any malicious intent.

### 8.1 Account Passwords

After you have just installed a Linux distribution there may well be only one usable account - root. It usually starts off with no password set, so the first task is to set one. You should choose your root password with particular care as it is all that lies between you and anyone else accessing your machine with root privilege. You should definitely avoid using any word which might appear in a dictionary, as well as your dog’s name or any variation on your birthdate or your partner’s name. All these things are easy to guess for anyone who knows you, even slightly. You change the root password with the same command as for changing ordinary user passwords:

```
# passwd
```

Even logged in as root, there is no way that you can find out what someone uses for a password. This means that the best you can do for a user who can't remember his or her password is either to remove the password altogether, which allows the user then to choose a new one the next time they login, or you can set up a new password for the user directly. You tell the new password to the user who can use it to login and then change it for something private. The latter approach is best as it doesn't leave a period of time when the user's account is unprotected. In order to change a user's password directly you use the passwd command with a parameter which is the login name of the user whose password you wish to change:

```
# passwd login_name
```

An easy way to find out who else is logged into your machine is to use the who command, as follows:

```
# who
pc      tty1    Jul  3 19:25
mot     tty p0   Jul  3 20:06 (grexiz.soc.staff)
carey   tty p1   Jul  3 20:08 (gregory.soc.staff)
rvc     tty p2   Jul  3 20:12 (rachel.soc.staff)
```

The information displayed by the who command is split up into several fields. First comes the user's login name, followed by the name of the terminal that the user is using. This is followed by the date and time at which the user logged in and, finally, if the user logged in to the machine over a network, the name of the machine from which the connection was made.

### 8.2 Adding User Accounts

Having put a password on your root account, the next task is to create yourself an ordinary user account. Many Linux distributions supply a special command to help you with creating a new user account. This command is called adduser or useradd depending on which distribution you have installed. Either way, the command will ask you a series of questions about the new user account and when you have supplied all the answers (or accepted the defaults, where applicable) the new user account will be created.

I can see that this simplifies the procedure all round but for novice administrators I think it is important to understand what is happening underneath so that you can make more informed choices. Therefore, so you will understand what is going on, we will add your account manually this time and you can look at the special command next time.

In fact, adding a user account manually is quite an easy job, consisting of the following steps:

- 1. Set up the login entry in /etc/passwd.
- 2. Create the user's home directory.
- 3. Set the user as the owner of the home directory.
- 4. Set up access permissions on the home directory.
- 5. Set up the user's group entry in /etc/group.

Before you can set up the password file entry, you need to decide on the following account details: the login name, the UID, the GID, the path to the home directory and which shell the user will use.

### 8.2.1 Password File

Armed with this information you can now edit the password file /etc/passwd and add the following line to the end of the file, substituting your details into the line as appropriate:

```
login_name:OFF:uid:gid:user’s_real_name:home_directory:shell
```

Choosing a login name is a matter of personal preference unless your site already has some convention for user names. Remember, however, that the name should be unique and must not be longer than eight characters.

Similarly, the choice of UID and GID are fairly arbitrary, except that the UID should be unique, as it is the UID that the system uses to identify a user. If you intend to make proper use of groups then the GID will just be the group number of the group that the new user is to join. The standard GID for the group users in the Slackware distribution is 100. If you don’t need a user to belong to a particular group then you could just set the GID to be the same as the UID so that these users just belong to a group of one.

The user’s home directory can be anywhere in the directory hierarchy but you should impose some kind of policy on the location rather than dot them about at random. A good choice is to site ordinary user home directories under /home. If you expect lots of users then it would be reasonable to mount a large disk partition over /home so that the user accounts can have as much space as they need, while also being confined to this space so that they can’t use up all the space on your root filesystem.

Finally, arguably the best choice for the shell is bash, though there are others available. A typical line to add to the password file might be:

```
roger:OFF:1234:100:R.N.Foxcroft:/home/roger:/bin/bash
```
