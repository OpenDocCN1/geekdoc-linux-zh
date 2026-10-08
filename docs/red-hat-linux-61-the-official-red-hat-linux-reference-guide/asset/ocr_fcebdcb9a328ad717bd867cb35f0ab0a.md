# Chapter 15. TCP Wrappers and xinetd

service telnet

```
{
  flags           = REUSE
  socket_type     = stream
  wait            = no
  user            = root
  server          = /usr/sbin/in.telnetd
  log_on_failure += USERID
  disable         = yes
}
```

These lines control various aspects of the telnet service:

+   * service — Defines the service name, usually to match a service listed in the /etc/services file.
* flags — Sets any number of attributes for the connection. REUSE instructs xinetd to reuse the socket for a Telnet connection.
* socket_type — Sets the network socket for stream.
* wait — Defines whether the service is single-threaded(yes) or multi-threaded(no).
* user — Defines what user ID process will run under.
* server — Defines the binary executable to be launched.
* log_on_failure — Defines logging parameters for log_on_failure in addition to those already-defined in xinetd.conf.
* disable — Defines whether the service is active.

# 15.4.3. xinetd Configuration Files

There are a large assortment of directives available for xinetd protected services. This section highlights-some of the more commonly used options.

# 15.4.3.1. Logging Options

The following options are available for both /etc/xinetd.conf and the service-specific configuration files in the /etc/xinetd.conf/directory.
Below is a list of the more commonly used logging options:

+   * ATTEMPT — Logs the fact that a attempt was made (log_on_failure).
* DURATION — Logs the length of time the service is used by a remote system (log_on_success).
* EXIT — Logs the status or termination signal of the service (log_on_success).
* HOST — Logs the remote host's IP address (log_on_failure and log_on_success).
* PID — Logs the process ID of the server receiving the request (log_on_success).
* RECORD — Records information about the remote system in case the service cannot be started. Only particular services, such as login and finger, may use this option (log_on_failure).
* USERID — Logs the remote user using the method defined in RFC 1413 for all multi-threaded stream services (log_on_failure and log_on_success).

For a complete list of logging options, consult the xinetd.conf man page.