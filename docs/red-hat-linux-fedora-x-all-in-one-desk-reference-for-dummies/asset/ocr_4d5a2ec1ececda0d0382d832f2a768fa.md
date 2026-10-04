# Setting Up Simple Firewalls 563

A user who wants to log in using ssh must also generate the public-and-private key pair. For example, here is what I do I can log in from another system on Fedora Core system using SSH:

+   1. I type the following command to generate the DSA keys for use with SSH2:
ssh-keygen -d

I am prompted for a passphrase and the last message inform me my public key is saved in /home/naba/.ssh/id_da.pub.

+   2. I copy my public key — the /home/naba/.ssh/id_da.pub file — to the remote system and save it as the ~/.ssh/authorized_keys2 file which name refers to the authorized_keys file in the .ssh subdirectory of the other system, ensuring that the remote system is also Fedora Core system. The note in the authorized_keys2 file refers to the SSH2 protocol.

+   3. To log in my account on Fedora Core system (with host name l1np200), I type the following command on the remote system:

```
ssh l1np200 -l naba
```

+   4. When prompted for my password on the l1np200 host, I enter the password and log in to this account with the following equivalent command:

```
ssh naba@l1np200
```

If I simply want to copy a file securely from the l1np200 system, I can use like this:

```
scp l1np200:/etc/ssh/ssh_config .
```

This command securely copies the /etc/ssh/ssh_config file from the l1np200 host to the system from which I type the command.

# Setting Up Simple Firewalls

An Internet firewall is an intermediary between your internal network and the Internet. The firewall controls access to and from the protected internal network.

If you connect an internal network directly to the internet, you have to make that every system on the internal network is properly secured — which can be nearly impossible because only one careless user can render the entire internal network vulnerable. A firewall is a single point of connection to the Internet: You can direct all your efforts toward making firewall system a daunting barrier to unauthorized externals.