For the ssh-agent to start automatically when an X server starts, you simply enter the following parameter in the file sys.xsession:

`usessh="yes"`

```
usessh="yes"
```

This entry is already set by default in SUSE Linux Enterprise Desktop 10.

After entering the yes parameter, the ssh-agent starts automatically the next time the user logs in to the graphical interface. The agent running in the background must be given the passphrase once, as in the following:

```
geeko@a10:~> ssh-add .ssh/id_dsa
Enter passphrase for .ssh/id_dsa:
Identity added: .ssh/id_dsa (.ssh/id_dsa)
```

For subsequent connections in which authentication takes place with the public key procedure, a passphrase now no longer has to be given. This ssh-agent takes care of the private keys. When the X server is terminated, the ssh-agent is also closed. The passphrase is never stored in a file; the private keys are stored in memory by the ssh-agent only until the user has logged out again.

![](bbox=[0.037, 0.444, 0.224, 0.515])

# Exercise 5-4: Perform Public Key Authentication

In this exercise, you practice using SSH with public key authentication. You need to work with a partner in this exercise.

Create an ssh-key pair, add the public key to the file `~geeko/.ssh/authorized_keys` on your partner’s computer, and note the difference between logging in with or without a public key. Then, use the ssh-agent to cache the private key and log in again to your partner’s machine as geeko.

As root, change the SSH server configuration to allow only public key authentication. Restart sshd and, as root, try `ssh geeko@localhost`.

# Detailed Steps to Complete This Exercise

To perform public key authentication, do the following:

+   1. As user geeko, open a terminal window.
+   2. Generate an RSA key pair:
+      a. From the terminal window, enter
+      b. Accept the default location for the key (`/home/geeko/.ssh/id_rsa`) by pressing Enter.
+      c. Enter a passphrase or secret.
+         Information on your key pair, such as the location of your identification and the public key, is displayed.

```
ssh-keygen -t rsa
```