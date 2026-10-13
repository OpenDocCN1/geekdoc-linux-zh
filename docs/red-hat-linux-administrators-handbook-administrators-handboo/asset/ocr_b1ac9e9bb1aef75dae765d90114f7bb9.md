/etc/hosts.allow. The /etc/hosts.allow file will have lines such as the following:

```
in.ftpd: .nitec.com EXCEPT reboot.nitec.com
ALL EXCEPT in.ftpd: .nitec.com
```

The first line states that the in.ftpd daemon is allowed to service all the hosts in the nitec.com domain except reboot.nitec.com. The next line states that all daemons (that is, services) except the FTP service (in.ftpd) are allowed to service all the hosts in the nitec.com domain.

The TCP wrapper can also be configured using an extended host access control language that uses the following configuration syntax:

```
daemon list : client list : option : option : . . .
```

An option can be any of the keywords shown in Table 15-8.

# Table 15-8 Acceptable Keywords in Extended Host Access Control Language

| Keyword | Description |
|---|---|
| ALLOW client list | Used to permit access to one or more hosts. For example, ALL : your-domain.com : ALLOW allows all the hosts in your-domain.com access to all the inetd-run services. |
| DENY client list | Used to restrict access to one or more hosts. For example, ALL : bad-guy-domain.com : DENY denies all the hosts in bad-guy-domain.com access to all the inetd-run services. |
| SPAWN shell command | Used to execute a shell command. The command is run such that STDIN, STDOUT, and STDERR are directed to /dev/null. This makes sure the command does not interfere with the client software on the host trying to access a service. The character expansion discussed earlier applies before the command is called. |
| TWIST shell command | Used to execute a shell command. The command is run such that STDIN, STDOUT and STDERR are directed to the client. The character expansion discussed earlier applies before the command is called. Use TWIST as the last option in the configuration line. I recommend using TWIST only for TCP-based services. |
| LINGER seconds | Used to make the kernel retry data delivery for a specified number of seconds. |