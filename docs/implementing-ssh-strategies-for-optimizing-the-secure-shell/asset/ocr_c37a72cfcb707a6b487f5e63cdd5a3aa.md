3. Enter the name of the key pair (I will call ours Shreya); then enter a passphrase, and confirm the passphrase:

```
Enter file in which to save the key (/root/.ssh/id_rsa): Shreya
Enter passphrase (empty for no passphrase): 
Enter same passphrase again:
```

4. After you have confirmed the passphrase, both the public and private keys should be generated. In this case, the names will be Shreya.pub for the public-key file and Shreya for the private-key file. The key fingerprint will be displayed on the shell or command prompt:

```
Your identification has been saved in Shreya.
Your public key has been saved in Shreya.pub.
The key fingerprint is:
ed:1e:67:22:29:d8:81:c9:b4:ee:0d:f5:55:0d:cf:5c
```

5. OpenSSH client keys have been generated!

After the creation process has been completed, copy the OpenSSH client key to the SSH server, specifically to the .ssh folder in the users' home directory (for example, /home/<username>/.ssh/PublicKey.pub. The following section demonstrates how to use an OpenSSH key on an OpenSSH server, a SSH Communications' SSH server, and a VanDyke VSHELL SSH server.

# How to Use an OpenSSH Key on an OpenSSH Server

After the OpenSSH public key has been securely uploaded to the SSH server, typically in the users' home directory (/home/Shreya/.ssh/Shreya.pub or Program Files\OpenSSH\ssh\Shreya.pub), you also need to append the key to the authorized key-list file, which is labeled authorized_keys in the users' home directory (/home/<username>/.ssh/authorized_keys). Example syntax is as follows on the server machine:

```
[Shreya@OpenSSH]$cat Shreya.pub >> /home/<username>/.ssh/authorized_keys
```

Furthermore, the permissions on the public-key and private-key pairs need to be protected in order to be used. Set the following permission on the key files generated on the client machine:

```
[Shreya@localhost]$chmod 600 Shreya
[Shreya@localhost]$chmod 600 Shreya.pub
```

Once you have made the key pairs, uploaded the public-key file to the appropriate home directory, added the key to the authorized_keys file, and set the correct permissions, you should be able to log in with the public key. Sample syntax follows on the client machine:

```
[Shreya@localhost]$ssh <SSH server IP address> -i Shreya
```