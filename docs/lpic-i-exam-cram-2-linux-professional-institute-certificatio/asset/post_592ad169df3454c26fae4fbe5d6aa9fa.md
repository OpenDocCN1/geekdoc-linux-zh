
## inetd Configuration Files

inetd is much older than xinetd, and the main difference between the two is the structure of the configuration files.

inetd uses a single configuration file, typically the `/etc/inetd.conf` file. This file contains comments that begin with `#` and entries that each define a single service. An example of a couple (many more exist) of typical lines from `/etc/inetd.conf` is shown here:

```text
ftp    stream  tcp  nowait  root  /usr/sbin/in.ftpd  in.ftpd
telnet stream  tcp  nowait  root  /usr/sbin/in.telnetd  in.telnetd
```

The lines shown here are broken up into the following fields and definitions:

- **Service name**—This name must match a valid service name entry in the `/etc/services` file.
- **Socket type**—This can be any of `stream`, `dgram`, `raw`, `rdm`, or `seqpacket`.
- **Protocol**—This is one of the protocols defined in the `/etc/protocols` file; typically it’s either `tcp` or `udp`.
- **wait** or **nowait** parameter—Use the `wait` parameter for single-threaded servers that grab the socket and operate until timeout; use `nowait` for multithreaded servers that free up the socket when not active.
- **User/group**—The user or group this service should run as, giving you the ability to restrict a risky service to an account that’s not root.
- **Server program**—The full path and name to the program that will provide the service.
- **Server argument(s)**—Any parameters the service might need to run properly.

If the service is to be controlled by `hosts.deny` and `hosts.allow` or TCP wrappers, the server program should be `/usr/sbin/tcpd` and the server argument should then be the full path and name of the service tcpd will be watching over. This is true only for inetd—not xinetd. You can learn more about this in Chapter 19, “Security.”

> **ALERT**
> If you have been running **inetd** and are converting to run **xinetd**, the most important file is `/etc/inetd.conf`, which contains entries that define which services should be provided on demand. These lines should form the basis of the new **xinetd** configuration. Red Hat includes a utility named **inetdconvert** that can help with this process.

### xinetd Configuration Files

The **xinetd** daemon initially uses the `/etc/xinetd.conf` file to set a few daemon configuration settings and the defaults that will be picked up by all **xinetd**-governed services, and to specify the include directory. (These defaults are overridden by any settings in the individual service configuration files.)

The include directory is typically `/etc/xinetd.d`, which contains a single text file for each governed service. The service configuration files contain the definition of a service and any special settings that need to be set for correct functioning.

Figure 18.1 shows the relationships between the components of the **xinetd** services and files.

![](img/49f4f38f3aec011238fa50f89e643db3_486_0.png)

**Figure 18.1** How **xinetd** works.

As you can see, **xinetd** reads `/etc/xinetd.conf` and gets its configuration, including the include directory location; then it waits for a client request for one of its services. When a client request arrives, xinetd looks at the packets and finds the target port/service and looks that service up by name in the `/etc/xinetd.d` directory. This directory contains one file per service, named exactly as the service name appears in `/etc/services`.

The `/etc/xinetd.conf` file is simple by nature:

```bash
# Simple configuration file for xinetd
# Some defaults, and include /etc/xinetd.d/
defaults
{
    instances                  = 60
    log_type                   = SYSLOG authpriv
    log_on_success             = HOST PID
    log_on_failure             = HOST
    cps                        = 25 30
}
include /etc/xinetd.d
```

The file contains a few lines that set the default limitations for the services governed by xinetd. If an individual service has a conflicting setting in its configuration file, that individual file setting takes precedence.

> **ALERT**
> You're likely to see questions about how to have a service run as a different user, which is accomplished by editing the service's configuration file and changing the user line.

Several of these lines bear defining:

- **instances**—This sets the total number of daemon instances allowed; this daemon is limited to 60 instances.
- **cps**—This limits the number of connections per second allowed through xinetd. Any more than the maximum (25) causes the service to be disabled for 30 seconds and then check whether it can accept more connections.
- The other settings are log related, logging the host and PID for successful connections and just the host for unsuccessful connections.

An individual service configuration file from the `/etc/xinetd.d` directory such as `telnet` would contain:

```text
 service telnet
 {
     disable     = yes
     flags       = REUSE
     socket_type = stream
     wait        = no
     user        = root
     server      = /usr/sbin/in.telnetd
     log_on_failure += USERID
     access_times   = 08:00-17:00
     only_from      = snowlower
 }
```

These files contain a number of settings:

- **service**—This keyword must be followed by the service name, such as `telnet`.
- **disable**—Values include *yes* (which disables the service and no connections are accepted) and *no* (which doesn't disable or enables the service for connections).
- **flags**—Many and varied flags exist; the most common is *REUSE*, which allows the port and service to accept multiple connections.
- **socket_type**—This can be `stream`, `dgram`, `raw`, `rdm`, or `seqpacket`.
- **wait**—Use the `wait` parameter for single-threaded servers that grab the socket and operate until timeout; use `nowait` for multithreaded servers that free up the socket when not active.
- **user**—The user or group this service should run as, giving you the ability to restrict a risky service to an account that’s not `root`.
- **server**—This is the full path and filename of the server or daemon program that is run when a client requests a connection.
- **log_on_failure**—This can also be `log_on_success`, and values include `HOST`, `USERID`, and `PORT`, to name a few options.
- **access_times**—This setting lets you set access timeframes for the service, such as from 8 a.m. to 5 p.m. in the previous file.
- **only_from**—This can be a list of hostnames, IPs, globs of addresses, and defined networks by name from the `/etc/networks` file.

To enable a service governed by `xinetd`, such as the previous `telnet` service, you would use the following command:

```bash
chkconfig telnet on
```

This changes the previous file to contain the following line:

```text
disable = no
```

The service is now enabled and can accept requested connections. Changes to the file for a service don’t require any restarting of services or `xinetd`; those changes take place for the next and subsequent instances of the service whose file you changed.

![](img/49f4f38f3aec011238fa50f89e643db3_488_0.png)

> If you edit the `/etc/xinetd.d/telnet` file by hand, the `xinetd` service might have to be restarted for the change to take effect. This is done automatically by the `chkconfig` command.

To disable the service completely from being initiated and governed by `xinetd`, you would use this command:

```bash
chkconfig telnet off
```

This disables the service and `xinetd` ignores requests for this service from this point on.

inetd must be restarted after a new configuration is written to the `/etc/inetd.conf` file, but xinetd reads the service configuration files in `/etc/xinetd.d` dynamically and requires restarting only if you change the `/etc/xinetd.conf` file.

## Using TCP Wrappers for Securing Services

If you want to protect your on-demand services, use TCP wrappers as one of the layers of protection for seldom-used services.

The common concept of using TCP wrappers is that only services in the `/etc/inetd.conf` file can be wrapped or protected; that's untrue. The TCP wrappers package includes a library called `libwrap.a` that an increasing number of Linux services reference for security. Although it used to be true that a service must be included in `/etc/inetd.conf` so that `tcpd` could govern it, many can directly use the `libwrap.a` library and the allow/deny files for protection.

### inetd and TCP Wrappers

When used with inetd, the concept of using TCP wrappers is to place a controlling daemon with instructions as to who's allowed and denied in front of each service that runs on your machine. Most services in the era of wide-spread inetd usage didn't have any built-in protection, so they were configured to be run as parameters of the `tcpd` daemon.

`tcpd` is set up to refer to the `/etc/hosts.allow` and `/etc/hosts.deny` files for the hosts that are allowed and denied access to services protected by `tcpd`.

### xinetd and TCP Wrappers

If you are using xinetd or running a current distribution of Linux, many of the services are developed to use the `libwrap.a` library, finally divorcing TCP wrappers from the `inetd.conf` file.

In the case of current distributions and xinetd, any service capable of referencing `libwrap.a` has the potential to benefit from the protection that the `hosts.allow` and `hosts.deny` files provide.

Additionally, if you wanted to run a set of services that were both secure and fast, you'd use TCP wrappers and a standalone daemon, instead of putting
