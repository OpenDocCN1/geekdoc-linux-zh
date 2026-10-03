most often best to disable DNS in sshd and stick with IP addresses.

# no-agent-forwarding

This disables SSH agent forwarding (see Chapter 7) for this key.

```
no-agent-forwarding ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAA...
```

# no-x11-forwarding

This (wait for it…) disables X forwarding (see Chapter 8).

```
no-x11-forwarding ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAA...
```

# no-pty

Sessions that authenticate with this key will not be granted a pseudo-terminal.

Many programs that run under automation do not need a terminal.

```
no-pty ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAA...
```

# no-user-rc

This disables sshd’s login script checks, as discussed in “Running Commands at Login” at the beginning of this chapter.

```
no-user-rc ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAA...
```

# permitopen="host:port"

The permitopen keyword restricts local port forwarding so that it can only attach to the given hostname or IP address and port on the local machine. If the server doesn’t allow local port forwarding, this has no effect.

```
permitopen="localhost:25" ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAA...
```

This example allows port forwarding to connect to port 25 on 127.0.0.1, but nothing else.

You can set permitopen to none to disallow all port forwarding.

# tunnel="n"

Use a specific tunnel device number for SSH tunnels (see Chapter 13).

```
tunnel="3" ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAA...
```

# restrict

By default, anything not denied is permitted. The restrict keyword inverts that, blocking everything unless you specifically allow it. You can use the keywords agent-forwarding, port-forwarding, pty, user-rc, and X11-forwarding to turn those functions back on.

# Using Multiple Keywords

As with just about everything in OpenSSH, you can use multiple keywords in one entry. Separate keywords with commas, not spaces.

```
restrict,command="/usr/local/scripts/backup.sh" ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAA...
```

# Keys and Automated Programs

Lots of us want to use SSH as a secure transport for other programs. Maybe you have a custom monitor program, or a backup process that runs over rsync. Such clients should never have a hard-coded username and password; in addition to being insecure, it’s neither maintainable nor scalable. One solution is to use an