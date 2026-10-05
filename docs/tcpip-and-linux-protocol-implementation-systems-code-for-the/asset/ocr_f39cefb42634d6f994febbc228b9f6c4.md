# TCP/IP and Linux Protocol Implementation

```
70      struct fib_node         *fn_next;
71      struct fib_info         *fn_info;
72  #define FIB_INFO(f)     ((f)->fn_info)
73      fn_key_t                fn_key;
74      u8                      fn_tos;
75      u8                      fn_type;
76      u8                      fn_scope;
77      u8                      fn_state;
78  );\n79
80  #define FN_S_ZOMBIE 1
81  #define FN_S_ACCESSED 2
82
83      static int fib_hash_zombies;
```

> Figure 8.73 Fast accessing of the FIB through hashing-types ii: linux/net/ipv4/fib_hash.c.

```
85 struct fn_zone
86 {
87     struct fn_zone *fz_next;    /* Next empty zone *//
88     struct fib_node **fz_hash;  /* Hash table pointer *//
89     int             fz_zent;      /* Number of entries *//
90
91     int             fz_divisor;   /* Hash divisor      *//
92     u32             fz_hashmask;  /* (1<fz_divisor) - 1 *//
93 #define FZ_HASHMASK(fz) ((fz)->fz_hashmask)
94
95     int             fz_order;   /* Zone order        *//
96     u32             fz_mask;/
97 #define FZ_MASK(fz)     ((fz)->fz_mask)
98 };
99
100 /* NOTE: Un fast computers evaluation of fz_hashmask and fz_mask
101 can be cheaper than memory lookup, so that FZ_* macros are used.
102 */
103
104 struct fib_hash
105 {
106     struct fn_zone *fn_zones[33];
107     struct fn_zone *fn_zone_list;
108 };
```

> Figure 8.74 Fast accessing of the FIB through hashing-inline functions i: linux/net/ipv4/fib_hash__hash.c.

```
110 static __inline_u32 fib_hash_idx_t fn_hash(struct fn_key_t key, struct fn_zone *fz)
11 {
112     u32 h = ntohl(key.datum)>>(32 - fz->fz_order);
113     h = (h>>20);
114     h = (h>>10);
```