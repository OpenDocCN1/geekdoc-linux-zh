# Routing 555

The overall structure (see Figure 8.6) is complex. Usually, FIB-related functions return the fib_result type (see Figure 8.7) as a reference parameter, with the fib_info *fi field pointing at the appropriate entry.

The fib_table structure is a more generic interface to the FIB, including pointers to the various FIB access functions, so that new FIB functions can be written by routing system. Currently, the only set of lookup functions in the fib_hash module are defined, so the pointers are only initialised to point at the respective fn_functions.

# 8.8 FIB generic interface: linux/include/net/ip_fib.h

```
struct fib_table
{
    unsigned char tb_id;
    unsigned tb_stamp;
        (*tb_lookup)(struct fib_table *tb, const struct rtm_key *key, struct
            fib_result *res);
    int
                (*tb_insert)(struct fib_table *table, struct rtmmsg *rtmsg,
            struct kern_rta *rta, unsigned nmsghdb *n,
            struct netlink_skb_parts *req);
    int
        (*(*_delete)(struct fib_table *table, struct rtmmsg *rtmsg,
            struct kern_rta *rta, unsigned nmsghdb *n,
            struct netlink_skb_parts *req);
    int
        (*tb_dump)(struct fib_table *table, struct sk_buff *skb,
            struct netlink_callback *cb);
    int
        (*tb_get_info)(struct fib_table *table, char *buf,
            int first, int count);
    void
        (*tb_select_default)(struct fib_table *table,
            const struct rtm_key *key, struct fib_result *res);
    unsigned char tb_data[0];
};
```

# 8.3.5 FIB Code

The FIB implementation is split into four main parts. There is a front end (fib_front), which is the externally visible interface to the FIB. Then there the fib_rules module, which implements the set of ways that we pick a next hop—we to discriminate from one another potentially by policy or metric, as well as on longest match. Thirdly, we have the fib_semantics module, which deals with the arcane definitions of what nexthop really means—this is well described in the comment in Figure 8.37. Finally, there is the fib_hash module, which implements the set of hash functions described earlier in this chapter.