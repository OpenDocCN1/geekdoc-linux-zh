# Chapter 5 • Networking with Linux

| any | Allows all hosts. |
| none | Denies all hosts. |
| localhost | Allows the IP addresses of all interfaces on the system. |
| localnets | Allows any host on a network for which the system has an interface. |

Defining your own is simple, "acl name { address list }." Name is an alphanumeric string and address list is a list of IPs, IP prefixes, or the name of another ACL. It is possible to negate elements with "!". For instance, to exclude machines on your LAN, you could define this ACL:

```
acl notlocal { localnets; };
```

It is important to keep in mind that the matches are checked against the list from left to right; as soon as a match is found, the rest of the line is ignored.Consider these two ACLs:

```
acl first { 10.10.10/24 ; ! 10.10.10.128 ; }
acl second { 10.10.10.128 ; ! 10.10.10/24 ; };
```

Only the second one will work the way it was intended: deny the IP 10.10.10.128 name service. Since the IP prefix is tested first and matches 10.10.10.128 the denied IP is never tested. Thus the host you want to deny will be able to use your DNS server.

# Using ACLs

Now that you have an idea of how to define ACLs we'll show you how to use them.

You may want to restrict what hosts can get (transfer) your zone record to only your trusted DNS slaves, one of which we have specified in an ACL statement.

```
acl trusted_slaves {localnets; 205.157.230.253; };

zone "ratatosk.org" {
type master;
file "named.ratatosk";nallow-transfer {trusted_slaves; 208.197.103.125; };

```