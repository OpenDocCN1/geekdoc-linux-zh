
## Linux Hack

Ajay Kumar Tiwari

### tune2fs -l output

| Field | Value |
|---|---|
| Errors behavior | Continue |
| Filesystem OS type | Linux |
| Inode count | 1094912 |
| Block count | 140138994 |
| Reserved block count | 0 |
| Free blocks | 16848481 |
| Free inodes | 1014969 |
| First block | 0 |
| Block size | 2048 |
| Fragment size | 2048 |
| Reserved GDT blocks | 512 |
| Blocks per group | 16384 |
| Fragments per group | 16384 |
| Inodes per group | 128 |
| Inode blocks per group | 8 |
| Filesystem created | Tue Jul 1 00:06:03 2008 |
| Last mount time | Thu Aug 21 05:58:25 2008 |
| Last write time | Fri Jan 2 15:40:36 2009 |
| Mount count | 2 |
| Maximum mount count | 20 |
| Last checked | Tue Jul 1 00:06:03 2008 |
| Check interval | 15552000 (6 months) |
| Next check after | Sat Dec 27 23:06:03 2008 |
| Reserved blocks uid | 0 (user root) |
| Reserved blocks gid | 0 (group root) |
| First inode | 11 |
| Inode size | 128 |
| Default directory hash | tea |
| Directory Hash Seed | 12345829-1236-4123-9aaa- |

You can also use the tune2fs to tune the ext2/ext3 filesystem parameter. For example, if you want to change the Filesystem volume name, you can do it as shown below.

```
# tune2fs -l /dev/sda1 | grep volume
Filesystem volume name:/home/database
# tune2fs -L database-home /dev/emcpowera1
tune2fs 1.35 (28-Feb-2004)
```

```
# tune2fs -l /dev/sda1 | grep volume
```

Filesystem volume name:database-home

### Hack 69. Create a swap file system.

Create a file for swap usage as shown below.

```
# dd if=/dev/zero of=/home/swap-fs bs=1M count=512
```

512+0 records in

512+0 records out

```
# ls -l /home/swap-fs
```

-rw-r--r-- 1 root root 536870912 Jan 2 23:13 /home/swap-fs

Use mkswap to setup a Linux swap area in the /home/swap-fs file that was created above.

```
# mkswap /home/swap-fs
```

Setting up swapspace version 1, size = 536866 kB

Once the file is created and has been setup for Linux swap area, it is time to enable the swap using swapon as shown below.

```
# swapon /home/swap-fs
```

Add the following line to /etc/fstab and reboot the system for the swap to take into effect.

```
/home/swap-fs swap swap defaults 0 0
```

### Hack 70. Create a new user

### Add a new user – Basic method

Specify only the user name.

```
# useradd jsmith
```

### Add a new user with additional Parameter

You can also specify the following parameter to the useradd

- -c : Description about the user.
- -e : expiry date of the user in mm/dd/yy format

```
# adduser -c "John Smith - Oracle Developer" -e 12/31/09 jsmith
```

Verify that the user got added successfully.

```
# grep jsmith /etc/passwd
```

```
jsmith:x:510:510:John Smith - Oracle Developer:/home/jsmith:/bin/bash
```

### Change the user password.

```
# passwd jsmith
```

Changing password for user jsmith.

New UNIX password:

BAD PASSWORD: it is based on a dictionary word

Retype new UNIX password:

passwd: all authentication tokens updated successfully.

Note: Make sure to follow these best practices to create a strong password for the user.

### How to identify the default values used by useradd?

Following are the default values that will be used when an user is created.

```
# useradd -D
```

```
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
```

### Hack 71. Create a new group and assign to an user

Create a new developer group.

```
# groupadd developers
```

Validate that the group was created successfully.

```
# grep developer /etc/group
```

```
developers:x:511:
```

Add an user to an existing group.

You cannot use useradd to modify an existing user, as you'll get the following error message.

```
# useradd -G developers jsmith
```

useradd: user jsmith exists

```
# usermod -g developers jsmith
```

Validate the users group was modified successfully.

```
# grep jsmith /etc/passwd
```

jsmith:x:510:511:Oracle Developer:/home/jsmith:/bin/bash

```
# id jsmith
```

uid=510(jsmith) gid=511(developers)
groups=511(developers)

```
# grep jsmith /etc/group
```

jsmith:x:510:
developers:x:511:jsmith

### Hack 72. Setup SSH passwordless login in OpenSSH

You can login to a remote Linux server without entering password in 3 simple steps using ssh-keygen and ssh-copy-id as explained in this example.
ssh-keygen creates the public and private keys. ssh-copy-id copies the local-host's public key to the remote-host's authorized_keys file. ssh-copy-id also assigns proper permission to the remote-host's home, ~/.ssh, and ~/.ssh/authorized_keys.

### Step 1: Create public and private keys using ssh-keygen on local-host

```
jsmith@local-host$ ssh-keygen
```

Generating public/private rsa key pair.

Enter file in which to save the key
(/home/jsmith/.ssh/id_rsa):[Enter key]
Enter passphrase (empty for no passphrase): [Press enter key]
Enter same passphrase again: [Press enter key]
Your identification has been saved in
/home/jsmith/.ssh/id_rsa.
Your public key has been saved in
/home/jsmith/.ssh/id_rsa.pub.
The key fingerprint is:
33:b3:fe:af:95:95:18:11:31:d5:de:96:2f:f2:35:f9
jsmith@local-host

### Step 2: Copy the public key to remote-host using ssh-copy-id

jsmith@local-host$ ssh-copy-id -i ~/.ssh/id_rsa.pub remote-host
jsmith@remote-host's password:
Now try logging into the machine, with "ssh 'remote-host'", and check in:
.ssh/authorized_keys to make sure we haven't added
extra keys that you weren't expecting.
Note: ssh-copy-id appends the keys to the remote-host's
.ssh/authorized_keys.

### Step 3: Login to remote-host without entering the password

jsmith@local-host$ ssh remote-host
Last login: Sun Nov 16 17:22:33 2008 from 192.168.1.2
[Note: SSH did not ask for password.]
jsmith@remote-host$ [Note: You are on remote-host here]

### Hack 73. Use ssh-copy-id along with ssh-agent

### Using ssh-copy-id along with the ssh-add/ssh-agent

When no value is passed for the option -i and If ~/.ssh/identity.pub is not available, ssh-copy-id will display the following error message.

```
jsmith@local-host$ ssh-copy-id -i remote-host
/usr/bin/ssh-copy-id: ERROR: No identities found
```

If you have loaded keys to the ssh-agent using the ssh-add, then ssh-copy-id will get the keys from the ssh-agent to copy to the remote-host. i.e, it copies the keys provided by ssh-add -L command to the remote-host, when you don't pass option -i to the ssh-copy-id.

```
jsmith@local-host$ ssh-agent $SHELL
jsmith@local-host$ ssh-add -L
The agent has no identities.
jsmith@local-host$ ssh-add
Identity added: /home/jsmith/.ssh/id_rsa
(/home/jsmith/.ssh/id_rsa)
jsmith@local-host$ ssh-add -L
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAsJIEILxftj8aSxMa3d8t6JvM79D aHrtPhTYpq7kIEMUNzApnyxsHpH1tQ/Ow== /home/jsmith/.ssh/id_rsa
jsmith@local-host$ ssh-copy-id -i remote-host
jsmith@remote-host's password:
```

Now try logging into the machine, with "ssh 'remote-host'", and check in: .ssh/authorized_keys to make sure we haven't added extra keys that you weren't expecting.

[Note: This has added the key displayed by ssh-add -L]

### Three Minor Annoyances of ssh-copy-id

Following are few minor annoyances of the ssh-copy-id.

- Default public key: ssh-copy-id uses ~/.ssh/identity.pub as the default public key file (i.e when no value is passed to option -i). Instead, I wish it uses id_dsa.pub, or id_rsa.pub, or identity.pub as default keys. i.e If any one of them exist, it should copy that to the remote-host. If two or three of them exist, it should copy identity.pub as default.
- The agent has no identities: When the ssh-agent is running and the ssh-add -L returns "The agent has no identities" (i.e no keys are added to the ssh-agent), the ssh-copy-id will still copy the message "The agent has no identities" to the remote-host's authorized_keys entry.
- Duplicate entry in authorized_keys: I wish ssh-copy-id validates duplicate entry on the remote-host's authorized_keys. If you execute ssh-copy-id multiple times on the local-host, it will keep appending the same key on the remote-host's authorized_keys file without checking for duplicates. Even with duplicate entries everything works as expected. But, I would like to have my authorized_keys file clutter free.

### Hack 74. Crontab

Using cron you can execute a shell-script or Linux commands at a specific time and date. For example a sysadmin can schedule a backup job that can run every day.

How to add a job to the cron?

```
# crontab -e
0 5 * * * /root/bin/backup.sh
```
