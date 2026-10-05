# CHAPTER IV | Configuring and Securing SSH

> NOTE
When you run ssh-agent, it prints out some shell commands. You need to run these commands to set environment variables by programs like ssh-add to communicate with it. The eval ${ssh-agent} command starts ssh-agent and runs those commands to automatically set those environment variables for shell session. it also displays the PID of the ssh-agent process.

Once ssh-agent is running, you need to tell it the passphrase for your private key or keys. You can do this with the ssh-add command.

The following ssh-add command adds private keys for /home/user/.ssh/id_rsa (the default) and /home/user/.ssh/key-with-pass, respectively.

```
[user@host ~]$ ssh-add
Identity added: /home/user/.ssh/id_rsa (user@host.example.com)
[user@host ~]$ ssh-add .ssh/key-with-pass
Enter passphrase for .key-with-pass: redpass
Identity added: .ssh/key-with-pass (user@host.example.com)
```

After successfully adding the private keys to the ssh-agent process, you can invoke an SSH connection using the ssh command. If you use any private key other than the default /home/user/.ssh/id_rsa file, then you must use the -i option with the ssh command to specify the path to the private key.

The following example of the ssh command uses the default private key to authenticate to an SSH server.

```
[user@host ~]$ ssh user@remothost
Last login: Fri Apr 5 10:53:50 2019 from host.example.com
[user@remothost ~]$
```

The following example of the ssh command uses the /home/user/.ssh/key-with-pass (non-default) private key to authenticate to an SSH server. The private key in the following example has already been decrypted and added to your ssh-agent process, so the ssh command does not prompt you to decrypt the private key by interactively entering its passphrase.

```
[user@host ~]$ ssh -i .ssh/key-with-pass user@remothost
Last login: Mon Apr 8 09:44:20 2019 from host.example.com
[user@remothost ~]$
```

When you log out of the session that started ssh-agent, the process will exit and your passphrases for your private keys will be cleared from memory.

# REFERENCES
ssh-keygen(1), ssh-copy-id(1), ssh-agent(1), ssh-add(1) man pages