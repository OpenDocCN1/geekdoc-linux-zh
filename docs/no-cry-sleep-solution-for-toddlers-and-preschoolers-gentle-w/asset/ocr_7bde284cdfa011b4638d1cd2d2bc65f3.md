> NOTE The .ssh/identity filename is used in SSH version 1; it may be installed by default on older distribution versions. SSH version 2 uses a different filename, .ssh/id_dsa or .ssh/id_rsa, depending on whether RSA or DSA authentication is used.

If you need to change your passphrase, you can do so with the ssh-keygen command and the -p option. Each user will have their own SSH configuration directory, called .ssh, located in their own home directory. The public and private keys, as well as SSH configuration files, are placed here. If you build from the source code, the make install operation will automatically run ssh-keygen. Table 18-2 lists the SSH configuration files.

# Authorized Keys

A public key is used to authenticate a user and its host. You use the public key on a remote system to allow that user access. The public key is placed in the remote user account's .ssh/authorized_keys file. Recall that the public key is held in the .ssh/id_dsa.pub file. If a user wants to log in remotely from a local account to an account on a remote system, they would first place their public key in the .ssh/authorized_keys file in the account on the remote system they want to access. If the user larisa on turtle.mytrek.com wants to access the aleina account on rabbit.mytrek.com, larisa's public key from /home/larisa/.ssh/id_dsa.pub first must be placed in aleina's authorized_keys file, /home/aleina/.ssh/authorized_keys. larisa could send the key or have it copied over. A simple cat operation can append a key to the authorized key file. In the next example, the user adds the public key for aleina in the larisa.pub file to the authorized key file. The larisa.pub file is a copy of the /home/larisa/.ssh/id_dsa.pub file that the user received earlier.

```
cat larisa.pub >> .ssh/authorized_keys
```

# Loading Keys

If you regularly make connections to a variety of remote hosts, you can use the ssh-agent command to place private keys in memory where they can be accessed quickly to decrypt received transmissions. The ssh-agent command is intended for use at the beginning of a login session. For GNOME, you can use the openssh-askpass-gnome utility, invoked by ssh-add, which allows you to enter a password when you log in to GNOME. GNOME will automatically supply that password whenever you use an SSH client.

Although the ssh-agent command enables you to use private keys in memory, you also must specifically load your private keys into memory using the ssh-add command. ssh-add with no arguments loads your private key from your .ssh/id_dsa or .ssh/id_rsa.pub file. You are prompted for your passphrase for this private key. To remove the key from memory, use ssh-add with the -d option. If you have several private keys, you can load them all into memory. ssh-add with the -l option lists those currently loaded.

# SSH Clients

SSH was originally designed to replace remote access operations, such as rlogin, rcp, and Telnet (see Chapter 15), which perform no encryption and introduce security risks such as transmitting passwords in clear text. You can also use SSH to encode X server sessions as well as FTP transmissions (sftp). The ssh-clients package contains corresponding SSH clients