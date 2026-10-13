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

# TABLE 10-3

# Standard Parameters for xinetd Configuration Files

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