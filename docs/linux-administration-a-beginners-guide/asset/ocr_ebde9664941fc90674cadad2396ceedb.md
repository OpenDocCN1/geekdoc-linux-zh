In order for SSH2 to do this, we need to tell it where the SSH1 server daemon is. This is done by editing the `/etc/ssh2/ssh2d_config` file. Look for the lines that read as follows:

```
```text
Ssh1Compatibility	yes
Ssh1Path	<set by configure>
```
```

The first line, `Ssh1Compatibility`, has already been set for us by default. Now we just need to tell it where the SSH1 daemon is located. Unless it’s been moved, it should be in `/usr/local/sbin/sshd`. So we need to remove the comment on the second line and set the path to `/usr/local/bin/ssh2d1` instead:

```
```text
Ssh1Path	/usr/compat/bin/sshd1
```
```

You can also do this for the SSH clients that were compiled as part of this package. This allows you to name your SSH2 client `ssh` and have it automatically kick over to “ssh1” if it contacts an SSH server that is still running version 1. To make this change, insert the following two lines into the `/etc/ssh2/ssh2d_config` file:

```
```text
Ssh1Compatibility	yes
Ssh1Path	/usr/compat/bin/ssh1
```
```

# Server Startup and Shutdown

If you want users to be able to login to your system via SSH, you will need to start the server process at boot time. The clean and proper way to do this is to create a startup script (as we discussed in Chapter 7) for the `/usr/local/compat/bin/ssh2d` process to start the Secure Shell server. However, for the last several years I’ve been using SSH and have never once had to shut it down—so here is the “cheat” technique: You can edit the `/etc/rc.d/rc.local` file so that the last instruction in it is as follows:

```
```bash
# Start the SSH server daemon
# 
# /usr/compat/bin/ssh2d
```
```

If for some reason you do need to stop the SSH server but not the entire system, you can simply kill the sshd process. To find out the server’s process number, use the `ps` command:

```
```bash
[root@ford /root]# ps -C sshd
  PID TTY          TIME CMD
 26847 ?        00:00:00 sshd
```
```

In this case, the PID for sshd was 26847, so to kill this process, you’ll type

```
```bash
[root@ford /root]# kill 26847
```
```

You can of course restart the daemon at any time, by simply running

```
```bash
[root@ford /root]# /usr/compat/bin/ssh2d
```
```