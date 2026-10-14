
- 6. The server also calculates a checksum and, if they are identical, the user has authenticated successfully.
- 7. If public key authentication fails and password authentication is allowed, the user is asked for the login password.

The secret key should be protected by a passphrase. Without passphrase protection, simply owning the file containing the private key is sufficient for a successful authentication. However, if the key is additionally protected with a passphrase, the file is useless if you do not know the passphrase.

## Create a Key Pair

You create a key pair with the ssh-keygen command. A different key is required for SSH1 than for SSH2. For this reason, you need to create a separate key pair for each version.

Use the option -t keytype to specify the type of key:

- `ssh-keygen -t rsa1` generates a key pair for SSH1.
- `ssh-keygen -t rsa` and `ssh-keygen -t dsa` generate key pairs for SSH2.

The keys are stored in the directory ~/.ssh. For SSH1, the default for these files is ~/.ssh/identity (private key) and ~/.ssh/identity.pub (public key). For SSH2, the default files are ~/.ssh/id_rsa and ~/.ssh/id_dsa, respectively, plus the corresponding public key files with the .pub extension.

The following shows how a key pair for the protocol version 2 is generated using option -t (required) to generate a DSA key pair:

```
geeko@dal0:~> ssh-keygen -t dsa
Generating public/private dsa key pair.
Enter file in which to save the key (/home/geeko/.ssh/id_dsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/geeko/.ssh/id_dsa.
Your public key has been saved in /home/geeko/.ssh/id_dsa.pub.
The key fingerprint is:
ef:73:c6:f6:8a:ff:9d:d1:50:01:cf:07:65:c5:54:8b geeko@dal0
```

## Configure and Use Public Key Authentication

For authentication using RSA or DSA keys, you need to copy the public key to the server, and then append the public key to the file ~/.ssh/authorized_keys.

For example, you can copy the key to the server with the scp command, as in the following:

```
geeko@dal0:~> scp .ssh/id_dsa.pub da50:geeko-pubkey
```

The key should then be added to the file `~/.ssh/authorized_keys` in such a way that the existing keys are not overwritten, as in the following:

```
geeko@da10:~> ssh da50
Password:
Last login: Tue May 30 12:03:29 2006 from da10.digitalairlines.com
geeko@da50:~> cat geeko-publickey >> ~/.ssh/authorized_keys
geeko@da50:~> exit
geeko@da10:~>
```

![](img/9129877170834ca9d5fdac5319bf5f12_160_0.png)

The utility `ssh-copy-id` can be used to simplify the previous steps of copying the key to the other computer and appending it to `~/.ssh/authorized_keys`. For more information, enter `man ssh-copy-id`.

You can now launch the client to see if authentication with the DSA key works properly, as in the following:

```
geeko@da10:~> ssh da50
Enter passphrase for key '/home/geeko/.ssh/id_dsa':
Last login: Tue May 30 12:03:40 2006 from da10.digitalairlines.com
geeko@da50:~>
```

You can use the option `-i` to enter the filename for a private key with a different name or location.

When authentication is done with keys, the passphrase is required when logging in to the server or when copying with scp. If you mistype your passphrase three times, you are asked for your usual login password. (The sshd configuration allows you to change this behavior; see Table 5-3.).

The ssh-agent can be used to avoid having to type this passphrase upon each connection. After starting the ssh-agent, you need to enter the passphrase using the ssh-add command. After that, the ssh-agent monitors all SSH requests and provides the required private key as necessary.

The ssh-agent serves as a wrapper for any other process (such as for a shell or the X server). The following example shows the start of a bash shell through the ssh-agent:

```
geeko@da10:~> ssh-agent bash
geeko@da10:~> ssh-add .ssh/id_dsa
Enter passphrase for .ssh/id_dsa:
Identity added: .ssh/id_dsa (.ssh/id_dsa)
```

For all ssh or scp commands entered from this shell (for which a key authentication is configured), the agent will automatically provide the private key.

You can also use the ssh-agent with a graphical login. When you log in to the graphical interface, an X server is started. If you log in by using a display manager, the X server loads the file `/etc/X11/xdm/sys.xsession`.

For the ssh-agent to start automatically when an X server starts, you simply enter the following parameter in the file sys.xsession:

`usessh="yes"`

```
usessh="yes"
```

This entry is already set by default in SUSE Linux Enterprise Desktop 10.

After entering the yes parameter, the ssh-agent starts automatically the next time the user logs in to the graphical interface. The agent running in the background must be given the passphrase once, as in the following:

```
geeko@da10:~> ssh-add .ssh/id_dsa
Enter passphrase for .ssh/id_dsa:
Identity added: .ssh/id_dsa (.ssh/id_dsa)
```

For subsequent connections in which authentication takes place with the public key procedure, a passphrase now no longer has to be given. This ssh-agent takes care of the private keys. When the X server is terminated, the ssh-agent is also closed. The passphrase is never stored in a file; the private keys are stored in memory by the ssh-agent only until the user has logged out again.

![](img/9129877170834ca9d5fdac5319bf5f12_161_0.png)

## Exercise 5-4: Perform Public Key Authentication

In this exercise, you practice using SSH with public key authentication. You need to work with a partner in this exercise.

Create an ssh-key pair, add the public key to the file `~geeko/.ssh/authorized_keys` on your partner’s computer, and note the difference between logging in with or without a public key. Then, use the ssh-agent to cache the private key and log in again to your partner’s machine as geeko.

As root, change the SSH server configuration to allow only public key authentication. Restart sshd and, as root, try `ssh geeko@localhost`.

### Detailed Steps to Complete This Exercise

To perform public key authentication, do the following:

- 1. As user geeko, open a terminal window.
- 2. Generate an RSA key pair:
  - a. From the terminal window, enter
  - b. Accept the default location for the key (`/home/geeko/.ssh/id_rsa`) by pressing Enter.
  - c. Enter a passphrase or secret.
Information on your key pair, such as the location of your identification and the public key, is displayed.

```
ssh-keygen -t rsa
```

- 3. Add the RSA public key to your partner’s ~geeko/.ssh/authorized_keys file:
  - a. Using the password novell, copy the file to your partner’s home directory of geeko by entering the following:
`scp .ssh/id_rsa.pub geeko@partner_IP_address`
  - b. Log in as geeko to your partner’s computer using ssh by entering
`ssh -l geeko partner_IP_address`
  - c. Enter `ls -al`.
Look for an .ssh directory.
  - d. (Conditional) If an .ssh directory does not exist, create it by entering
`mkdir .ssh`
  - e. Copy the public key to the ~/.ssh/authorized_keys file by entering
`cat id_rsa.pub >> .ssh/authorized_keys`

- 4. Log out from the partner’s computer by entering exit.
- 5. Log in as geeko to your partner’s computer using ssh by entering
`ssh -l geeko partner_IP_address`
You are prompted for a passphrase, not a password.
- 6. Log in by entering secret; then log out by entering exit.
- 7. To track authentication, start the ssh-agent by entering
`ssh-agent bash`
- 8. Add your private key to the agent for authentication by entering
`ssh-add .ssh/id_rsa`
Then enter a passphrase of secret.
- 9. Log in as geeko to your partner’s computer using ssh by entering
`ssh -l geeko partner_IP_address`
This time you are not prompted for a password or a passphrase.
- 10. Log out from your partner’s computer by entering exit.
- 11. Switch to user root (su -, password n0v3ll).
- 12. Open the /etc/ssh/sshd_config file in an editor of your choice, such as gedit.
  - a. Find the line containing PasswordAuthentication and make sure it is set to no.
  - b. Find the line containing UsePAM and change its setting from yes to no.
  - c. Save the file and close the editor.
