# SYNTAX

```
ssh [-option(s)] [-option argument(s)] [command]
```

Purpose: ssh (SSH client) is a program for logging into a remote machine and for executing commands on a remote machine. It is intended to replace rlogin and rsh, and provide secure encrypted communications between two untrusted hosts over an insecure network.

Output: A remote connection over a secure channel to a host on a network or the Internet

# Common Options and Features:

+   -D [bind_address:]port Specifies a local "dynamic" application-level port forwarding. This works by allocating a socket to listen to port on the local side, optionally bound to the specified bind_address.

+   -L [bind_address:]port:host:hostport Specifies that the given port on the local (client) host is to be forwarded to the given host and port on the remote side.

+   -l login_name Specifies the user to log in as on the remote machine. This also may be specified on a per-host basis in the configuration file.

You can log in to a remote host or execute a command on a remote host with the ssh command just like you do with the rsh command. For example, in the following session, from a PC-BSD client machine, you start an ssh session on a remote host ssh server named 192.168.0.12 using the default username (which in this case is the same username you have on the local client machine), and then log out of the remote host:

```
% ssh 192.168.0.12
The authenticity of host '192.168.0.12 (192.168.0.12)' can't be established.
RSA key fingerprint is 37:a2:db:ce:97:17:ce:37:26:bf:58:9d:a2:ed:1c:0f.
No matching host key fingerprint found in DNS.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.0.12' (RSA) to the list of known hosts.
Password: xxxxx
Last login: Tue Sep 23 08:51:38 2014
OpenIndiana (powered by illumos) SunOS 5.11 oi_151a9
November 2013
$
...
$ logout
Connection to 192.168.0.12 closed.
%
```