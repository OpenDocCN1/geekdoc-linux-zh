The ssh-server package contains default /etc/ssh/sshd_config and /etc/ssh/ssh_config files that work well for most purposes. It also contains an /etc/rc.d/init.d/ssh script for starting the sshd daemon when you boot the host. To start the sshd daemon manually, run /etc/rc.d/init.d/ssh start. If you want to start it automatically when the server boots, create an appropriate softlink in the /etc/rc.d/rc7.d directory that corresponds to your server's initdefault runlevel.

The ssh and ssh-clients packages contain several programs. The most useful are ssh and scp. ssh allows you to log on to a remote host, execute remote programs, and redirect ports from the local host to the remote host and vice versa. scp, which allows you to copy files securely from one host to another, is a replacement for the rcp program.

# The ssh Command

The ssh command is used to log on to a remote server and execute a command. It has the following syntax:

```
ssh options host options command
```

ssh also handles X connection forwarding. Whenever you log on to a remote host using ssh from a host that is running X Windows, sshd creates a dummy X server and sets the DISPLAY variable to point to it. All X traffic going to this dummy server is actually forwarded to the X server on your local host. X authentication is automatically taken care of via xauth. That way, the X traffic is also encrypted and secure. You don't have to do anything to make this happen, just log on to the remote server from an X session.

There are many options to the ssh command that can be included either before or after the hostname. The most common options to ssh are listed in Table 20.11.

| **TABLE 20.11** Most Common ssh Options | |
|---|---|
| Option | Meaning |
| -f | Send process to background after authentication. Useful when you need to enter a password. |
| -1 user | Log in as user to the remote server. |
| -o 'option' | Set option in the same format as the configuration file. Useful for some options that don't have command-line switch equivalents. |
| -v | Activate verbose mode. Useful for debugging connections. |
| -C | Compress. All data in the connection will be compressed. Useful especially over modem lines. The compression algorithm used is the same one used by gzip. |