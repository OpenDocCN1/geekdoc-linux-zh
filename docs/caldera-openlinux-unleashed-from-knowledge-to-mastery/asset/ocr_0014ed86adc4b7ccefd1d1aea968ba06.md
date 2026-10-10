Traditionally, ypbind finds an NIS server by broadcasting a request on the local network and listening for responses. This is not secure, however: Anyone who has physical access to your network can plug in a Linux laptop and supply an NIS server with fake password entries.

Because broadcasts are insecure, it is usual to specify the NIS server. This is done in the file `/etc/nis.conf`. If your NIS domain is `yp_foo` and your NIS server's IP address is `192.168.2.3`, put a line like this in `/etc/nis.conf`:

```
domain yp_foo server 192.168.2.3
```

To start ypbind, run this command:

```
# sh /etc/rc.d/init.d/nis-client start
```

This command parses `/etc/nis.conf`, sets the NIS domain name with the `domainname` command, and starts ypbind.

The `domainname` command displays the NIS domain name. Invoke it like this:

```
$ domainname
yp_foo
```

If you run with root privileges, you can set the domain name as follows:

```
# domainname my_domain.name
```

The ypbind command creates a file called `/var/nis/binding/domain.version`. For example, the file might be called `/var/nis/binding/yp_foo.2`. The Linux C library looks for this file to determine how to connect to the NIS server.

ypbind has many options; they are documented in `ypbind(8)`.

# # Name Service Switch

The standard Linux runtime library has functions for accessing various pieces of system information. For example, the `getpwnam` and `getpwuid` functions obtain password information keyed from the login name or numerical user ID, respectively. In traditional UNIX systems, these functions simply read the `/etc/passwd` file to obtain the required information.

Modern Linux systems are NIS-aware, meaning that these functions may retrieve information from an NIS server rather than (or in addition to) reading configuration files in `/etc`. To determine how the library functions retrieve information, the system consults the file `/etc/nsswitch.conf`. Each line in `/etc/nsswitch.conf` looks like this:

```
database: services
```