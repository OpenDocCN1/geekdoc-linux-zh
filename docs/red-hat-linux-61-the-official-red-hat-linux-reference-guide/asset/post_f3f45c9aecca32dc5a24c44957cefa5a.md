
## Chapter 15. TCP Wrappers and xinetd

service telnet

```xinetd
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

- service — Defines the service name, usually to match a service listed in the /etc/services file.
- flags — Sets any number of attributes for the connection. REUSE instructs xinetd to reuse the socket for a Telnet connection.
- socket_type — Sets the network socket for stream.
- wait — Defines whether the service is single-threaded(yes) or multi-threaded(no).
- user — Defines what user ID process will run under.
- server — Defines the binary executable to be launched.
- log_on_failure — Defines logging parameters for log_on_failure in addition to those already-defined in xinetd.conf.
- disable — Defines whether the service is active.

### 15.4.3. xinetd Configuration Files

There are a large assortment of directives available for xinetd protected services. This section highlights some of the more commonly used options.

### 15.4.3.1. Logging Options

The following options are available for both /etc/xinetd.conf and the service-specific configuration files in the /etc/xinetd.conf/directory.
Below is a list of the more commonly used logging options:

- ATTEMPT — Logs the fact that an attempt was made (log_on_failure).
- DURATION — Logs the length of time the service is used by a remote system (log_on_success).
- EXIT — Logs the status or termination signal of the service (log_on_success).
- HOST — Logs the remote host's IP address (log_on_failure and log_on_success).
- PID — Logs the process ID of the server receiving the request (log_on_success).
- RECORD — Records information about the remote system in case the service cannot be started. Only particular services, such as login and finger, may use this option (log_on_failure).
- USERID — Logs the remote user using the method defined in RFC 1413 for all multi-threaded stream services (log_on_failure and log_on_success).

For a complete list of logging options, consult the xinetd.conf man page.

### 15.4.3.2. Access Control Options

Users of xinetd services can choose to use the TCP wrappers hosts access rules, provide access control via the xinetd configuration files, or a mixture of both. Information concerning the use of TCP wrappers access control files can be found in Section 15.2 Wrappers Configuration Files. This section discusses using xinetd to control access services.

Note
Unlike TCP wrappers, changes to access control only take effect if the xinetd administrator restarts the xinetd service.

The xinetd hosts access control from the method used by TCP wrappers. While TCP wrappers places all of the access configuration within two files, /etc/hosts.allow and /etc/hosts.deny, each service's file in /etc/xinetd.d can contain its own access control rules.

The following access options are supported by xinetd:

- only_from — Allows only the hosts to use the service.
- no_access — Blocks listed hosts from using the service.
- access_times — Specifies the time when a particular service may be used. The time range must be stated in 24-hour format notation, HH:MM-HH:MM.

The only_from and no_access options can use a list of IP addresses or hostnames, or can specify any network. TCP wrappers, combining xinetd access control with the enhanced logging configuration can enhance security by blocking requests from hosts while verbose recording each connection.

For example, the following /etc/xinetd.d/telnet file can be used to block Telnet from a particular network group and restrict the overall time that allowed users can log in:

```xinetd
service telnet {
    disable         = no
    flags           = REUSE
    socket_type     = stream
    wait            = no
    user            = root
    server          = /usr/sbin/in.telnet
    log_on_failure = 10.0.0.1/24
    no_access       =
    log_on_success += PID HOST EXIT
    access_times    = 09:45-16:15
}
```

In this example, when client is from the 10.0.0.1/24 network, such as 10.0.1.2, tries to access the Telnet service, it will receive a message stating the following message:

Connection closed by foreign host.

In addition, their login attempt is logged in /var/log/secure as follows:

```log
May 15 17:38:49 boo xinetd[16252]: START: telnet pid=16256 from=10.0.1.2
May 15 17:38:49 boo xinetd[16252]: FAIL: telnet address from=10.0.1.2
May 15 17:38:49 boo xinetd[16252]: EXIT: telnet status=0 pid=16256
```

When using TCP wrappers in conjunction with xinetd, it is important to understand the relationship between the two access mechanisms. The following is the order of operations followed by xinetd when client requests a connection:

1. The xinetd daemon accesses TCP wrappers access rules through libwrap. If a deny rule matches the client host, the connection is dropped. If an allow rule matches the client host, the connection is passed to xinetd.
2. The xinetd daemon checks its own access control rules for the xinetd service. If a deny rule matches the client host, the connection is dropped. Otherwise, xinetd starts an instance of the requested service and passes control of the connection to it.

Important
Care should be taken when using TCP wrappers in conjunction with access controls. Misconfiguration can cause undesired effects.

### 15.4.3.3. Binding and Redirection

The service configuration files for xinetd support binding the service to an IP address and redirecting incoming requests to another IP address, hostname, or port.

Binding is controlled with the bind option in the service-specific files and links the service to one IP address on the system. Once configured, the bind option only allows requests for the proper IP address to access the service. This way services can be bound to different interfaces based on name.

This is particularly useful for systems with multiple networks or with multiple IP addresses. On such a system, insecure services like Telnet can be configured to listen only on the interface connected to a private network and not the interface connected with the Internet.

The redirect option accepts an IP address or hostname followed by a port number. It configures the service to redirect all requests for this service to the specified host and port number. This feature can be used to point to another port number on the same system, redirect the request to a different IP address on the same machine, or any combination of these options. xinetd is able to accomplish this redirection by spawning a process that stays alive for the duration of the connection between the client machine and the host. The advantages of bind and redirect options are most clearly seen when binding to a particular IP address on a system and redirecting requests for this service to a second machine that only the first machine can use. Alternatively, these options can be used to limit the exposure of a particular service on a multi-homed machine to a known IP address, as well as redirect requests for that service to another machine specifically configured for that purpose.

For example, a system that is used as a firewall with its Telnet service:

```xinetd
service telnet
{
    socket_type = stream
    wait        = no
    server      = /usr/sbin/in.xinetd
log_on_success    += DURATION USERID
log_on_failure    += USERID
bind               = 123.123.123.123
redirect           = 10.0.1.1 21 23
}
```

The bind and redirect options in this file ensure that the Telnet service on the machine is bound to the external IP address (123.123.123.123), the one facing the Internet. In addition, requests for Telnet service to 123.123.123.123 are redirected via a second network adapter to an internal IP address (10.0.1.0) that facilitates the communication between the two systems. The connecting system is connected to 123.123.123.123 when it is actually connected to a different machine.

This feature is particularly useful for users with broadband connections and only one fixed IP address. When using Network Address Translation (NAT), services behind the gateway using internal IP addresses are not available from outside the gateway. However, when services controlled by xinetd are configured with the bind and redirect options, the gateway can act as a type of proxy between outside services and a particular internal machine. In addition, the various xinetd access control and logging options are also available for additional protection, by limiting the number of simultaneous connections to the redirected service.

### 15.4.3.4. Resource Management Options

The xinetd daemon can add a basic level of protection from Denial of Service (DoS) attacks. Below is a list of directives which can aid in limiting the effectiveness of such attacks:

- max_source Defines the maximum number of instances for a service per IP address. It accepts only integers as an argument and can be used in both xinetd.conf and in the service-specific configuration files in the xinetd.directory.
- cps Defines the maximum number of connections per second. This directive takes two integer arguments separated by white space. The second is the maximum number of seconds xinetd must wait before re-enabling the service. It accepts only integers as an argument and can be used in both xinetd.conf and in the service-specific configuration files in the xinetd.directory.
- max_load Defines the CPU usage for a service. It accepts a floating point argument.

There are more resource management options available for xinetd. See the chapter titled Server Security in the Red Hat Linux Security Guide for more information. Also consult the xinetd.conf man page.

## 15.5. Additional Resources

Additional information concerning TCP wrappers and xinetd is available from system documentation and on the Web.

### 15.5.1. Installed Documentation

The bundled documentation on your system is a good place to start looking for additional TCP Wrappers, xinetd, and access control configuration options.
