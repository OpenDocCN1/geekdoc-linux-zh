With this file in place, this next section reviews a couple of additional examples showing what you can do with the rsh and rcp commands. While logged in to stockholm, you can display a list of the processes running on oslo without ever "logging in" to oslo by using this command:

```
$ rsh oslo ps aux
```

The output from this command is displayed on stockholm's screen. If you want to store the results in a file on oslo, the command would include a redirection operator enclosed in single quotes so that your local shell doesn't interpret it and create the file on stockholm:

```
$ rsh oslo ps aux '>1 processlist
```

The rcp command lets you copy files between any two computers that are running the r-utilities. You simply include the host name as part of the file specification. For example, while logged in to stockholm, you can copy a file named processlist from oslo to stockholm using this command:

```
$ rcp oslo:processlist /home/nwells/
```

You can also copy between two other computers (not the one you are sitting at). For example, while logged in at stockholm, you could copy a file from oslo to helsinki with this command (assuming the .rhosts files on both oslo and helsinki include the stockholm host name with nwells as the user name):

```
$ rcp oslo:processlist helsinki:/temp/processlist_backup
```

# Secure Shell (SSH)

The simplest description of Secure Shell (SSH) is that it is an encrypted version of Telnet—it lets you access a remote host the same way Telnet does, but without the danger that everyone on the network can see what you are transmitting. Everything sent by SSH is encoded so that only the authorized recipient can read it. This simple explanation, however, hides the power of SSH: unlike Telnet, SSH can act as a complete networking toolkit.

For example, protocols such as FTP and remote sessions of the X Window System are completely unprotected. However, you can start an SSH session and tie an FTP or X session to it, so that all traffic for the FTP or X connection is transmitted using SSH—and is completely encrypted.

Like other Linux Internet services, ssh consists of a client utility (ssh or slog in) and a server program (sshd). In addition, the SSH package includes utilities such as scp, which acts like rcp, letting you copy files between any two computers on your network with full encryption. SSH is available as a commercial product—see www.ssh.com. Linux distributions rely on the free version of SSH, called OpenSSH—see www.openssh.org. OpenSSH is installed by default on many Linux systems, including Red Hat Linux.