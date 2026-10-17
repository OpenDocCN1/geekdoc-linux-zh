
The name server record specifies the name of the name server for these zone. These have a resource record type of `NS`. If you have more than one name server, list them in `NS` records. These records usually follow the same domain as the `SOA` record, the name field is often left blank or `@` symbol to indicate the server's domain name specified by the previous `SOA` record.

```
IN NS turtle.mytrek.com.
```

You can, if you wish, enter the domain name explicitly as shown here:

`mytrek.com. IN NS turtle.mytrek.com.`

## Address Record: A and A6

Resource records of type `A` records associate a fully qualified domain name with an IP address. Often, they are hidden. Any domain without a terminating period automatically will have the domain `mytrek.com`, the turtle name in the example is expanded to `turtle.mytrek.com`:

```
rabbit.mytrek.com IN A 192.168.0.2
turtle IN A 192.168.0.1
```

`BIND` versions `8.2.2` and `9.1` support IPv6 addresses which have a different format from that of the IPv4 addresses used. Instead of numerals separated in segments (Chapter 38), IPv6 addresses use hexadecimal numbers represented in segments. In the following example, `turtle.mytrek.com` is associated with a site-local IPv6 address `fe80::`. Recall that there are only three fields in a site-local: format prefix, sub-net identifier, and interface identifier. The empty segments is created with the unregistered version of `CHM2PDF Pilot`.

The empty slots of the sub-net identifier can be represented by an empty colon (`:`). The identifier `8:8000:200C:417A` follows

`turtle.mytrek.com. IN A6 FE0::8800:200C:417A`

IPv6 also uses the IPv4 addresses as an interface identifier, instead of the MAC-derived identifier. The network information part of the IPv6 address would use IPv6 notation and the remaining interface (host) identifier would use the full IPv4 address. These are known as mixed addresses. In the next example, `lizard.mytrek.com` is given a mixed address using IPv6 information.

`lizard.mytrek.com. IN A6 ::192.168.0.3`

## Mail Exchanger: MX

The `MX` record specifies the mail server for your zone. The `MX` record informs the remote site of your zone's mail server. In the next example, `lizard.mytrek.com` is given a mixed address using IPv6 information.

`lizard.mytrek.com. IN A6 ::192.168.0.3`

## Aliases: CNAME

Resource records of type `CNAME` are used to specify alias names for a host. Aliases are often used for machines. Aliases are also used to locate a host when it changes. In the following example, `ftp.mytrek.com` is an alias for:

`ftp.mytrek.com IN CNAME turtle.mytrek.com`

The `CNAME` stands for canonical. The canonical name is the actual name of the host. In the preceding example, the canonical name is `turtle.mytrek.com`. The alias, also known as `CNAME`, cannot be used for `NS` (name server) or `MX` (mail server). For those records, you need to use the original domain name or IP address.

A more stable way to implement aliases is simply to create another record for a host. You may have many hosts with the same IP address as you, provided they are certified. For example, to make `www.mytrek.com` an alias for `turtle.mytrek.com`, you only have to add another record for it, giving it the same IP address as `turtle.mytrek.com`.

```
turtle.mytrek.com. IN A 192.168.0.1
www.mytrek.com. IN A 192.168.0.1
```

## Pointer Record: PTR

A `PTR` record is used to perform reverse mapping from an IP address to a host. `PTR` records are used in the reverse mapping files. The name entry holds a reversed IP address, and the data entry holds the name of the host. The following example maps the IP address `192.168.0.1` to `turtle.mytrek.com`:

```
1.1.168.192 IN PTR turtle.mytrek.com.
```

In a `PTR` record, you can specify just that last number segment of the address (the host address) and let DNS fill in the domain part of the address. In the next example, `1` has the domain address, `1.168.192`, automatically added to `1.1.168.192`:

```
1 IN PTR turtle.mytrek.com.
```

## 区域文件 (Zone Files)
