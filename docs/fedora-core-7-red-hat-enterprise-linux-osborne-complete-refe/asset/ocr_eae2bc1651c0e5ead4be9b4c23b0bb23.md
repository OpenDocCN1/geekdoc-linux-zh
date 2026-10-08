The SSH tools are listed in Table 19-2. They include several client programs like **scp** and **ssh**, as well as the ssh server. The ssh server (**sshd**) provides secure connections to anyone from the outside using the ssh client to connect. Several configuration utilities are also included, such as **ssh-add**, which adds valid hosts to the authentication agent, and **ssh-keygen**, which generates the keys used for encryption.

On Red Hat Fedora, you can start, restart, and stop the sshd server with the **service** command or redhat-config-services (Services on the Server Settings window and menu):

```
# service sshd restart
```

For version 2, names of the actual tools have a 2 suffix. Version 1 tools have a 1 as their suffix. During installation, however, links are set for each tool to use only the name with the suffix. For example, if you have installed version 2, there is a link called **scp** to the **scp2** application. You can then use the link to invoke the tool. Using **scp** starts **scp2**. Table 19-2 specifies only the link names, as these are the same for each version. Remember, though, some applications, such as sftp, are available only with version 2.

# ## SSH Setup

Using SSH involves creating your own public and private keys and then distributing your public key to other users you want to access. These can be different users or simply user accounts of your own that you have on remote systems. Often people remotely log in from

| Application | Description |
| :---- | :---- |
| ssh | SSH client |
| sshd | SSH server (daemon) |
| sftp | SSH FTP client, Secure File Transfer Program. Version 2 only. Use ? to list sftp commands (SFTP protocol). |
| sftp-server | SSH FTP server. Version 2 only (SFTP protocol). |
| scp | SSH copy command client |
| ssh-keygen | Utility for generating keys. Use -h for help. |
| ssh-keyscan | Tool to automatically gather public host keys to generate **ssh_known_hosts** files |
| ssh-add | Adds RSD and DSA identitites to the authentication agent |
| ssh-agent | SSH authentication agent that holds private keys for public key authentication (RSA, DSA) |
| ssh-askpass | X Window System utility for querying passwords, invoked by **ssh-add** (openssh-askpass) |
| ssh-askpass-gnome | GNOME utility for querying passwords, invoked by **ssh-add** |
| ssh-signer | Signs host-based authentication packets. Version 2 only. Must be suid root (performed by installation). |
| slogin | Remote login (version 1) |