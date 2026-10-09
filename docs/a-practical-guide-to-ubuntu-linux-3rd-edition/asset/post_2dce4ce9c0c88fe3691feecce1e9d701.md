
connection dies for another reason, even if it is only temporary. This option tests the connection at the transport (TCP) layer (page 380). Setting this parameter to **no** causes the client not to check whether the connection is alive. This declaration uses the TCP **keealive** option, which is not encrypted and is susceptible to *IP spoofing* (page 1154). Refer to “ClientAliveInterval” on page 679 for a server-based nonspoolable alternative.

**User name** Specifies a username to use when logging in on a system. You can specify a system with the Host declaration. This option means that you do not have to enter a username on the command line when you are using a username that differs from your username on the local system.

**VisualHostKey yes | no** (Ubuntu 8.10 and later) Displays an ASCII art representation of the key of the remote system in addition to displaying the hexadecimal representation of the key when set to **yes**. See *ssh-keygen* on page 677 for an example. When set to **no** (default), this declaration displays the hexadecimal key only.

## SETTING UP AN OPENSSH SERVER (**sshd**)

This section describes how to set up an OpenSSH server.

### Prerequisites

**Installation** Install the following package:

- **openssh-server**

When you install the **openssh-server** package, the **dpkg** **postinst** script creates the host key files in /etc/ssh (OpenSSH uses these files to identify the server; page 665) and starts the sshd daemon:

```
Unpacking openssh-server (from .../openssh-server_1.3a3s.3pl-3ubuntu3_i386.deb) ...
Setting up openssh-server (1.5.3p1-3ubuntu3) ...
Creating SSH2 RSA key; this may take some time ...
Creating SSH2 DSA key; this may take some time ...
* Stopping OpenBSD Secure Shell server sshd [ OK ]
ssh start/running, process 1741
```

**ssh init script** After you configure the OpenSSH server, give the following **initctl restart** command (page 434) to restart the sshd daemon:

```
$ sudo restart ssh
ssh start/running, process 1434
```

# NOTE

**Firewall** An OpenSSH server normally uses TCP port 22. If the OpenSSH server system is running a firewall, you need to open this port. To do so, use **gufw** (page 876) to set a policy that allows the SSH service.

## JUMPSTART: STARTING AN OPENSSH SERVER

Installing the requisite package starts the OpenSSH server (sshd) daemon. Look in `/var/log/auth.log` to make sure everything is working properly.

## RECOMMENDED SETTINGS

The configuration files provided by Ubuntu establish a mostly secure system and may or may not meet your needs. The Ubuntu `/etc/ssh/sshd_config` file turns on X11 forwarding (page 681). It is important to set `PermitRootLogin` (page 680) to `no`, which prevents a known-name, privileged account from being exposed to the outside world with only password protection. If the `root` account is locked, the setting of this declaration is not an issue.

## AUTHORIZED KEYS: AUTOMATIC LOGIN

You can configure OpenSSH so you do not have to enter a password each time you connect to a server (remote system). To set up this feature, you need to generate a personal authentication key on the client (local system), place the public part of the key on the server, and keep the private part of the key on the client. When you connect to the server, it issues a challenge based on the public part of the key. The private part of the key must then respond properly to this challenge. If the client provides the appropriate response, the server logs you in.

The first step in setting up an automatic login is to generate your personal authentication keys. First check whether these authentication keys already exist on the local system (client) by looking in `~/.ssh` for either `id_dsa` and `id_dsa.pub` or `id_rsa` and `id_rsa.pub`. If one of these pairs of files is present, skip the next step (do not create a new key).

On the client, the `ssh-keygen` utility creates the public and private parts of an RSA key. The key's `randomart` image is a visual representation of the public key; it is designed to be easy to recall. Display of the `randomart` image by a client is controlled by the `VisualHostKey` declaration (page 676) in the `ssh_config` file.

```
$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/sam/.ssh/id_rsa): RETURN
Enter passphrase (empty for no passphrase): RETURN

Enter same passphrase again: RETURN
Your identification has been saved in /home/sam/.ssh/id_rsa.
Your public key has been saved in /home/sam/.ssh/id_rsa.pub.
The key fingerprint is:
f2:e:b:c8:fe:ed:fd:32:98:e8:24:5a:76:1d:0f:1d sam@peach
The key's randomart image is:
++[ RSA 2048]----+
|                 oE|
|    . o o |
| . . |  |  . . |
|   . + + o |
| . +  o |  |  |
| . . |
```

Replace rsa with dsa to generate DSA keys. In this example, the user pressed RETURN in response to each query. You have the option of specifying a passphrase (10–30 characters is a good length) to encrypt the private part of the key. There is no way to recover a lost passphrase. See the following security tip for more information about the passphrase.

### When you encrypt your personal key

The private part of the key is kept in a file that only you can read. If a malicious user compromises your account, an account that can use **sudo** to gain **root** privileges, or the **root** account on the local system, that user then has access to your account on the remote system because she can read the private part of your personal key.

Encrypting the private part of your personal key protects the key and, therefore, restricts access to the remote system should someone compromise your local account. However, if you encrypt your personal key, you must supply the passphrase you used to encrypt the key each time you use the key, negating the benefit of not having to type a password when logging in on the remote system. Also, most passphrases that you can remember can be cracked quite quickly by a powerful computer.

A better idea is to store the private keys on a removable medium, such as a USB flash drive, and use your ~/.ssh directory as the mount point for the filesystem stored on this drive. You may want to encrypt these keys with a passphrase in case you lose the flash drive.

The *ssh-keygen* utility generates two keys: a private key or identification in *~/.ssh/id_rsa* and a public key in *~/.ssh/id_rsa.pub*. No one except the owner should be able to write to either of these files, and only the owner should be able to read from the private key file.

To enable you to log in on or copy files to and from another system without supplying a password, first create a *~/.ssh* directory with permissions set to 700 on the server (remote system). Next copy *~/.ssh/id_rsa.pub* from the client (local system) to a file named *~/.ssh/authorized_keys* on the server (remote system). Set its permissions to 600 so that no one except the owner can read from or write to this file. Now when you run *ssh* or *scp* to access the server, you do not have to supply a password. To make the server even more secure, you can disable password authentication by setting PasswordAuthentication to *no* in */etc/ssh/sshd_config* (remove the # from the beginning of the PasswordAuthentication line and change the yes to no; page 680).

## COMMAND-LINE OPTIONS

Command-line options override declarations in the configuration files. Following are descriptions of some of the more useful sshd options.

- **d** (debug) Sets debug mode so that sshd sends debugging messages to the system log and the server stays in the foreground (implies -D). You can specify this option a maximum of three times to increase the verbosity of the output. See also -e. (The ssh client uses -v for debugging; see page 672.)
- **e** (error) Sends output to standard error, not to the system log. Useful with -d.
- **f** *file* Specifies *file* as the default configuration file instead of */etc/ssh/sshd_config*.
