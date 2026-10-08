
At the prompt, you use `nsupdate` commands to implement changes. You match on a record using its full or partial entry. To update a record, you would first delete the old one and then add the changed version, as shown here:

```
update delete rabbit.mytrek.com. A 192.168.0.2
update add rabbit.mytrek.com. A 192.168.0.44
```

## DNS Security: Access Control Lists, TSIG, and DNSSEC

DNS security currently allows you to control specific access by hosts to the DNS server, as well as providing encrypted communications between servers and authentication of DNS servers. With access control lists, you can determine who will have access to your DNS server. The DNS Security Extensions (DNSSEC), included with BIND 9.x, provide private/public key-encrypted authentication and transmissions. TSIGs (transaction signatures) use shared private keys to provide authentication of servers to secure actions such as dynamic updates between a DNS server and a DHCP server.

### Access Control Lists

To control access by other hosts, you use access control lists, implemented with the `acl` statement. `allow` and `deny` options with access control host lists enable you to deny or allow access by specified hosts to the name server. With `allow-query`, you can restrict queries to specified hosts or networks. Normally this will result in a response saying that access is denied. You can further eliminate this response by using the `blackhole` option in the `options` statement.

You define an ACL with the `acl` statement followed by the label you want to give the list and then the list of addresses. Addresses can be IP addresses, network addresses, or a range of addresses based on CIDR notation. You can also use an ACL as defined earlier. The following example defines an ACL called `mynet`:

```
acl mynet { 192.168.0.1; 192.168.0.2; };
```

If you are specifying a range, such as a network, you also add exceptions to the list by preceding such addresses with an exclamation point (!). In the following example, the `mynet` ACL lists all those hosts in the 192.168.0.0 network, except for 192.168.0.3:

```
acl myexceptions { 192.168.0.0; !192.168.0.3; };
```

Four default ACLs are already defined for you. You can use them wherever an option uses a list of addresses as an argument. These are `any` for all hosts, `none` for no hosts, `localhost` for all local IP addresses, and `localnet` for all hosts on local networks served by the DNS server.

Once a list is defined, you can then use it with the `allow-query`, `allow-transfer`, `allow-recursion`, and `blackhole` options in a `zone` statement to control access to a zone. `allow-query` specifies hosts that can query the DNS server. `allow-transfer` is used for master/slave zones, designating whether update transfers are allowed. `allow-recursion` specifies those hosts that can perform recursive queries on the server. The `blackhole` option will deny contact from any host in its list, without sending a denial response. In the next example, an ACL of `mynet` is created. Then in the `mytrek.com` zone, only these hosts are allowed to query the server. As the server has no slave DNS servers, zone transfers are disabled entirely. The **blackhole** option denies access from the `myrejects` list, without sending any rejection notice.

```
acl mynet { 192.168.0.0; };
    acl myrejects { 10.0.0.44; 10.0.0.93; };

    zone "mytrek.com" {
        type master;
        file "mytrek.com";
        allow-query { mynet; };
        allow-recursion { mynet; };
        allow-transfer { none; };
        blackhole { myrejects; };
        };
```

### Secret Keys

Different security measures will use encryption keys generated with the **dnssec-keygen** command. You can use **dnssec-keygen** to create different types of keys, including zone (ZONE), host (HOST), and user (USER) keys. You specify the type of key with the **-n** option. A zone key will require the name ZONE and the name of the zone's domain name. A zone key is used in DNSSEC operations. The following example creates a zone key for the **mytrek.com** zone:

```
dnssec-keygen -n ZONE mytrek.com.
```

To create a host key, you would use the HOST type. HOST keys are often used in TSIG operations.

```
dnssec-keygen -n HOST turtle.mytrek.com.
```

You can further designate an encryption algorithm (**-a**) and key size (**-b**). Use the **-h** option to obtain a listing of the **dnssec-keygen** options. Currently you can choose from RSA, DSA, HMAC-MD5, and DH algorithms. The bit range will vary according to the algorithm. RSA ranges from 512 to 4096, and HMAC-MD5 ranges from 1 to 512. The following example creates a zone key using a 768-bit key and the DSA encryption algorithm:

```
dnssec-keygen -a DSA -b 768 -n ZONE mytrek.com.
```

The **dnssec-keygen** command will create public and private keys, each in corresponding files with the suffixes _.private_ and _.key_. The _.key_ file is a KEY resource record holding the public key. For DNSSEC, the private key is used to generate signatures for the zone, and the public key is used to verify the signatures. For TSIG, a shared private key generated by the HMAC-MD5 algorithm is used instead of a public/private key pair.

### DNSSEC

DNSSEC provides encrypted authentication to DNS. With DNSSEC, you can create a signed zone that is securely identified with an encrypted signature. This form of security is used primarily to secure the connections between master and slave DNS servers, so that a master server transfers update records only to authorized slave servers and does so with a secure encrypted communication. Two servers that establish such a secure connection do so using a pair of public and private keys. In effect, you have a parent zone that can securely authenticate child zones, using encrypted transmissions. This involves creating zone keys for each child and having those keys used by the parent zone to authenticate the child zones.

### Zone Keys

You generate a zone key using the **dnssec-keygen** command and specifying the zone type, *ZONE*, with the *-n* option. For the key name, you use the zone’s domain name. The following example creates a zone key for the **mytrek.com** zone:

```
dnssec-keygen -n ZONE mytrek.com.
```

You can further designate an encryption algorithm (*-a*) and a key size (*-b*). Use the *-h* option to obtain a listing of the **dnssec-keygen** options. Since you are setting up a public/private key pair, you should choose either the RSA or DSA algorithm. The bit range will vary according to the algorithm. RSA ranges from 512 to 4096, and DSA ranges from 512 to 1024. The following example creates a zone key using a 768-bit key and the DSA encryption algorithm:

```
dnssec-keygen -a DSA -b 768 -n ZONE mytrek.com.
```

The **dnssec-keygen** command will create public and private keys, each in corresponding files with the suffixes *.private* and *.key*. The private key is used to generate signatures for the zone, and the public key is used to verify the signatures. The *.key* file is a KEY resource record holding the public key. This is used to decrypt signatures generated by the corresponding private key. You add the public key to the DNS configuration file, **named.conf**, using the **$INCLUDE** statement to include the *.key* file.

### DNSSEC Resource Records

In the zone file, you then use three DNSSEC DNS resource records to implement secure communications for a given zone: KEY, SIG, and NXT. In these records, you use the signed keys for the zones you have already generated. The KEY record holds public keys associated with zones, hosts, or users. The SIG record stores digital signatures and expiration dates for a set of resource records. The NXT record is used to determine that a resource record for a domain does not exist. In addition, several utilities let you manage DNS encryption. With the **dnskeygen** utility, you generated the public and private keys used for encryption. **dssigner** signs a zone using the zone’s private key, setting up authentication.

To secure a DNS zone with DNSSEC, you first use **dnskeygen** to create public and private keys for the DNS zone. Then use **dssigner** to create an authentication key. In the DNS zone file, you enter a KEY resource record in which you include the public key. The public key will appear as a lengthy string of random characters. For the KEY record, you enter in the domain name followed by the KEY and then the public key.

```
mytrek.com. KEY 0x4101 3 3 (AvqYXgk/uguxkJF/hbrP YZxZFG3x8EfnX389L7GX6w7rlLYBJ14TgvrDVXr84XsSxg+OFcUJaFnr84UDRE23dGnrlRAMZA1jFV0UWDWHCR2zjJnvgV92JB2ULMGJheDHeyzM1KG2dOGkAensm74N1FQkZy/3KZ9KnmQmEpj/EEBn48Va5gAT9KmjN+V3
```
