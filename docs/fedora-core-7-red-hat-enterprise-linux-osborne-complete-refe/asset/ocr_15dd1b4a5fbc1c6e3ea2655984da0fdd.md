mapping file. For example, the reverse mapping zone name for a domain with the IP address of **192.168.43** would be **43.168.192.IN-ADDR.ARPA**. In the following example, the reverse domain name for the domain address **192.168.0** is **1.168.192.IN-ADDR.ARPA**:

```
```
zone "1.168.192.IN-ADDR.ARPA"  in {
    type master;
    file "192.168.0";
}
```
```

A reverse mapping file begins with an SOA record, which is the same as that used in a forward mapping file. Resource records for each machine defined in the forward mapping file then follow. These resource records are PTR records that point to hosts in the zone. These must be actual hosts, not aliases defined with CNAME records. Records for reverse mapping begin with a reversed IP address. Each segment in the IP address is sequentially reversed. Each segment begins with the host ID, followed by reversed network numbers. If you list only a host ID with no trailing period, the zone domain is automatically attached. In the case of a reverse mapping file, the zone domain as specified in the **zone** statement is the domain IP address backward. The 1 expands to 1.1.168.192. In the following example, **turtle** and **lizard** inherit the domain IP address, whereas **rabbit** has its address explicitly entered:

```
```
; reverse mapping of domain names 1.168.192.IN-ADDR.ARPA

$
$TTL 86400
@ IN SOA turtle.mytrek.com. hostmaster.turtle.mytrek.com.(
92050300 ; Serial (yymmddxx format)
10800 ; Refresh 3hHours
3600 ; Retry 1 hour
3600000 ; Expire 1000 hours
86400 ) ; Minimum 24 hours

@ IN NS turtle.mytrek.com.
1 IN PTR turtle.mytrek.com.
2.1.168.192 IN PTR rabbit.mytrek.com.
3 IN PTR lizard.mytrek.com.
```
```

# ### IPv6 IPv6.ARPA Reverse Mapping Format

In IPv6, reverse mapping can be handled either with the current IPv6.ARPA domain format, or with the older IPv6.INT format. With IPv6.ARPA, the address is represented by a bit-level representation that places the hexadecimal address within brackets. The first bracket is preceded by a backslash. The address must be preceded by an x indicating that it is a hexadecimal address. Following the address is a number indicating the number of bits referenced. In a 128-bit address, usually the first 64 bits reference the network address and the last 64 bits are for the interface address. The following example shows the network and interface addresses for **lizard**.

```
```
\[FEC0:0000:0000:0000:00E0:18F7:3466:007D lizard IPv6 address
\[xFEC000000000000/64] lizard network address
\[x00E018F73466007D/64] lizard interface address
```
```