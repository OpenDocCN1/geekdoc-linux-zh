files id_dsa and id_dsa.pub. The first is your private key and should never be given out. The second is your public key, which is safe for distribution. You need to copy the public key to each server you want to connect to via key-based SSH.

Using `scp`, you can copy the public key over to your server, like this:

```
scp id_dsa.pub 10.0.0.1:
```

This places id_dsa.pub in your home directory on 10.0.0.1. The next step is to SSH into 10.0.0.1 normally and set up that key as an authorized key. So, you can SSH in as yourself and then `type`

```
touch .ssh/authorized_keys
cat id_dsa.pub >> .ssh/authorized_keys
chmod 400 .ssh/authorized_keys
```

The `touch` command creates the authorized_keys file (if it does not exist already); then you use `cat` to append the contents of id_dsa.pub to the list of already authorized keys. Finally, `chmod` is used to make authorized_keys read only.

With that done, you can type `exit` to disconnect from the remote machine and return to your local machine. Then you can try running `ssh` again. If you are prompted for your passphrase, you have successfully configured key-based authentication.

That is the current machine secured, but what about every other machine? It is still possible to log in from another machine using only a password, which means your remote machine is still vulnerable.

The solution to this is to switch to root and edit the /etc/ssh/sshd_config file. Look for the `PasswordAuthentication` line and make sure it reads `no` (and that it is not commented out with a #). Save the file, and run `kill -HUP `cat /var/run/sshd.pid` to have `sshd` reread its configuration files. With that done, `sshd` accepts only connections from clients with authorized keys, which stops crackers from brute-forcing their way in.

> TIP
> For extra security, consider setting `PermitRootLogin` to `no` in /etc/ssh/sshd_config. When this is set, it becomes impossible to SSH into your machine using the root account—you must connect with a normal user account and then use `su` or `sudo` to switch to root. This is advantageous because most brute-force attempts take place on the root account because it is the only account that is guaranteed to exist on a server.
> Also, even if a cracker knows your user account, she has to guess both your user password and your root password to take control of your system.

# Remote X

Everything we have looked at so far has been about command-line remoting, with no mention of how to bring up a graphical user interface. There are two ways of doing this in Linux: the X Display Manager Control Protocol (XDMCP) and Virtual Network