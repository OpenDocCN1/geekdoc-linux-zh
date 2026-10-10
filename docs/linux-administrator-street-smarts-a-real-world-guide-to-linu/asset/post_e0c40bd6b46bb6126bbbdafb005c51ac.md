
This task assumes you’re using OpenSSH, which is the most common SSH implementation in Linux. SSH Tectia (http://www.ssh.com) was the original SSH implementation, but it’s uncommon in Linux because it’s a commercial package. Various less-common SSH implementations also exist, but most are configured differently from OpenSSH.

## Caveats

Because you must be **root** to configure OpenSSH, the usual **root** caveats apply. Because SSH is a server that grants users full shell access to the computer, a misconfiguration or bug in SSH can quickly lead to security problems. Thus, you should be careful not to make mistakes, and if a system doesn’t really need an SSH server, you should disable it or, better yet, uninstall the package when you’re done with this task.

## Procedure

This task requires completing two subtasks. First, you must configure the basic SSH server options. This task is fairly straightforward but requires **root** access. The second part of this task requires setting up SSH keys to enable quicker logins. This part of the task is somewhat more involved but you can do it as an ordinary user.

## Configuring the SSH Server

The SSH server is configured through the `/etc/ssh/sshd_config` file, and the SSH client is configured through the `/etc/ssh/ssh_config` file. These filenames are very similar, so be sure not to confuse them! Both files consist of comments (indicated by hash marks, #) and key-word/argument pairs, as in this example:

```
PermitRootLogin no
```

For the most part, both the client and server configurations are reasonable with most distributions. You might want to change a few options, though. Table 6.1 summarizes some additional SSH server options (in `sshd_config`) that you might want to change. Pay particular attention to the `PermitRootLogin` server option (it should be set to no to conform with the requirements outlined in this task’s scenario) and to the X forwarding options. Using SSH to initiate a connection that supports X-based applications can be a convenient method of remote GUI access, but this configuration requires support in the client and server.

In Linux, the primary SSH client is called, naturally enough, `ssh`. In its simplest form, you type the program name followed by the system to which you want to connect. Ordinarily, the remote server then prompts you for a password. The first time you connect, the system also informs you that it can’t verify the authenticity of the remote site. To test your configuration thus far, you’d do something like this from a second Linux system:

```
alfred@werner:~$ ssh mail.pangaea.edu
```

```
The authenticity of host 'mail.pangaea.edu (192.168.1.6)' can't be established.
RSA key fingerprint is 4b:68:c1:a8:75:5e:b4:76:7b:a6:a2:0d:1a:8b:5f:48. Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'mail.pangaea.edu,192.168.1.6' (RSA) to the list of known hosts.
alfred@mail.pangaea.edu's password:
[alfred@mail alfred]$
```

## Common SSH Server Configuration Options

| Keyword | Argument Type | Description |
|---|---|---|
| Protocol | Integer | SSH protocol version number. OpenSSH 4 supports versions 1 and 2. To specify both versions, separate them with a comma, as in `Protocol 1,2` |
| ListenAddress | Hostname or IP address and optional port number | Binds the server to listen only to the network interface associated with the specified address. If a port number is specified, it follows the address and a colon, as in `ListenAddress 172.26.7.3:22`. (The default SSH port number is 22.) |
| PermitRootLogin | Boolean, without-password, or forced-commands-only | Whether or not to accept direct logins as root. This option defaults to yes. Changing it to no will improve your system's security by requiring intruders to log in using an ordinary account and then using `su`, thereby requiring two passwords. The without-password option disables password authentication, meaning that another authentication method must be available. This option does not mean that users can log into the root account without any authentication. The forced-commands-only option enables public key authentication only for running commands remotely, which may be useful for performing remote backups or the like. |
| RhostsAuthentication | Boolean | If this option is set to yes, the server accepts authentication based on the rhosts trusted-hosts authentication model for protocol level 1 sessions. This authentication method is inherently dangerous, so I strongly recommend you leave this option at its default value of no. |
| RsaAuthentication | Boolean | If this option is set to yes (the default), the server accepts Rivest/Shamir/Adleman (RSA) authentication for protocol level 1 sessions. This approach can improve security or eliminate the need to type a password, depending on how it's used. |
| PubKeyAuthentication | Boolean | If this option is set to yes (the default), the server accepts public key authentication for protocol level 2 sessions. This approach can improve security or eliminate the need to type a password, depending on how it's used. |
| AuthorizedKeysFile | Filename | Name of the file in which clients' keys for public key authentication are stored. |
| KerberosAuthentication | Boolean | If set to yes, this option enables SSH to accept Kerberos tickets and to authenticate users via a Kerberos server. This option is useful if your network uses Kerberos but is set to no by default. Additional options that begin with Kerberos can fine-tune the configuration; consult the `sshd_config` man page for details. |
| X11Forwarding | Boolean | If set to yes, this option enables the server to forward X session data. The default value is no. |
| Compression | Boolean | If this option is set to yes (the default), the server accepts requests from the client to enable compression. This option consumes CPU time but reduces network bandwidth use. |

Some configurations automatically add previously unknown sites to the key file, so you may not have to authorize a connection. Either way, subsequent connections to the same system will lack the prompt and need to type yes to authorize a connection. You will have to type a password, though, unless you modify the configuration as described shortly. (The password doesn't echo to the screen.)

Linux's ssh client passes the current username as part of the connection protocol. If your username on the server system is different from your username on the client system, you must pass this information. You can do so by preceding the hostname with the username and an at sign (@) or by using the `-l` parameter. For instance, both of the following two commands log you onto the al account on mail1.pangaea.edu:

```
$ ssh al@mail1.pangaea.edu
$ ssh -l al mail1.pangaea.edu
```

## Configuring SSH Keys

In a default configuration, SSH prompts for a password when making a connection. You can use alternative authentication tools, though; several such options are summarized in Table 6.1. When you activate these methods, they’re tried before a password prompt. As an example, consider using public key authentication. As described here, this method will enable you to log into the remote system without typing a password. Instead, SSH will use private and public keys stored on the client and server. As a result, an interloper won’t be able to masquerade as you without breaking into your computer and stealing your public key. You can use a similar approach, but with some modifications, to require use of an SSH-specific passphrase rather than the client’s normal password for logins. To implement a public key system that requires no password, follow these steps:

- 1. Log into the SSH client system (say, wegener.pangaea.edu).
- 2. Type the following command to generate public and private keys for the client system:
  ```
  $ ssh-keygen -q -t rsa -f ~/.ssh/id_rsa -C '' -N ''
  ```
  
  ![](img/f430a19bdf014c43ad7c2d594afd5b21_310_0.png)
  
  Omitting the `-N ''` parameter from this command causes the program to prompt for a passphrase. You will then need to use the passphrase instead of a password when you connect to the server. If you press the Enter key twice when prompted for the password, the effect is the same as including `-N ''`.
- 3. Copy the `~/.ssh/id_rsa.pub` file from the client computer to the server computer. You can transfer this file via floppy disk, using `scp` (an SSH-based file copy utility), or by any other means you choose. If you use `scp`, you’ll have to enter a password.
- 4. Log into the SSH server system (say, mail1.pangaea.edu). You may use SSH to do this, but at this point you’ll still have to use a password.
- 5. Ensure that the `~/.ssh` directory exists and has 0700 (`-rw-------`) permissions. If necessary, type **mkdir** `~/.ssh` to create the directory or **chmod** **0700** `~/.ssh` to set appropriate permissions on the directory.
- 6. Add the contents of the `id_rsa.pub` file you’ve transferred from the client to the `~/.ssh/authorized_keys` file on the server. (This filename may differ; check the `AuthorizedKeysFile` option in your SSH server configuration.) If this is the first
