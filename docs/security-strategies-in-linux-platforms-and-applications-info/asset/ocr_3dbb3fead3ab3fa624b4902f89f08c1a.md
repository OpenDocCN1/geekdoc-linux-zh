# The Simple rsync Solution

The rsync command is frequently used for backups. You'll see how backups work in Chapter 14. For now, this section examines the basic features of the rsync command. The first time you back up a system with the rsync command, everything might seem slow. With its archive features, the rsync command can back up more than just the information in regular files. It can preserve more, including the following:

+   * Ownership by users and groups
* Last file-access times
* Permissions
* Symbolic links between files

An rsync-based backup with all such original information can form the basis for a "gold baseline." The dates associated with files on the backup provide assurance that such files have not been changed after a certain date. Such a date can be important in case of a security breach, especially if your managers suddenly refuse to trust files created after that date.

One of the risks associated with the rsync command is that it normally transmits data in clear text. If SSH clients are installed on the local system, rsync doesn't have to take such risks. For example, the following command takes the contents of user michael's home directory recursively (with all subdirectories) and sends it to the remote system named backup.example in the /backups/subdirectory:

```
$ rsync -e ssh -ahZ ~michael/backup.example:/backups/
-e ssh tunnels the backup packets over an SSH connection. If you haven't yet connected to the remote system, the remote SSH server prompts for a password or sends a message to verify the passphrase described earlier in this chapter. The -H transmits hard-linked files in the archive. The -z compresses the data being transmitted, speeding up the backup.
```

# E-Mail Clients

Standard e-mail clients connect to servers using three major protocols: the Simple Mail Transfer Protocol (SMTP), the Post Office Protocol version 3 (POP3), and the Internet Mail Access Protocol version 4 (IMAP4). Most users configure e-mail clients as Evolution, Thunderbird, and specifically Microsoft's Outlook Express to send and receive their e-mail communications using these protocols.

Every time a request to send or receive e-mail is sent from a client to an e-mail server, the username and password is also sent over the network. With those clear-text protocols, it's easy for a black-hat hacker to identify those usernames and passwords with tools such as Wireshark.