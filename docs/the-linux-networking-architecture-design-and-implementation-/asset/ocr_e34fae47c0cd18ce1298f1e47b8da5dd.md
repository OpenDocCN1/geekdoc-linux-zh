# 21.4.1 Transport Protocols

The functions ip_nat_protocol_register() and ip_nat_protocol_unregister() can be used to register a new transport protocol or to unregister an existing protocol. When registering a new protocol, we have to pass a pointer to a structure of the type ip_nat_protocol as a parameter.

```
struct_ip_nat_protocol  linux/netfilter/ipv4/ip_nat_protocol.h
struct ip_nat_protocol {
	struct list_head list;
	/* Protocol name */
	const char *name;
	/* Protocol number. */
	unsigned int protum;
	/* Do a packet translation according to the ip_nat_proto_manip
	and and manipulate type. */
	void (*manip_pkt)(struct iphdr *iph, size_t len,
		struct ip_conntrack_manip *manip,
		enum ip_nat_manip_type manipt,
		const struct ip_conntrack_tuple *tuple);
/* Is the mappable part of the tuple between min and max incl? */
	int (*in_range)(const struct ip_conntrack_tuple *tuple,
		enum ip_nat_manip_type manipt,
		const struct ip_conntrack_manip_proto *min,
		const struct ip_conntrack_manip_proto *max);
```

/* Alter the per-proto part of the tuple (depending on maniptype), to give a unique in the given range if possible; return false if not. Per-protocol part of tuple is initialized to the incoming packet. */
int (*unique_tuple)(struct ip_conntrack_tuple *tuple,
		const struct ip_nat_range *range,
		enum ip_nat_manip_type maniptype,
		const struct ip_conntrack *conntrack);
	ununsigned int (*print)(char *buffer,
		const struct ip_conntrack_tuple *match,
		const struct ip_conntrack_tuple *mask);

unsigned int (*print_range)(char *buffer,
		const struct ip_nat_range *range);

The list header required to manage the protocol list contains pointers to predecessors and successors and is initially set to {NULL, NULL}.