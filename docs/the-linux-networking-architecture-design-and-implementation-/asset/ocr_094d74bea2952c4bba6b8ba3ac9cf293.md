```
struct ip_conntrack_tuple tuple;
struct ip_conntrack_tuple mask;
/* Helper function: returns verdict */
unsigned int (*help)(struct ip_conntrack *ct,
struct ip_nat_info *info,
enum ip_conntrack_info ctinfo,
unsigned int hooknum,
struct sk_buff **pskb);
};

const char *name;
```

help is a pointer to the main function of the helper module, which is invoked by do_bindings(), as was mentioned previously.