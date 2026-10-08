The following example will encrypt and authenticate transmissions between hosts 192.168.0.2 and 192.168.0.5. Any outgoing transmissions between these hosts will be both encrypted and authenticated:

```
spadd 192.168.0.2 192.168.0.5 any -P out ipsec esp/transport//require ah/transport/require;
```

In the spadd instruction, you will need to specify the connection, such as one between two hosts or two networks. For two hosts, you would use their IP addresses, in this example, 192.168.0.2 and 192.168.0.5. You then specify the kind of packet and its direction, in this case any outgoing packet, any -P out. Then you can specify the ipsec directives for either the ESP or AH protocol, or both. For each entry, you specify the mode (transport or tunnel), the hosts involved (this can be different in tunnel mode), and the policy for the encryption, usually require. This example shows that the ESP protocol will use the transport mode for connections between 192.168.02 and 192.168.0.5, and it will be required:

```
esp/transport/192.168.02-192.168.0.5/require
```

You can leave out the host information if it is the same, as in the prior example.

```
esp/transport//require
```

# ## Receiving Hosts

For a host to receive an encrypted IPsec transmission, it must have corresponding security association instructions in its own SAD database that tell it how to authenticate and decrypt the received instructions. The security association instructions would mirror those of the sender's instructions, using the same encryption method, secret keys, and security indexes. A corresponding policy, though, is not required.

```
#!/sbin/setkey -f add 192.168.0.2 192.168.0.5 ah 15700 -A hmac-md5 "secret key"; add 192.168.0.2 192.168.0.5 esp 15701 -E 3des-cbc "secret key";
```

Receiving hosts may want to set up policies to screen incoming packets on secure connections, discarding those that are not encrypted. The following policy will accept only incoming IPsec encrypted and authenticated transmissions from 192.168.0.2.

```
spadd 192.168.0.2 192.168.0.5 any -P in ipsec esp/transport//require ah/transport//require;
```

# ## Two-Way Transmissions

The preceding example set up a secure connection between two hosts going only one way, from 192.168.0.2 to 192.168.0.5, not the other way, from 192.168.0.5 to 192.168.0.2. To implement two-way secure transmissions between two hosts, both need to be configured as the sender and the receiver, with corresponding security associations to match. The following scripts are based on common examples of a simple two-way IPsec connection between two hosts. They set up a secure two-way IPsec connection between hosts 192.168.0.2 and 192.168.0.5. Corresponding incoming policies are also included, but not required.