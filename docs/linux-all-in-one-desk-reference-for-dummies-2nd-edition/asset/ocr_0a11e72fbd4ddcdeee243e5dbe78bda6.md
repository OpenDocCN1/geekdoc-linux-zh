# **658** *Configuring DNS*

+   2. **Create the zone file** `/var/named/naba.zone` **with the following lines in it:**

```
```
$TTL	86400
$ORIGIN naba.net.
	@		IN	SOA	@ root.naba.net (
						100		; serial
						3H		;
			refresh	15M		; retry
						1W		; expiry
						1D )
			;
			minimum
		1D IN NS		@
		1D IN A		192.168.0.7
wxp	IN	A	192.168.0.2
```
```

+   3. **Create the zone file** `/var/named/0.168.192.zone` **with the following lines in it:**

```
```
$TTL	86400
; Remember zone name is: 0.168.192.in-addr.arpa
	@	IN	SOA	naba.net. root.naba.net {
			1		; Serial
			28800		; Refresh
			14400		; Retry
			3600000	; Expire
			86400 )	; Minimum
			IN	NS	naba.net.
7	IN	PTR	naba.net.
2	IN	PTR	wxp.naba.net.
```
```

+   4. **To test the new configuration, restart the named server with the following command:**

```
```
/etc/init.d/named restart
```
```

+   5. **Use** `dig` **or** `host` **to query the DNS server.**

For example, here’s how I use `host` to check the address of the host `wxp.naba.net` at the DNS server running on `localhost:`

```
```
host wxp.naba.net localhost
```
```

This command results in the following output:

```
```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:
wxp.naba.net has address 192.168.0.2
```
```

If you want to use `dig` to check the DNS server, type the following command:

```
```
dig @localhost wxp.naba.net
```
```

That `@localhost` part specifies the DNS server that `dig` contacts.