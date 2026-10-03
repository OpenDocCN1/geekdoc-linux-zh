the server.

Yes, this looks much like a regular password-based logon, but behind the scenes it’s very different. You’ve decrypted the key file locally. The only authentication information you’ve sent to the server is confirmation that you’re able to exchange data encrypted with a public key stored in the authorized_keys file in your account on the server. You never send a password or other traditional authentication information.

OpenSSH automatically checks for all the standard key files. You might have a special-purpose key that’s only used for special circumstances, such as automated jobs. To use that key with scp, sftp, or ssh, use the -i flag and the filename.

```
$ ssh -i $HOME/specialkey sloth
```

Now that you know your key works, you’ll need to enter your passphrase every time you log onto this server. This is a good time to configure an SSH agent.

# Using PuTTY User Keys

If you don’t have an agent running, you must tell PuTTY where to find your private key file. On the left side of the PuTTY Configuration screen, select Connection-> SSH-> Auth. In the text box labeled Private key file for authentication:, put the full path to your private key file. Remember, the private key file ends in .ppk.

Now try to connect. PuTTY should prompt you for your username and then request your passphrase. If you enter the passphrase correctly, you’ll get a command prompt.

Once you know that your key works and is installed correctly, reduce how often you must type your passphrase with the Pageant SSH agent.

# SSH Agents

While the SSH agents for OpenSSH and PuTTY are wildly different, both perform identical tasks. They host your private key in secure memory so that you don’t have to keep typing your passphrase. Both let you view the decrypted keys, add new keys, and delete keys. The only real difference between them is how they’re programmed and how you make them behave—you know, the unimportant stuff.

With your key loaded into ssh-agent, your login attempts will look like this:

```
$ ssh mail
Last login: Thu Nov 16 16:56:52 2017 from ceo.worldhq.mwl.io
FreeBSD 10.3-RELEASE-p20 (GENERIC) #0: Wed Jul 12 03:13:07 UTC 2017
```

Note the absence of any request for a password or passphrase; you’ve just logged into the remote machine without human authentication. If you connect to many machines during your working day, an SSH agent makes life much easier