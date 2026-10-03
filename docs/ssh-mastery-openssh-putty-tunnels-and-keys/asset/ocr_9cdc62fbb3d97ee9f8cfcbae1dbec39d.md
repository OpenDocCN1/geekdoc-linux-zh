# Chapter 3: The OpenSSH Server

The OpenSSH server sshd is highly configurable and lets you restrict who may connect to the server, what actions those users can take, and what actions it permits. Every modern Unix-like operating system comes with sshd installed as part of the base operating system.

We’ll look at some basics of running sshd, and proceed to various global configuration options. More specific options get discussed in relevant chapters of this book.

# Is sshd Running?

From a client, the simplest way to test if a server is running an accessible SSH daemon is to try to log into the server. While that’s great when everything works, a failure to connect means that either the client or server could be busted, or maybe you have a packet filter in the middle. SSH normally runs on TCP port 22. Use netcat(1) to see if you can access the daemon.

```
$ nc -v devio.us 22
Connection to devio.us 22 port [tcp/ssh] succeeded!
SSH-2.0-OpenSSH_7.0
^C
```

When you connect over raw TCP, sshd returns a banner giving the SSH protocol version, the SSH server software, and the software version. This host uses SSH protocol 2, provided by OpenSSH version 7.0.

If you don’t get something similar perhaps sshd isn’t running, or maybe you have a packet filter in the way.

From the server, check and see if the sshd process is running.

```
$ ps ax | grep sshd
626 - Is 0:00.03 /usr/sbin/sshd
31960 - Is 0:00.38 sshd: mwlucas [priv] (sshd)
44387 - S 0:05.75 sshd: mwlucas@pts/0 (sshd)
```

This host shows three sshd(8) processes. The first, PID 626, shows plain old /usr/sbin/sshd. It’s the master process that listens to TCP port 22.

The second process, PID 31960, is the privileged process that handles my SSH connection into this host. The third, PID 44387, is the unprivileged child process that handles your login session. OpenSSH improves security through privilege separation, discussed in “Protecting the SSH Server” at the end of this chapter. If someone has deliberately disabled privilege separation and is running sshd insecurely, you won’t see the unprivileged sessions.¹

If sshd isn’t running, enable it through your operating system configuration tool.

# Configuring sshd

Most operating systems run sshd as a standalone server without any command-