The sequence starts with the client (target) transmitting a broadcast frame attempting to discover a DHCP server. This is shown by the DHCPDISCOVER message shown. The server responds (if it has been so configured and enabled) by offering an IP address for the client. This is evidenced by the DHCPOFFER message. The client then responds by testing this IP address locally. The testing includes sending the DHCPREQUEST packet to the DHCP server, as shown. Finally, the server responds by acknowledging the IP address assignment to the client, thus completing the automatic target configuration.

It is interesting to note that a properly configured client will remember the last address it was assigned by a DHCP server. The next time it boots, it will skip the DHCPDISCOVER stage and proceed directly to the DHCPREQUEST stage, assuming that it can reuse the same IP address that the server previously assigned. A booting Linux kernel does not have this capability and emits the same sequence every time it boots.

Configuration of your host's DHCP server is not difficult. As usual, our advice is to consult the documentation that came with your desktop Linux distribution. On a Red Hat or Fedora Core distribution, the configuration entry for a single target might look like Listing 12-6.

# Listing 12-6

# Example DHCP Server Configuration

```
# Example DHCP Server configuration
allow bootp;

subnet 192.168.1.0 netmask 255.255.255.0 {
  default-lease-time 1209600;   # two weeks
  option routers 192.168.1.1;
  option domain-name-servers 1.2.3.4;
  group {
    host pdnal {
      hardware ethernet 00:30:bd:2a:26:1f;
      fixed-address 192.168.1.68;
      filename "uImage-pdna";
      option root-path "/home/chris/sandbox/pdna-target";
    }
  }
}
```