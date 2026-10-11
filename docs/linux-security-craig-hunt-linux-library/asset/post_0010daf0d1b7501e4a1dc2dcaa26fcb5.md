
this service. In addition, it is very difficult to enforce access control on RPC-based services, especially since their associated ports change each time the system is rebooted. This makes the portmap daemon a security liability.

If you are using a Linux distribution that’s over two years old, I recommend that you disable it as soon as you build your system and leave it disabled until you come up with an alternative.

> **TIP** If your Linux distribution is more than three years old, I also recommend that you upgrade your Linux system altogether. Just make sure that you test the upgrade on a practice server and not on a development server; otherwise you could run into a lot of trouble.

In most Linux distributions, portmap is started or stopped from one or more of the following files:

- /etc/rc.d/rc2.d/S11portmap
- /etc/rc.d/rc3.d/S11portmap
- /etc/rc.d/rc4.d/S11portmap
- /etc/rc.d/rc5.d/S11portmap

Since 1996, Linux distributions have included a secure version of the portmap service that can enforce access-control rules on the same files as TCP Wrappers (`/etc/hosts.allow` and `/etc/hosts.deny`). To find out if you’re running this version of portmap, insert the following line into the /etc/hosts.deny file:

```
portmap: ALL
```

In addition, insert the following line into the /etc/hosts.allow file:

```
portmap: <a trusted hostname>
```

Then, proceed to mount an NFS share from the trusted host and from a different host. If you can mount the share from the trusted host but not from the different host, you’re running a version of portmap that enforces access control. You can go ahead and enable it by putting the startup script back in /etc/rc.d/rc*.d/S11portmap.

Note, however, that securing the portmap service is only one step toward enhancing the security of your system. If you must use RPC services, make sure that each of them (NLS, NFS, etc.) is secure and up to date, because an intruder can always simply brute-force guess which port the service is running on.

## Running Network Services as chroot

Linux allows you to run a command with a modified root directory such that directory references are relative to the path specified in the chroot command. This allows you, for example, to run several instances of an HTTP server, each with its own set of configurations and executables. The idea is an attractive one: allow the process to believe that it has free reign of the server while confining it to a small “sandbox.” However, the chroot protection can be easily circumvented, especially when the application runs with root privileges.

Limit chroot execution of network services to instances when the daemon runs under a nonprivileged user, and ideally, to when the daemon operates in read-only mode. chroot is especially useful for non-interactive Web servers whose content stays static over time.

# TCP Wrappers

Developed by Wietse Venema during his tenure at The Netherlands’ Eindhoven University, the TCP Wrappers package has quickly become a standard tool included in all of today’s Linux distributions. Furthermore, this is arguably the most useful network security tool to come along since the dawn of the operating system.

By interposing itself between the inetd daemon and the server application itself, TCP Wrappers adds a layer of access control to an otherwise wide-open inetd facility. The real beauty of this tool, and the main reason for its popularity, is its simple design. There is no need to recompile (or even modify) either the inetd daemon or the server applications themselves. Instead, you simply modify your /etc/inetd.conf file to include the TCP Wrappers application instead of the real server name. The TCP Wrappers application receives and examines every connection request and decides to grant it or deny it based on a set of criteria specified by the network administrator.

The next two sections describe the TCP Wrappers installation and configuration.

## Installing TCP Wrappers

The success of TCP Wrappers has resulted in its widespread use on the majority of production Linux servers today. In fact, most distributions even come outfitted with a default configuration for TCP Wrappers. If you need to install TCP Wrappers on an older Linux installation, or you would like to upgrade your existing installation, simply find the .rpm distribution of the tool in your favorite archive. Listing 4.7 shows you how to install TCP Wrappers using the RPM facility.

**Listing 4.7** Installing TCP Wrappers via RPM (Upgrade option)

```
[ramon]$ rpm -q tcp_wrappers
tcp_wrappers-7.6-7
[ramon]$ sudo rpm -U tcp_wrappers-7.6.10.i386.rpm
[ramon]$ rpm -q tcp_wrappers
tcp_wrappers-7.6-10
```

Listing 4.7 shows a system that was running version `7.6.7` and has been upgraded to the more recent version `7.6.10`.

> **WARNING** Trojan horse versions of TCP Wrappers were placed on a number of public FTP servers around January 21, 1999. The offending file was labeled as version `7.6`, and it introduced a root vulnerability on the systems where it was installed. I strongly discourage you from downloading this file (the tar archive was named `tcp_wrappers_7.6.tar.gz`). Obtain it in RPM format from a well-known and trusted repository instead. Refer to CERT Advisory `CA-1999-01` for more detailed information.

Once you have verified your TCP Wrappers installation, it’s time to look at the configuration files that you need to edit. This is the topic of the next section.

## Configuring TCP Wrappers

The first step in configuring the TCP Wrappers package is to make sure it is being properly invoked. This is done by ensuring that the **service** name field in `/etc/inetd.conf` is set to the location of the `tcpd` binary (`/usr/sbin/tcpd` in Listing 4.2). This allows the TCP Wrappers daemon to intercept all incoming requests and to examine them before passing them on to the real server application. The name of this application is specified in the **server program arguments** field of `/etc/inetd.conf`.

The real power of the TCP Wrappers tool is the fine-grain level of access control that it provides. The system administrator can define a set of allowable clients for each network service. To do this, you must edit two configuration files that are typically found in the `/etc` directory: `/etc/hosts.allow` and `/etc/hosts.deny`. These files are already included in most Linux distributions, but make sure that they exist and edit them to reflect your site’s security policy.

These two files are consulted by the TCP Wrappers application in that order (first `hosts.allow`, then `hosts.deny`) and can contain rules specifying access-control directives. The connection request is granted unless there is a specific `deny` directive found in one of these files. I recommend that your `/etc/hosts.deny` file have a catchall rule at the end that denies all requests. This forces you to have to enter specific `allow` directives for those services that should be permitted.

The basic syntax for the rules in the `/etc/hosts.allow` and `/etc/hosts.deny` files is as follows:

`daemon_list : client_list [ : shell_command ]`

These fields have the following meanings:

- `daemon_list` is a comma-separated list of server names.
- `client_list` is a comma-separated list of patterns matching one or more clients.
- `shell_command` is the action to execute when the rule has found a match.

Table 4.2 describes the types of expressions that can make up one of these rules.

**Table 4.2**
**TCP Wrappers Configuration: Access Control List Patterns**

| Pattern | Meaning |
| :--- | :--- |
| `.example.com` | Any host name that ends with `.example.com`. |
| `134.33.` | Any host address whose first two octets are `134.33`. |
| `10.0.0.0/255.0.0.0` | The class-A network `10.0.0.0`. |
| `ALL` | A true wildcard (i.e., any host). |
| `LOCAL` | Host name that contains no period (.). |
| `KNOWN` | Both host name and address are resolved (via DNS). |
| `UNKNOWN` | Both host name and address are not resolved (via DNS). |
| `PARANOID` | Host name does not match the address (via DNS). |

In addition, shell commands can make use of a number of supplied variables whose instance gets replaced on the fly according to the current context. Table 4.3 summarizes the most significant of these variables.

**Table 4.3**
**TCP Wrappers Configuration: Shell Command Expansion**

| Pattern | Meaning |
| :--- | :--- |
| `%a` | Client host address |
| `%A` | Server host address |
| `%h` | Client host name |
