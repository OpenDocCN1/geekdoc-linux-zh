# 610 TCP/IP and Linux Protocol Implementation

# Deleting a FIB Entry

Figure 8.88 Fast accessing of the FIB through hashing--delete entry: linux/net/ipv4/fib_hash.c.

```
617
618 static int
619 fn_hash_delete(struct fib_table *tb, struct rtmag *r, struct rta *rta,
620             struct nlmsghdr *n, struct netlink_skparms *req)
621 {
622     struct fn_hash *table = (struct fn_hash*)tb->tb_data;
623     struct fib_node *fp = *del_fp, fp;
624     int z = r->rtm_dest_len;
625     struct fn_zone *fz;
626
627     fn_key_t key;
628     if (!matched)
629         #if (CONFIG_IP_ROUTE_TOS)
630             u8 tos = r->rtm_tos;
631         #endif
632
633     dprint("%d).delete: %d %08x/%d\n", tb->ib_id, r->rtm_type, rta->rta_dst ?
634             *(u32*)rta_dst, 0, rta->rta_ois ? *rta->rta_ois : -1);
635     if (z > 0)
636         return -EINVAL;
637     if ((fz = fn_hash_zones[z]) == NULL)
638         return -ESRCH;
639
640     fn_key_0(key);
641     if (rta->rta_dst) {
642         u32 dst;
643         memcpy(&dst, rta->rta_dst, 4);
644         if (dst & FZ_MASK(fz))
645             return -EINVAL;
646             key = fn_key(dst, fz);
647     }
648
649     fp = fz_chain_p(fp, fz);
650
651     FIB_SCAN(f, fp) {
652         if (fn_key_eq(f->fn_key, key))
653             break;
654         if (fn_key_leg(key, f->fn_key)
655             return -ESRCH;
656     }
657 }
```

Figure 8.89 Fast accessing of the FIB through hashing--delete entry: linux/net/ipv4/fib_hash.c.

```
658 #ifdef CONFIG_IP_ROUTE_TOS
659     FIB_SCAN_KEY(f, fp, key) {
660         if (f->fn_tos == tos)
661             break;
662     }
```