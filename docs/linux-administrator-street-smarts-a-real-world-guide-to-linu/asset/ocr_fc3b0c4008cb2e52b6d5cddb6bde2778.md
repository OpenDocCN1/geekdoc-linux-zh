If the BOOTPROTO variable is set to something else, changing it as shown here will configure the system to use DHCP. It's usually easier to use a GUI configuration tool to set this option, however. Such tools include Network Configuration (aka system-config-network) in Red Hat and Fedora, and YaST and YaST2 in openSUSE.

> If you don't know where the relevant configuration line is found, try searching the /etc/sysconfig or /etc/conf.d directories, if they're present. Chances are you'll find configuration files with fairly obvious names. You can use grep to search these directories, or all of /etc if necessary, for files that refer to DHCP or your network interface.

Once a DHCP client is configured to run when the system boots, the configuration task is done—at least if everything works as it should. On very rare occasions, you may need to tweak DHCP settings to work around client/server incompatibilities or to have the DHCP client do something unusual. Consult the man page for your DHCP client if you need to make changes. You'll then have to modify its SysV startup script or a file to which it refers in order to change its operation.

If you want to bring the network up without rebooting the computer, you can call the SysV script directly:

```
```
# /etc/init.d/network start
```
```

As described in Phase 3, the exact path to the SysV startup scripts vary from one distribution to another. If your network was already working, but didn't use DHCP, you may need to pass the stop parameter to the script before you can pass it the start parameter.

# Static IP Address Configuration

If a network lacks a DHCP server, you must provide basic network configuration options manually. Static IP address configuration is also useful for computers that require a constant IP address, such as servers. You can set these options using interactive commands, as described shortly, but to set them in the long term, you adjust a configuration file such as /etc/sysconfig/network-scripts/ifcfg-eth0. Listing 6.1 shows a typical ifcfg-eth0 file, configured to use a static IP address. (Note that this file's exact location and name may vary from one distribution to another.)

# Listing 6.1: A Sample Network Configuration File

```
```
DEVICE=eth0
BOOTPROTO=static
IPADDR=192.168.29.39
NETMASK=255.255.255.0
NETWORK=192.168.29.0
BROADCAST=192.168.29.255
GATEWAY=192.168.29.1
ONBOOT=yes
```
```