# Chapter 17 DNS: The Domain Name System

program, and with improper configuration it might let anyone on the Internet
mess with your name server. The syntax is

```
controls {
  inet_addr port ip-port allow { address_match list } keys { key_list };
}
```

The port that rndc uses to talk to named defaults to 953 if it is not specified
with the port clause.

Allowing your name server to be controlled remotely is both handy and dangerous. Strong authentication through a key entry in the allow clause is required; keys in the address match list are ignored and must be explicitly stated in the keys
clause of the controls statement.

You can use the rndc-command to generate an authentication key for you
bween rndc and named. There are essentially two ways to set this up: you can
have both named and rndc use the same configuration file to learn the key
(/etc/rndc.key), or you can include the key in both the rndc and rndc configuration-
files (/etc/rndc.conf and /etc/named.conf for named). The latter
out is more complicated, but it's necessary when named and rndc will run
iffer different computers. rndc-a sets up keys for localhost access.

When no controls statement is present, BIND binds to the loopback address
t address list and looks for the key in /etc/rndc.key. Because strong
authentication is mandatory; the rndc command cannot control named if there is
no key. This precaution may seem draconian, but consider: even if rndc worked
only 127.0.0.1 and this address was blocked from the outside world at your
firewall, you would still be telling all users not to tamper with your name
server. Any user can use telnet to the control port and type "stop"—quite an effective
d own service attack.

Here is an example of the output (to standard out) from rndc-config when
256-bit key is requested. We chose 256 bits because it fits on the page. You would
ormally choose a generator key and redirect the output to /etc/rndc.conf. The com-ments at the bottom of the output shows the lines you need to add to named.conf
to make named and rndc play together.

```
$ rndc-config -b 256
# Start of rndc.conf
key "rndc-key" {
  algorithm hmd5:
  secret "OrUz2samkUnEp52zlHdX6cd5hACldOGsG/elP/dv2IY";
}
```

```
default {
  default-key "rndc-key"
  default-server 127.0.0.1;
  default-port 953;
}
# End of rndc.conf
```