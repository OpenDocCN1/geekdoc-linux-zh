To grant the users Jason and Scott on any remote host access to any account on the local system, add the following to /etc/hosts.equiv.

+   + jason scott

For the purposes of this chapter, you can allow access to the root account from a particular host. For example, to allow access from the machine server1, you can add server1 to root's hosts file. If, instead, you added server1 root to /etc/hosts.equiv, you would have allowed root access not just from the remote root user, but from any user on the client.

Now that you can log in as root, you can perform a variety of remote administrative tasks. For example, use these commands to copy a new version of /etc/inetd.conf to another server and restart inetd.

```
# rcp /etc/inetd.conf server1:/etc/inetd.conf
# rsh server1 -kill HUP inetd
```

Setting up this access for two or three servers may seem like overkill, but when you are intervening tens or hundreds of servers, the r-commands can be invaluable administrative tools.

# The Security Dangers of r-commands

The Berkeley r-commands were the tools of choice for remote command execution before the advent of the Internet in the early 1990s. But r-commands provide little security—the primary concern in today's publicly accessible networks. Not only is r-command network traffic unencrypted, but of even greater concern is the trust servers place in the clients.

On a server that allows the user to log in from any host, for example, a malicious user could easily install his own system on the same network with a user that has the same UID as the one on the server. That second then would be able to log to the server without a password. This prospect is even scarier if you have several allowances for access as root.

![](bbox=[0.125, 0.631, 0.2, 0.683])

> Host Restrictions Can Be Compromised
Even r-command restrictions can be compromised by forging the source address in IP packets. This is called spoofing, and you can read more about it in Chapter 13, "Implementing System Security."

# Using SSH Instead of the r-commands

One solution to the r-command security problem is to use r-commands only on trusted networks. When that isn't possible, you can use SSH, the secure shell. In addition to using an encrypted channel, SSH provides public key authentication, which can be used for password-less logins. OpenSSH, with origins in the OpenBSD operating system, is quickly becoming the most popular SSH server for Unix systems. It is freely available from http://www.openssh.org and comes standard with many versions of Linux.