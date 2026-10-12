
Two different versions of SSH exist, called SSH1 and SSH2. The latter is newer, is more secure, comes with more features, and is the default in Fedora Core Linux. However, support for SSH1 clients is also left enabled by default so that older clients can connect. Because it is less secure, you should disable SSH1 if you have no one who specifically relies on it.

To do this, edit the `/etc/ssh/sshd_config` file and look for this line:

```
#Protocol 2,1
```

Edit this line so that it becomes

```
Protocol 2
```

This removes the comment sign (#) and tells sshd that you want it to only allow SSH2 connections. Save the file and exit your editor. The next step is to tell sshd to reread its configuration file, by executing this command:

```
kill -HUP `cat /var/run/sshd.pid`
```

If this returns `cat: /var/run/sshd.pid: No such file or directory`, it means you didn't have sshd running. Next time you start it, it reads the configuration file and uses SSH2 only.

You can test this change by trying to connect to your SSH server in SSH1 mode. From the same machine, type this:

```
ssh -1 localhost
```

The -1 switch forces SSH1 mode. If you successfully forced the SSH2 protocol, you should get the message `Protocol major versions differ: 1 vs. 2`.

## The SSH Tools

To the surprise of many, OpenSSH actually comprises a suite of tools. We have already seen `ssh`, the secure shell command that connects to other machines, and `sshd`, the SSH server daemon that accepts incoming SSH connections. However, there is also `sftp`, a replacement for `ftp`, and `scp`, a replacement for `rcp`.

You should already be familiar with the `ftp` command because it is the lowest-common-denominator system for handling FTP file transfers. Like Telnet, though, `ftp` is insecure: It sends your data in plain text across the network and anyone can sniff your packets to pick out a username and password. The SSH replacement, `sftp`, puts FTP traffic over an SSH link, thus securing it.

The `rcp` command might be new to you, largely because it is not used much anymore. Back in its day, `rcp` was the primary way of copying a single file to another server. As with `ftp`, `scp` replaces `rcp` by simply channeling the data over a secure SSH connection. The difference between `sftp` and `scp` is that the former allows you to copy many files, whereas the latter just sends one.

### Using scp to Copy Individual Files Between Machines

The most basic use of the *scp* command is to copy a file from your current machine to a remote machine. You can do that with the following command:

```
scp test.txt 10.0.0.1:
```

The first parameter is the name of the file you want to send, and the second is the server to which you want to send it. Note that there is a colon at the end of the IP address. This is where you can specify an exact location for the file to be copied. If you have nothing after the colon, as in the previous example, *scp* copies the file to your home directory. As with *SSH*, *scp* prompts you for your password before copying takes place.

You can rewrite the previous command so that you copy *test.txt* from the local machine and save it as *newtest.txt* on the server:

```
scp test.txt 10.0.0.1:newtest.txt
```

Alternatively, if there is a directory where you want the file to be saved, you can specify it like this:

```
scp test.txt 10.0.0.1:subdir/stuff/newtest.txt
```

The three commands so far have all assumed that your username on your local machine is the same as your username on the remote machine. If this is not the case, you need to specify your username before the remote address, like this:

```
scp test.txt japh@10.0.0.1:newtest.txt
```

You can use *scp* to copy remote files locally by simply specifying the remote file as the source and the current directory (*.*) as the destination:

```
scp 10.0.0.1:remote.txt .
```

The *scp* command is nominally also capable of copying files from one remote machine to another remote machine, but this functionality has yet to be properly implemented in Fedora Core Linux. If a patch is released—and we hope one is eventually—the correct command to use would be this:

```
scp 10.0.0.1:test.txt 10.0.0.2:remotetest.txt
```

That copies *test.txt* from *10.0.0.1* to *remotetest.txt* on *10.0.0.2*. If this works, you are asked for passwords for both servers.

### Using sftp to Copy Many Files Between Machines

*sftp* is a mix between *ftp* and *scp*. Connecting to the server uses the same syntax as *scp*—you can just specify an IP address to connect using your current username, or you can specify a username using *username@IPaddress*. You can optionally add a colon and a directory, as with *scp*. After you are connected, the commands are the same as *ftp*: *cd*, *put*, *mput*, *get*, *quit*, and so on.

In one of the scp examples, we copied a remote file locally. You can do the same thing with sftp through the following conversation:

```
[paul@susanah -]$ sftp 10.0.0.1
Connecting to 10.0.0.1...
paul@10.0.0.1's password:
sftp> get remote.txt
Fetching /home/paul/remote.txt to remote.txt
/home/paul/remote.txt 100% 23 0.0KB/s 00:00
sftp> quit
paul@susanah -]$
```

Although FTP remains prominent because of the number of systems that do not have support for SSH (Windows, specifically), SFTP is gaining in popularity. Apart from the fact that it secures all communications between client and server, SFTP is popular because the initial connection between the client and server is made over port 22 through the sshd daemon. Someone using SFTP connects to the standard sshd daemon, verifies himself, and then is handed over to the SFTP server. The advantage to this is that it reduces the attack vectors because the SFTP server cannot be contacted directly and so cannot be attacked as long as the sshd daemon is secure.

## Using ssh-keygen to Enable Key-Based Logins

There is a weak link in the SSH system, and, inevitably, it lies with users. No matter what lengths system administrators go to in training users to be careful with their passwords, Post-it notes with "pAssw0rd" written on are attached to monitors around the world. Sure, it has a mix of letters and numbers, but it can be cracked in less than a second by any brute-force method. Brute-forcing is the method of trying every password possibility, starting with likely words (such as password and variants, or god) and then just trying random letters (for example, a, aa, ab, ac, and so on).

Even very strong passwords are no more than about 16 characters; such passwords take a long time to brute-force but can still be cracked. The solution is to use key-based logins, which generate a unique, 1024-bit private and public key pair for your machine. These keys take even the fastest computers a lifetime to crack, and you can back them up with a password to stop others from using them.

Creating an SSH key is done through the ssh-keygen command, like this:

```
ssh-keygen -t dsa
```

Press Enter when it prompts you where to save your key, and enter a passphrase when it asks you to. This passphrase is just a password used to protect the key—you can leave it blank if you want to, but doing so would allow other people to use your account to connect to remote machines if they manage to log in as you.

After the key is generated (it might take up to 30 seconds depending on the speed of your machine), change the directory to .ssh (`cd .ssh`), which is a hidden directory where your key is stored and also where a list of safe SSH hosts is kept. There you will see the files id_dsa and id_dsa.pub. The first is your private key and should never be given out. The second is your public key, which is safe for distribution. You need to copy the public key to each server you want to connect to via key-based SSH.

Using `scp`, you can copy the public key over to your server, like this:

```
scp id_dsa.pub 10.0.0.1:
```

This places id_dsa.pub in your home directory on 10.0.0.1. The next step is to SSH into 10.0.0.1 normally and set up that key as an authorized key. So, you can SSH in as yourself and then run:

```
touch .ssh/authorized_keys
cat id_dsa.pub >> .ssh/authorized_keys
chmod 400 .ssh/authorized_keys
```

The `touch` command creates the authorized_keys file (if it does not exist already); then you use `cat` to append the contents of id_dsa.pub to the list of already authorized keys. Finally, `chmod` is used to make authorized_keys read only.

With that done, you can type `exit` to disconnect from the remote machine and return to your local machine. Then you can try running `ssh` again. If you are prompted for your passphrase, you have successfully configured key-based authentication.

That is the current machine secured, but what about every other machine? It is still possible to log in from another machine using only a password, which means your remote machine is still vulnerable.

The solution to this is to switch to root and edit the /etc/ssh/sshd_config file. Look for the `PasswordAuthentication` line and make sure it reads `no` (and that it is not commented out with a #). Save the file, and run `kill -HUP \`cat /var/run/sshd.pid\`` to have `sshd` reread its configuration files. With that done, `sshd` accepts only connections from clients with authorized keys, which stops crackers from brute-forcing their way in.

> **TIP**
> For extra security, consider setting `PermitRootLogin` to `no` in /etc/ssh/sshd_config. When this is set, it becomes impossible to SSH into your machine using the root account—you must connect with a normal user account and then use `su` or `sudo` to switch to root. This is advantageous because most brute-force attempts take place on the root account because it is the only account that is guaranteed to exist on a server.
> Also, even if a cracker knows your user account, she has to guess both your user password and your root password to take control of your system.

## Remote X

Everything we have looked at so far has been about command-line remoting, with no mention of how to bring up a graphical user interface. There are two ways of doing this in Linux: the X Display Manager Control Protocol (XDMCP) and Virtual Network
