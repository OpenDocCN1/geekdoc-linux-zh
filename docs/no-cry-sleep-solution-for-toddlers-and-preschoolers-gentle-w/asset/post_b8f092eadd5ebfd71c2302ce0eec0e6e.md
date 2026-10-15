
To enable management by chkconfig, a commented default and description entry needs to be placed before each service segment. Where separate files are used, the entry is placed at the head of each file. Red Hat already provides these for the services it installs with its distribution, such as POP3 and SWAT. A default entry can be either on or off. For example, the chkconfig default and description entries for the FTP service are shown here:

```
# default: off
# description: The POP3 service allows users\
#           to access their mail using a POP3 client \
#           such as Netscape Communicator, or fetchmail.
```

Red Hat indicates whether a service is set on or off by default. If you want to turn on a service that is off by default, you have to set its disable attribute to no and restart xinetd. The Red Hat entry for the POP3 mail server, ipop3d, is shown here. An initial comment tells you that it is off by default, but then the disable attribute turns it on:

```
# default: off
# description: The POP3 service allows users\
#           to access their mail using a POP3 client \
#           such as Netscape Communicator, or fetchmail.

service pop3
{
    socket_type    = stream
    wait           = no
    user           = root
    server         = /usr/sbin/ipop3d
    log_on_success += HOST DURATION
    log_on_failure += HOST
    disable        = no
}
```

## Logging xinetd Services

You can further add a variety of other attributes such as logging information about connections and server priority (nice). In the following example, the log_on_success attribute logs the duration (DURATION) and the user ID (USERID) for connections to a service, log_on_failure logs the users that failed to connect, and nice sets the priority of the service to 10.

```
log_on_success += DURATION USERID
log_on_failure += USERID
nice = 10
```

The default attributes defined in the defaults block often set global attributes such as default logging activity and security restrictions. log_type specifies where logging information is to be sent, such as to a specific file (FILE) or to the system logger (SYSLOG). log_on_success specifies information to be logged when connections are made, and log_on_failure specifies information to be logged when they fail.

```
log_type = SYSLOG authpriv
log_on_success = HOST PID
log_on_failure = HOST RECORD
```

## xinetd Network Security

For security restrictions, you can use only_from to restrict access by certain remote hosts. no_access denies access from the listed hosts, but no others. These controls take IP addresses as their values IP addresses. You can list individual IP addresses, a range of IP addresses, or a network, using the network address. The instances attribute limits the number of server processes that can be active at once for a particular service. The following examples restrict access to a local network 192.168.1.0 and the localhost, deny access from 192.168.1.15, and use the instances attribute to limit the number of server processes at one time to 60.

```
only_from = 192.168.1.0
only_from = localhost
no_access = 192.168.1.15
instances = 60
```

## xinetd Defaults and Internal Services

A sample default block is shown here:

```
defaults
{
    instances = 60
    log_type = FILE /var/log/servicelog
    log_on_success = HOST PID
    log_on_failure = HOST RECORD
    only_from = 192.168.1.0
    only_from = localhost
    no_access = 192.168.1.15
}
```

The xinetd program also provides several internal services, including time, services, servers, and xadmin. services provides a list of currently active services, and servers provides information about servers. xadmin provides xinetd administrative support.

## Service Files in xinetd.d Directory

Instead of having one large xinetd.conf file, you can split it into several configuration files, one for each service. You do this by creating an xinetd.conf file with an includedir attribute that specifies a directory to hold the different service configuration files. In the following example, the xinetd.d directory holds xinetd configuration files for services like swat. Red Hat uses just such an implementation. This approach has the advantage of letting you add services by just creating a new configuration file for them. Modifying a service involves editing only its configuration file, not an entire xinetd.conf file.

```
includedir /etc/xinetd.d
```

The following example shows the xinetd.conf file used for Red Hat Linux:

```
# Simple configuration file for xinetd
# Some defaults, and include /etc/xinetd.d/
```
