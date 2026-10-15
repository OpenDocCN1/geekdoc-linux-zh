
To create a base jail:

```
# iocage create -b
```

To create a lightweight jail and set its IP address and tag name to myjail:

```
# iocage create -c tag=myjail ip4_addr="em0|10.1.1.10/24"
```

Listing jails: To list all jails:

```
# iocage list
```

To see all downloaded releases:

```
# iocage list -r
```

To see available templates:

```
# iocage list -t
```

Starting, stopping, or restarting a jail: To start or stop any jail on the system, both UUID and TAG can be used interchangeably. To simplify UUID handling, iocage also accepts a partial UUID with any subcommand.

To start a jail tagged myjail:

```
# iocage start myjail
```

To start a jail with a full UUID run:

```
# iocage start 26e8e027-f00c-11e4-8f7f-3c970e80eb61
```

Or, to start the jail only with a partial UUID, enter the first few characters only:

```
# iocage start 26e8
```

To stop a jail, just use the stop subcommand instead of start:

```
# iocage stop myjail
```

To restart a jail run, which must already be running:

```
# iocage restart myjail
```

Note: Short UUIDs are supported with all operations and subcommands within iocage.

Configure a jail: Any property can be reconfigured with the set subcommand.
To set the jail's tag property:

```
# iocage set tag=myjail 26e8e027
```

Get a jail property: To verify any property, use the get subcommand:

```
# iocage get tag 26e8e027
```

Get all properties, or display all supported properties:

```
# iocage get all 26e8e027
```

System-wide defaults: Starting with Version 1.6.0 of iocage, system-wide defaults can be set. These defaults will be reapplied for all newly created jails. To create a system-wide default override for a property, simply specify the default keyword instead of a jail UUID or tag.

To turn off VNET capability for all newly created jails:

```
# iocage set vnet=off default
```

Destroy a jail:

```
# iocage destroy myjail
```

The jail must be down or stopped before it can be destroyed.
Warning: This will irreversibly destroy the jail!

## 25.2.3 iocage Networking

Jails have multiple networking options based on what features are desired.

### 25.2.3.1 For IP Alias-Based Networking (Shared IP)

iocage will try to guess whether VNET support is available in the system, and if it is, will enable it by default for newly created jails.

Make sure VNET is disabled:

```
# iocage get vnet UUID | TAG
```

If set to "on", disable it:

```
# iocage set vnet=off UUID | TAG
```

A system-wide default can be configured if required. This will take effect for newly created jails only.

```
# iocage set vnet=off default
```

Configure an IP address:

```
# iocage set ip4_addr="em0|10.1.1.10/24" UUID | TAG
```

If multiple addresses are desired, just separate the configuration directives with a comma:

```
# iocage set ip4_addr="em0|10.1.1.10/24,em0|10.1.1.11/24" UUID | TAG
```

Start jail:

```
# iocage start UUID | TAG
```

Verify visible IP configuration in the jail (the jail must be running for this to work):

```
# iocage exec UUID | TAG ifconfig
```

### 25.2.3.2 For VNET Networking

Add bridge configuration to /etc/rc.conf (on the host):

```
cloned_interfaces="bridge0 bridge1"
ifconfig_bridge0="addm em0 up"
ifconfig_em0="up"
```

Add these tunables to /etc/sysctl.conf:

```
net.inet.ip.forwarding=1
net.link.bridge.pfil_onlyip=0
net.link.bridge.pfil_bridge=0
net.link.bridge.pfil_member=0
```

Configure default gateway for jail:

```
# iocage set defaultrouter=10.1.1.254 UUID | TAG
```

Configure an IP address:

```
# iocage set ip4_addr="vnet0|10.1.1.10/24" UUID | TAG
```

Start jail and ping default gateway.
Start the jail:

```
# iocage start UUID | TAG
```

Open a console into the jail:

```
# iocage console UUID | TAG
```

Ping default gateway:

```
# ping 10.1.1.254
```

### 25.2.3.3 Configuring Network Interfaces

iocage handles network configuration for both shared IP and VNET jails transparently.

Configuring a shared IP jail:

IPV4

```
# iocage set ip4_addr="em0|192.168.0.10/24" UUID|TAG
```

IPV6

```
# iocage set ip6_addr="em0|2001:123:456:242::5/64" UUID|TAG
```

This command will add an IP alias of 192.168.0.10/24 to interface em0 for the shared IP jail at start time, as well as 2001:123:456:242::5/64.

Configuring a VNET jail:

To configure both IPV4 and IPV6:

```
# iocage set ip4_addr="vnet0|192.168.0.10/24" UUID|TAG
```

```
# iocage set ip6_addr="vnet0|2001:123:456:242::5/64" UUID|TAG
```

```
# iocage set defaultrouter6="2001:123:456:242::1" UUID|TAG
```

For VNET jails, a default route has to be specified also.

Additionally, to start a jail with no IPV4/6 address, set these properties:

```
# iocage set ip4_addr=none ip6_addr=none UUID|TAG
```

```
# iocage set defaultrouter=none defaultrouter6=none UUID|TAG
```

## 25.2.4 Jail Types

iocage supports five different jail types:

- thick (default)
- thin
- base
- template
- empty

Full (thick): Full (thick) jail is the default type and it is created with the following command:
