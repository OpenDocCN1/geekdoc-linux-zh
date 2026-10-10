
UNIX has a strict and consistent notion of file ownership. Windows 95/98 SMB protocols have no concept whatsoever of file ownership. There is no way, therefore, for a UNIX SMB server to signal to a Windows 95/98 client that permission to access a file is denied because of lack of ownership.

Many SMB clients convert passwords to uppercase before transmitting them. Samba tries to compensate by trying various permutations of passwords. Other SMB clients encrypt passwords before transmitting them. Samba supports encrypted passwords.

SMB provides many types of locks to Windows clients. Samba can simulate most of these locks, but it cannot enforce locking against UNIX programs. That is, if a Windows client locks a file, it will be locked for other Windows clients, but a UNIX process can access the file without difficulty. This can lead to problems if both Windows and UNIX processes update a file at the same time.

Finally, SMB is poorly documented. Although the Samba team did receive some documentation and help from Microsoft, and SMB is an X/Open standard, much of the Samba functionality was implemented by reverse-engineering the protocol. It is a tribute to the Samba team’s tenacity that Samba works as well as it does.

## Samba Configuration

Samba uses the file `/etc/samba.d/smb.conf` to hold configuration options. Samba has a huge number of configuration options, all of which are described in the `smb.conf(5)` manual page. To aid in your understanding of Samba, let’s look at a simple configuration file that illustrates some of the common options and then build from there.

The configuration file (as is usual on UNIX) is a plain text file. Blank lines and lines beginning with `#` or `;` are ignored.

The configuration file is divided into a number of sections. The `global` section controls the overall behavior of Samba. Each `share` has its own section that controls parameters related to it. (A share is a shared resource such as a printer or disk directory that the server offers to clients.)

### Global Configuration Options

Global options apply to the Samba server as a whole. Here are some global settings. They are edited versions of the sample configuration options in `/etc/samba.d/smb.conf.sample` supplied with Caldera OpenLinux.

```text
# Sample SAMBA file
# The global settings begin with the tag [global]
```

```text
[global]

# Workgroup (NT domain name)
workgroup = WORKGROUP

# Server string — equivalent of NT "Description" field
server string = Samba Server on Caldera OpenLinux

# Automatically set up printers from /etc/printcap
load printers = yes

# Caldera uses LP/Rng printer daemon
printing = lp1ng

# Cap the size of the log file at 50kB
max log size = 50

# Security mode: Don't use share-level security!
security = user

# How to fiddle with upper/lowercase matches
password level = 1
username level = 1

# Encrypt passwords? (commented out)
# encrypt passwords = yes
# smb passwrd file = /etc/samba/.smbpasswd
```

The `[global]` tag indicates the start of the global options section. The `workgroup` option specifies a Microsoft domain name. You should set it to your Windows NT domain name. The `server string` option is a comment that appears in the Network Neighborhood browser on a Windows client in Detailed view mode.

The `load printers = yes` option tells Samba to create a shared printer for each printer found in the system `/etc/printcap` file. We will cover Samba printer configuration later in this chapter. UNIX systems have a number of methods for print spooling; the `printing = lp1ng` tells Samba that the server uses the LP/Rng print spooler.

The `security = user` option tells Samba that all users must authenticate themselves with a username/password pair. This is far more secure than share-level security. In share-level security, a password is associated with the shared resource itself, and any user who can produce that password is granted access. Modern clients (Windows 95/98 and NT) support user-level security, and you should configure Samba to use it.

The `password level` and `username level` options specify how many combinations of upper- and lowercase letters to try when matching usernames and passwords. Some silly clients convert usernames and passwords to uppercase; this is clearly no good for UNIX authentication. A level of 1 means that Samba tries the following possibilities:

- The name as sent.
- The name in all uppercase.
- The name in all lowercase.
- All combinations of one uppercase and the rest lowercase.
- All combinations of one lowercase and the rest uppercase.

The higher this value, the longer a connection attempt may take and the lower security.

### Encrypted Passwords

Modern Windows clients can encrypt passwords before sending them over the network. This increases security because a person listening in on your network cannot capture users’ passwords.

Samba supports encrypted passwords, but it is mildly painful to set them up. SMB does not use the same encryption algorithm as the UNIX password file, so it needs a separate file to store encrypted passwords. This file is typically `/etc/samba.d/smbpasswd`.

To set up the file, you must create an entry for each user in your system password file. If you are not using NIS, do it like this (as root):

```bash
# mksmbspasswd < /etc/passwd > /etc/samba.d/smbpasswd
```

If you are using NIS, run this command instead:

```bash
# ypcat passwd | mksmbspasswd > /etc/samba.d/smbpasswd
```

These commands set up a file with everyone’s password locked. Next, you must set the password for each user who wishes to access shares from a Windows client. Do this as follows (as root):

```bash
# smbpasswd user
New SMB password: gr9x3wq
Retype new SMB password: gr9x3wq
Password changed for user user
```

### Disabling Encrypted Passwords

If your local network is secure or you are using other protocols (like Telnet) that transmit clear-text passwords anyway, you may wish to disable encrypted passwords. This simplifies maintenance of the password file. (You don’t need to maintain a separate smbpasswd file.)

![](img/df365d352a104b50fea29e59a052de4d_390_0.png)

You can disable encrypted passwords on Windows clients. The mechanism for doing this varies depending on which version of Windows you are using. For details, see the files `NT4_PlainPassword.reg`, `Win95_PlainPassword.reg`, and `Win98_PlainPassword.reg` in `/usr/doc/samba-2.0.3/docs`. You should also look at the documentation files in `/usr/doc/samba-2.0.3/docs/textdocs`, especially the `ENCRYPTION.txt` file.

### File Shares

After the global configuration options come share configurations. Each share section specifies a resource to be shared with Windows clients. Continuing with the sample configuration file, here is a section which that shares the CD-ROM volume:

```text
# Make the CD-ROM available to anyone read-only
[cdrom]
    path = /mnt/cdrom
    public = yes
    writable = no
```

The `[cdrom]` section creates a share called `cdrom`. The `path` specifies which directory is to be shared. Any Windows client accessing the share will see the directory tree rooted at `/mnt/cdrom`.

The `public = yes` option specifies that anyone may access the share without a password. The Samba daemon changes its user ID to `nobody` when a public connection is made. The `writable = no` option provides read-only access, which is certainly to be expected for a CD-ROM device.

I have set up the `cdrom` share on `shishi`. From the test Windows machine, the resource is known as `\\shishi\cdrom`. Windows names network resources as two backslashes followed by the server name, another backslash, and the share name.

Samba supports a special kind of share called `[homes]`. Here is an example:

```text
[homes]
    valid users = %$S
    only user = yes
    user = %$S
    writable = yes
    create mask = 0750
```

The share is special because it creates artificial shares based on the user name. If, for example, user `dfs` connects to a share called `dfs`, Samba first looks for a share named `dfs` in the `smb.conf` file. Not finding one, it checks for the presence of a homes share. If this exists, and if `dfs` has an entry in the UNIX password file, the homes share is cloned with a default path equal to the user's home directory. In essence, this makes `\\servername\default` map to `username`'s home directory (as long as `username` has an entry in the UNIX password file).
