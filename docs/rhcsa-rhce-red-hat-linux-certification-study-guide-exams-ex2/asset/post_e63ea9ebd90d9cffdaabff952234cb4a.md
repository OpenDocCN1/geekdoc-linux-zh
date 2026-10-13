
coverage of xinetd services to a minimum. Nevertheless, xinetd services are “Network Services,” an important subset of the exam objectives.

The xinetd (also known as the Extended Internet Services Daemon) service can start a number of server daemons simultaneously. The xinetd service listens for connection requests for all active servers with scripts in the /etc/xinetd.d directory. There’s a generic configuration file for xinetd services, /etc/xinetd.conf. The scripts in the /etc/xinetd.d directory function as service-specific configuration files.

## Generic xinetd Configuration

The generic configuration for xinetd services is stored in the /etc/xinetd.conf file. As RHCE candidates need to configure services only for “basic operation,” this chapter analyzes only the active directives in this file. First, a number of default settings are enabled with the following command:

```
defaults
```

This allows services such as rsync to retain their default TCP/IP ports (873) within the xinetd service.

This is followed by

```
log_type = SYSLOG daemon info
```

which specifies logging through the rsyslog daemon as described in Chapters 9 and 17, as configured in /etc/rsyslog.conf.

This is followed by

```
log_on_failure = HOST
```

which specifies the logging information when a login through an xinetd-controlled service fails. Naturally, this specifies the host name (or IP address) of the client host. It might help to add USERID to the list, which lists the UID number associated with the failed login. This can help you identify compromised accounts.

This line,

```
log_on_success = PID HOST DURATION EXIT
```

specifies the logging information associated with a successful connection. For example, once I logged off a Telnet connection from a remote system, and this led to the following entries in /var/log/messages:

```
Jan 31 08:46:55 server1 xinetd[16543]: START: telnet pid=16582
from=::ffff:tester1.example.com
```

```
Jan 31 08:47:01 server1 xinetd[16543]: EXIT: telnet status=0 pid=16582 duration=6 (sec)
```

The effect from /etc/xinetd.conf is straightforward. The next active line is

```
cps = 50 10
```

The cps command prevents attempts to "flood" any xinetd service; this line limits connections to 50 per second. If this limit is exceeded, xinetd waits 10 seconds before allowing a remote user to try again.

The next line,

```
instances = 50
```

limits the number of active services for a particular service; in this case, no more than 50 users can be logged into the local Telnet server simultaneously. That number goes down if other xinetd services are running.

This is followed by a related directive:

```
per_source = 10
```

which limits the number of connections from each IP address. The next active directive is almost self-explanatory:

```
v6only = no
```

If this were set to yes, access would be limited to systems with IPv6 addresses. A couple of environment directives follow, which allow execution with the xinetd group, or one defined with the group directive (singular), since there is no default xinetd group.
groups = yes
umask = 002
Finally, the last active line supports the use of the other configuration files specified in the /etc/xinetd.d directory:
includedir /etc/xinetd.d

## Service-Specific xinetd Configuration

Each file in the /etc/xinetd.d directory specifies a particular service for xinetd to manage. By default, scripts in this directory are disabled. The following code shows a sample of the /etc/xinetd.d/telnet configuration file, with this service disabled:

```
# default: on
# description: The telnet server serves telnet sessions; it uses
# unencrypted username/password pairs for authentication.
service telnet
{
flags          = REUSE
socket_type    = stream
wait           = no
user           = root
server         = /usr/sbin/in.telnetd
log_on_failure += USERID
disable        = yes
}
```

This is a typical /etc/xinetd.d configuration file. The variables (and a few additional variables that you can use) are described in Table 10-3. This is a versatile configuration file; other fields are described in the man pages for xinetd.conf. Do read the xinetd.conf man page; the only_from and no_access directives may be of particular interest, as they can help you "configure host-based and user-based security for the service." You can enable any xinetd service by changing disable = yes to disable = no.

## TABLE 10-3

### Standard Parameters for xinetd Configuration Files

| Field | Description of Field Entry |
|---|---|
| flags | Supports different parameters for the service; REUSE is a default that supports continuous use of the service. Options include IPv6 to set this as a service for those types of networks. |
| socket_type | Specifies the communication stream. |
| wait | Set to yes for single-threaded applications or no for multithreaded applications. |
| user | Account under which the server should run. |
| group | Group under which the server should run. |
| server | The server program. |
| only_from | Host name or IP address allowed to use the server. CIDR notation (such as 192.168.0.0/24) is okay. |
| no_access | Host name or IP address not allowed to use the server. CIDR notation is okay. |
| log_on_failure | If there's a failed login attempt, this specifies the information sent to a log file. |
| disable | By default, set to yes, which disables the service. |

> **exam watch**
> Always remember to make sure that a service will be active after a reboot. The `chkconfig servicename on` command is one way to do this for xinetd services. Otherwise, anything you configure may not work after a system is rebooted.

There are two ways to activate an xinetd service. You can edit the configuration file directly by changing the `disable` field from `yes` to `no`. Then make the xinetd daemon reread the configuration files with the `service xinetd reload` command.

Alternatively, you can use the `chkconfig servicename on` command, which automatically makes this change and makes xinetd reread the configuration file.

## EXERCISE 10-1

### Configure xinetd

In this exercise, you will enable the Telnet service using xinetd. This exercise assumes that the telnet-server package is already installed. Before starting this exercise, try to establish a Telnet session using the command `telnet localhost`. If you're successful, Telnet was previously enabled; in that case, disable it first with the `chkconfig telnet off` command.

- 1. Edit `/etc/xinetd.d/telnet` and change the value of `disable` from `yes` to `no`.
- 2. Tell xinetd to reread its configuration file using this command:
  ```
  # service xinetd reload
  ```
- 3. Try the `telnet localhost` command again. It should work.
- 4. Try to log in with an incorrect username or password.
- 5. Log in to another terminal. What do you see when you run `utmpdump /var/log/wtmp`?
- 6. Now log in with a correct username and password.
- 7. What do you see in `/var/log/messages`?
- 8. Log out of the Telnet session. What do you see now in `/var/log/messages`?
- 9. Use the `chkconfig` command to disable Telnet. (Remember that the name of the service is telnet.) Try connecting to the Telnet server again. Do you have to restart or reload xinetd?
- 10. What happens when you use `chkconfig` to disable Telnet? Does it change the `/etc/xinetd.d/telnet` configuration file?
- 11. For the security of this system, uninstall the associated package with the rpm -e telnet-server command. As suggested by the NSA, crackers can't exploit weaknesses in uninstalled software.

## CERTIFICATION OBJECTIVE 10.04

### TCP Wrappers

As suggested by its name, TCP Wrappers protects those services that communicate using the TCP protocol. It was originally designed to help protect services configured through the Extended Internet Super-Server just described. But TCP wrappers protection is no longer limited to such services; the protection can apply to all services statically and dynamically linked to the associated library wrapper file, libwrap.so.0. The way TCP wrappers protects a service is defined in the /etc/hosts.allow and /etc/hosts.deny configuration files.

### Is a Service Protected by TCP Wrappers?

The strings command can be used to identify those daemons protected by TCP Wrappers. It does so by listing the strings associated with various components of binary files. The string associated with TCP Wrappers is hosts_access. Daemons can be found in the /sbin and /usr/sbin directories. Thus, the quickest way to scan the daemons in these directories for the hosts_access string is with the following commands:

```
# strings /sbin/* | grep hosts_access
# strings /usr/sbin/* | grep hosts_access
```

The output depends on installed packages. One example is the SSH daemon, /usr/sbin/sshd. You can then use the full path to that daemon to confirm a link to the TCP Wrappers library, libwrap.so.0.

The library dependencies command, ldd, can list the libraries used by the sshd daemon. To identify those dependencies, run the following command:

```
# ldd /usr/sbin/sshd
```

But that's not convenient, as it returns the files for more than a couple of dozen library files. As an expert at the Linux command line, you should know how to pipe
