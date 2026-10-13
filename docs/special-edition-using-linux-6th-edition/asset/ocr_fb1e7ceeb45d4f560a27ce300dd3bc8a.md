# LISTING 30.2 CONTINUED

```
BROADCAST=192.168.1.255
GATEWAY=192.168.1.1
ONBOOT=yes
#>>>End of variable declarations
```

The Red Hat file contains basically the same information. In Red Hat, a PROTO line will be present with either static or dynamic as its argument. The NETWORK and BROADCAST entries are not included, and the GATEWAY entry is found in /etc/sysconfig/network.

Note the GATEWAY specification in the sample entry. It is pointing to the IP address used by rumble.fish.net, which is the server that will eventually be connecting to the Internet. All computers that will be given access to the Internet through rumble need to have it specified as the gateway system; otherwise, no Internet access will be possible.

You cannot have your system gating through an Ethernet card and through a modem at the same time; if you are using PPP and a modem to go out to the Internet, do not specify an Ethernet gateway. Replace any address in the GATEWAY= line with none.

> **Note**
> 
> Although all other systems list `rumble.fish.net` as their gateway, the `rumble.fish.net` system should not have any entry as a gateway in this example. If `rumble.fish.net` were connected to a router (DSL router or cable modem box) using an Ethernet cable, it would have that router or modem’s IP listed as its gateway. In this network, the gateway will be set up dynamically through the modem when a connection is made to the Internet.

Also note the netmask, network, and broadcast addresses. These are used on all computers on the network. In fact, the only address that changes per machine on a typical network is the IP address; all the rest of the addresses are shared among all computers on the same subnetwork.

> **Caution**
> 
> The netmask defines the network in use (its beginning and ending). If you assign a different netmask to any of the hosts, they will be on another network. This can adversely affect their capability to communicate with other hosts on the network.

When discussing addresses, it is important to note that some sort of name server is required for Internet use (your hosts files only cover address conversion on the local network). Because Internet navigation will be common on this network, the ISP’s name servers need to be used when addresses outside the local network are requested (unless you’ve opted to set up your own DNS). These addresses are entered in various locations on the various systems (for instance, in the Network setup under Control Panel on Windows systems, and the MacTCP extension on the Mac), but on Linux, they are entered in the /etc/resolv.conf file. Assuming the IP address for the ISP’s nameservers are 192.168.100.100 and 192.168.100.101, Listing 30.3 illustrates the Linux systems’ /etc/resolv.conf files (including rumble’s):