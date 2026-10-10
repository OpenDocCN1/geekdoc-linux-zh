pass this information. You can do so by preceding the hostname with the username and an at sign (@) or by using the -l parameter. For instance, both of the following two commands log you onto the al account on mail1.pangaea.edu:

```
$ ssh al@mail1.pangaea.edu
$ ssh -l al mail1.pangaea.edu
```

# ## Configuring SSH Keys

In a default configuration, SSH prompts for a password when making a connection. You can use alternative authentication tools, though; several such options are summarized in Table 6.1. When you activate these methods, they’re tried before a password prompt. As an example, consider using public key authentication. As described here, this method will enable you to log into the remote system without typing a password. Instead, SSH will use private and public keys stored on the client and server. As a result, an interloper won’t be able to masquerade as you without breaking into your computer and stealing your public key. You can use a similar approach, but with some modifications, to require use of an SSH-specific passphrase rather than the client’s normal password for logins. To implement a public key system that requires no password, follow these steps:

+   1.  Log into the SSH client system (say, wegener.pangaea.edu).

+   2.  Type the following command to generate public and private keys for the client system:
+   $ ssh-keygen -q -t rsa -f ~/ .ssh/id_rsa -C '' -N ''

![](bbox=[0.14, 0.58, 0.28, 0.68])

Omitting the -N '' parameter from this command causes the program to prompt for a passphrase. You will then need to use the passphrase instead of a password when you connect to the server. If you press the Enter key twice when prompted for the password, the effect is the same as including -N '',

+   3.  Copy the ~/ .ssh/id_rsa.pub file from the client computer to the server computer. You can transfer this file via floppy disk, using scp (an SSH-based file copy utility), or by any other means you choose. If you use scp, you’ll have to enter a password.
+   4.  Log into the SSH server system (say, mail1.pangaea.edu). You may use SSH to do this, but at this point you’ll still have to use a password.
+   5.  Ensure that the ~/ .ssh directory exists and has 0700 (-rw-------) permissions. If necessary, type **mkdir** ~/ .ssh to create the directory or **chmod** **0700** ~/ .ssh to set appropriate permissions on the directory.
+   6.  Add the contents of the id_rsa.pub file you’ve transferred from the client to the ~/ .ssh/authorized_keys file on the server. (This filename may differ; check the AuthorizedKeysFile option in your SSH server configuration.) If this is the first