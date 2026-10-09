The randomart image renders a system's host key in a visual format that can be easier to recall than a host key fingerprint (see the preceding example). Making it easier for a user to detect a change in the fingerprint can mean that a user will be aware when he is connecting to a system other than the one he intended to connect to.

# ssh-agent: HOLDS YOUR PRIVATE KEYS

# Personal key encryption, passphrase, and ssh-agent

The private part of your personal authentication key is kept in a file that only you can read. When you set up automatic login on a remote system, any user who has access to your account on the local system also has access to your account on the remote system because that user can read the private part of your personal key. Thus, if a malicious user compromises your account or the **root** account on the local system, that user then has access to your account on the remote system.

Encrypting the private part of your personal key protects the key and, therefore, restricts access to the remote system should someone compromise your local account. However, if you encrypt your personal key, you must supply the passphrase you used to encrypt the key each time you use the key, negating the benefit of not having to type a password when logging in on the remote system. You can use `ssh-agent` to remember the private key of your personal key for the duration of a session; you supply your passphrase once, at the beginning of the session.

# Storing private keys on a removable medium

You can store the private keys on a removable medium, such as a USB flash drive, and use your `~/.ssh` directory as the mount point for the filesystem stored on this drive. You might want to encrypt these keys with a passphrase in case you lose the flash drive.

When you use `ssh-keygen` to generate a public/private key pair, you have the option of specifying a passphrase. If you specify a passphrase, you must supply that passphrase each time you use the key. The result is, when you set up a key pair to avoid specifying your password when you log in on a remote system using ssh, you end up supplying the passphrase instead.

The `ssh-agent` utility allows you to use a passphrase with your personal key while entering the key one time, at the beginning of each session. When you log out, `ssh-agent` forgets the key. Because Fedora/RHEL is set up with `ssh-agent` enabled for X sessions, it is very easy to use in a graphical environment. It is also easy to set up in a textual environment.

If you are running a textual session (not within a terminal emulator window), you must give the following command to enable `ssh-agent`. If you are running a graphical session, skip this step (`ssh-agent` is set up in the files in `/etc/X11/xinit/xinitrc`).

```
```shell
$ eval $(ssh-agent -s)
Agent pid 9882
```
```

Once `ssh-agent` is enabled, use `ssh-add` to specify the passphrase for a key pair:

```
```shell
$ ssh-add -- ~/.ssh/id_rsa
Enter passphrase for /home/sam/.ssh/id_rsa:
Identity added: /home/sam/.ssh/id_rsa (/home/sam/.ssh/id_rsa)
```
```