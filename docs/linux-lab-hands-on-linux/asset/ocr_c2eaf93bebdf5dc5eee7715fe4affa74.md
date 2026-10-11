# Status Of SSH

You can test whether or not the SSH process is running by using the following syntax:

```
root@netmon tmp]# pgrep sshd
```

You should get a response of plain old process ID numbers.

# The /etc/ssh/sshd_config File

The SSH configuration file is stored in the sshd_config file in the /etc/ssh directory.. By default SSH listens on all your NICs and uses TCP port 22. Open the ssh configuration file in the vi editor. It shows the following output:

```
# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented. Uncommented options change a
# default value.

#Port 22
#Protocol 2,1
#ListenAddress 0.0.0.0
#ListenAddress ::
```

# SSH Versions 1 and 2

The original encryption scheme of SSH was adequate but was eventually found to have a number of limitations. Therefore, version 2 was launched. It is advisable to operate your system with version 2 by setting the protocol statement in the /etc/ssh/sshd_config file to 2. You should restart SSH to make the changes effective..

```
#
# File: /etc/ssh/sshd_config
#
Protocol 2
```

In the preceding section you learned the SSH version 1 and 2 let’s now learn to change the TCP port using SSH.

# Change the TCP Port on Which SSH Listens

You can change the TCP port using SSH to secure your TCP/IP network you can change port 22 to a location that would not t interfere with other applications on your system, such as port 435.

Let’s perform the following steps to do this:

+   1.  Use the netstat command to ensure your system is not listening on port 435. using grep to filter out everything that doesn’t have the string “435”:

```
[root@netmon root]# netstat -an | grep 435
[root@netmon root]#
```