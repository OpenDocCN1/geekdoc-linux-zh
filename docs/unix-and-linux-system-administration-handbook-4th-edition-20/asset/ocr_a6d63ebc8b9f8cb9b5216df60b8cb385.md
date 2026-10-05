# Solaris firewalls and filtering

variables. Many variable names are the same, so you can partially work around
Sun's minimal **ndd** man page.

Interface-specific options such as link speed, autonegotiation, and jumbo packet
support are also set with **ndd**; run **ndd** directly on the device file for the interface
(e.g., `/dev/e100g0`). Unfortunately, the way Sun has set this up nowadays makes the
names of the configuration parameters dependent on the specific driver, so
isn't a universal recipe for it, locking a network interface to 100 Mb/s.

To change speeds, you'll need to identify the writable "capability" variables for
e speed (usually named `_cap`) and turn off (set to zero) all the ones you want to disallow. Turn off the `_autoneg_cap` variable, to disable autonegotiation.
 example, the following script sets `/dev/e100g0` to 100 Mb/s full duplex on
of one of our machines:

```
!/bin/sh
ndd -dev/e100g0 adv_autoneg_cap 0
ndd -dev/e100g0 adv_1000fdx_cap 0
ndd -dev/e100g0 adv_100fdx_cap 1
ndd -dev/e100g0 adv_10hdx_cap 0
ndd -dev/e100g0 adv_10fdx_cap 0
ndd -dev/e100g0 adv_10hdx_cap 0
```

# Solaris security

Table 14.11 shows Solaris's default behavior with regard to very touchy net-work issues. For a brief description of the implications of these behaviors, see Se-curity issues starting on page 472. You can adjust most of these using **ndd**.

| Feature | Default | ndd variable |
| :--- | :--- | :--- |
| IP forwarding | off | ip_forwarding |
| ICMP redirects | obeys | Can't be changed* |
| Routing source | ignores | ip_forward_src_routed |
| Broadcast ping (respond) | on | ip_respond_to_echo_broadcast |
| Broadcast ping (forward) | off | ip_forward_directed_broadcasts |

a. You can only modify the entries' time-to-live.

# Solaris firewalls and filtering

As mentioned in the **Security issues section**, you generally shouldn't use a UNIX,
Linux, or Windows box as a firewall or NAT gateway. A dedicated piece of
network hardware stands. Solaris used to make it easy to follow this rule by
including any filtering software, but Darren Reed's free IPFilter software has now
bun bundled into the basic distribution. If you must use a UNIX-based filter, this
is a good choice—it was always our favorite of the add-on filters for Solaris.