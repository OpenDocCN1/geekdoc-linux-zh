This command would then generate a secure connection and prompt me for a password. After you have logged in, you have the same freedom as you would under a Telnet session. I can just as easily log in to the same box as another user, such as root, though on my client box I am still logged in as the user kerry:

```
$ ssh -l root antares.astronomy.org
```

The program would then prompt me for the root password on the box named antares. If you are connecting from the client box to the server, certain command-line options are available for optimizing the connection. Table 19.1 describes some of the flags associated with the command ssh.

# NOTE

When you first connect via ssh to another ssh-enabled box, you will notice the following message.

```
$ ssh antares.astronomy.org
Host key not found from database.
Key fingerprint:
uyuvaz-etip-nahok-tytah-bupyx-sosuh-narim-munep-hebuz-bebex-cebox
You can get a public key's fingerprint by running
% ssh-keygen -F publickey.pub
on the keyfile.
Are you sure you want to continue connecting (yes/no)?
```

This is a normal process and you should answer yes if you are connecting to the correct machine. Whenever you subsequently connect to this host, the program will not prompt you before establishing a connection. You can add additional machines to your known hosts configuration file beforehand and not receive this message from other machines.

# Securing Copying Files across Machines

As mentioned earlier, ssh is a replacement for other less secure methods of transmitting data across server connections. If you wish to grab data from another machine on your local network or from another subnet that also has ssh installed, you can use the scp command to copy over the data files remotely. The scp program is part of the ssh package.