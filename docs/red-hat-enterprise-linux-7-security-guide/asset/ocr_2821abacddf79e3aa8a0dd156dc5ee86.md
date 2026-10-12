```
source-ports:
icmp-blocks:
rich rules:
```

# NOTE

To specify the zone for which to display the settings, add the `--zone=zone-name` argument to the `firewall-cmd --list-all` command, for example:

```
[~]# firewall-cmd --list-all --zone=home
home
  target: default
  icmp-block-inversion: no
  interfaces:
  sources:
  services: ssh mdns samba-client dhcpv6-client
... [output truncated]
```

To see the settings for particular information, such as services or ports, use a specific option. See the `firewalld` manual pages or get a list of the options using the command help:

```
[~]# firewall-cmd --help

Usage: firewall-cmd [OPTIONS...]

General Options
 -h, --help                Prints a short help text and exists
 -V, --version             Print the version string of firewalld
 -q, --quiet               Do not print status messages

Status Options
 --state                   Return and print firewalld state
 --reload                  Reload firewall and keep state information
... [output truncated]
```

For example, to see which services are allowed in the current zone:

```
[~]# firewall-cmd --list-services
ssh dhcpv6-client
```

Listing the settings for a certain subpart using the CLI tool can sometimes be difficult to interpret. For example, you show the SSH service and `firewalld` opens the necessary port (22) for the service. Later, if you list the allowed services, the list shows the SSH service, but if you list open ports, it does not show any. Therefore, it is recommended to use the `--list-all` option to make sure you receive a complete information.

# 5.4. STARTING FIREWALLD

To start `firewalld`, enter the following command as `root`:

```
[~]# systemctl unmask firewalld
[~]# systemctl start firewalld
```