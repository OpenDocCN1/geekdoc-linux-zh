This tells services that they should consult standard Unix/Linux files for passwd, shadow, and group (`/etc/passwd`, `/etc/shadow`, `/etc/group`, respectively) lookups. For host lookups, the system checks `/etc/hosts` and if there is no entry, it checks DNS. The commented `hosts` entry lists the possible values for hosts. Edit this file only if your naming service has changed.

# Setting a Name Server with `/etc/resolv.conf`

`/etc/resolv.conf` is used by DNS, the domain name service. (DNS is covered in detail in Chapter 27.) The following is an example of `resolv.conf`:

```
```text
nameserver 192.172.3.8
nameserver 192.172.3.9
search mycorp.com
```
```

This sets the nameservers and the order of domains for DNS to use. The contents of this file will be set automatically if you use Dynamic Host Configuration Protocol, or DHCP (see the section on “DHCP” later in this chapter).

# Setting DNS Search Order with `/etc/host.conf`

The `/etc/host.conf` file lists the order in which your machine will search for hostname resolution. The following is the default `/etc/host.conf` file:

```
```text
order hosts, bind
```
```

In this example, the host checks the `/etc/hosts` file first and then performs a DNS lookup. A couple more options control how the name service is used. The only reason to modify this file is if you use NIS for your name service or you want one of the optional services. The `nosport` option can be a good option for system security. It compares a standard DNS lookup to a reverse lookup (host-to-IP then IP-to-host) and fails if the two don’t match. The drawback is that often when proxy services are used, the lookup fails, so you want to use this with caution.

# Examining Host Network Settings in `/etc/sysconfig/network`

Changes to `/etc/sysconfig/network` will not take effect until you restart the networking daemons or reboot the system. If you use Fedora’s graphical configuration network tools (described in the next section), you should not edit this file. The file might look like this:

```
```text
NETWORKING=yes
HOSTNAME=myhost
GATEWAY=192.112.50.99
```
```

A `GATEWAYDEV` setting is also available to associate a specific network device (such as `eth0` or `eth1` and so on). An additional optional entry to `/etc/sysconfig/network` is for NIS domain machines and would look like this:

```
```text
NISDOMAIN=rebel
```
```