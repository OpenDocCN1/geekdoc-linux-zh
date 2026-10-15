# Objective 1 Configure DHCP Pools

The pool declaration can be used to specify a pool of addresses that will be treated differently than any other pool of addresses, even on the same network segment or subnet.

For example, you may want to provide a large set of addresses that can be assigned to DHCP clients that are registered to your DHCP server, while providing a smaller set of addresses, possibly with short lease times, that are available for unknown clients.

To do this, you would set up a pair of pool declarations:

```
subnet 10.0.0.0 netmask 255.255.255.0 {
  option routers 10.0.0.254;

  # Unknown clients get this pool.
  pool {
    option domain-name-servers 10.0.0.254;
    max-lease-time 300;
    range 10.0.0.100 10.0.0.250;
    allow unknown-clients;
  }

  # Known clients get this pool.
  pool {
    option domain-name-servers 10.0.0.251, 10.0.0.252;
    max-lease-time 28800;
    range 10.0.0.5 10.0.0.99;
    deny unknown-clients;
  }
}
```

It is also possible to set up entirely different subnets for known and unknown clients. "Known clients" mean, that an IP address is assigned to a MAC address using the host statement. Pools exist at the level of shared networks, so address ranges within pool declarations can be on different subnets.