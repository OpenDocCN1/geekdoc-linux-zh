```
% /etc/rc.d/sshd restart
Stopping sshd.
Waiting for PIDS: 1523
Starting sshd.
%
```

An alternative way of starting the ssh daemon is to start an sshd server automatically at boot time by adding the following line to the /etc/rc.conf file:

```
sshd_enable="YES"
```

Now start the sshd server by typing the following on the command line:

```
% /etc/rc.d/sshd start
```

+   1. Configuration of ssh on Solaris

On the local client machine, examine the files /etc/ssh_config and /etc/ssh/sshd_config, the client-side and server-side configuration files for ssh, respectively. The lines in these files that are uncommented (i.e., no # as the first character), are the configuration settings for your ssh sessions, both as client and as server, respectively.

+   2. Starting or restarting sshd on Solaris

To start sshd on the remote server, if it is not already running, run the following command:

```
$ svcadm enable svc:/network /ssh:default
```

To restart sshd on the remote server, type the following:

```
$ svcadm restart svc:/network/ssh:default
```

# 11.8.10.2 The ssh Command

The ssh command allows you to perform basically the same tasks that you can perform with the telnet, rlogin, and rsh commands, but in a more secure manner. You are allowed to log in to the remote host or execute a command on it if the ssh server running on the remote host finds your machine name in the /etc/host.equiv or /etc/shosts.equiv file and your login name is the same on your machine and the remote machine. You are also allowed to log in to the remote host if your login names are different on the local and remote hosts, and your local machine's name and your login name on it are contained in the ~/.rhosts or ~/.shosts file. Additional security features are used by ssh, including public-key cryptography, to authenticate a user and its host before allowing the user to log in to the remote machine. We describe only some of the rather basic features of the ssh command that are needed for remote login, remote execution of commands, and file transfer between your client and the server machines. Here is a brief description of the ssh command: