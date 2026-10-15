If you are specifying a range, such as a network, you also add exceptions to the list by preceding such addresses with an exclamation point (!). In the following example, the mynetx ACL lists all those hosts in the 192.168.0.0 network, except for 192.168.0.3:

```
acl myexceptions { 192.168.0.0; !192.168.0.3; };
```

Four default ACLs are already defined for you. You can use them wherever an option uses a list of addresses as an argument. These are any for all hosts, none for no hosts, localhost for all local IP addresses, and localnet for all hosts on local networks served by the DNS server.

Once a list is defined, you can then use it with the allow-query, allow-transfer, allow-recursion, and blackhole options in a zone statement to control access to a zone. allow-query specifies hosts that can query the DNS server. allow-transfer is used for master/slave zones, designating whether update transfers are allowed. allow-recursion specifies those hosts that can perform recursive queries on the server. The blackhole option will deny contact from any hosts in its list, without sending a denial response. In the next example, an ACL of mynet is created. Then in the mytrek.com zone, only these hosts are allowed to query the server. As the server has no slave DNS servers, zone transfers are disabled entirely. The blackhole option denies access from the myrejects list, without sending any rejection notice.

```
acl mynet { 192.168.0.0; };
acl myrejects { 10.0.0.44; 10.0.0.93; };
```

```
zone "mytrek.com" {
    type master;
    file "mytrek.com";
    allow-query { mynet; };
    allow-recursion { mynet; };
    allow-transfer { none; };
    blackhole {myrejects};
};
```

# Secret Keys

Different security measures will use encryption keys generated with the dnssec-keygen command. You can use dnssec-keygen to create different types of keys, including zone (ZONE), host (HOST), and user (USER) keys. You specify the type of key with the -n option. A zone key will require the name ZONE and the name of the zone's domain name. A zone key is used in DNSSEC operations. The following example creates a zone key for the mytrek.com zone:

```
dnssec-keygen -n ZONE mytrek.com.
```

To create a host key, you would use the HOST type. HOST keys are often used in TSIG operations.

```
dnssec-keygen -n HOST turtle.mytrek.com.
```