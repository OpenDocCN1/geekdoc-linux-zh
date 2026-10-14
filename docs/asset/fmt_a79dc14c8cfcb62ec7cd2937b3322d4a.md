
# TCP/IP 和 Linux 协议实现

## 删除 FIB 条目

图 8.7 通过哈希表快速访问 FIB--插入条目 `vi`：`linux/net/ipv4/fib_hash.c`。

```c
if (del_fp) {
    f = del_fp;
    /* 解链节点 */
    write_lock_bh(&fib_hash_lock);
    f = f->fn_next;
    del_fp = unlock_bh(&fib_hash_lock);
    if (!(f->fn_state&FN_S_ZOMBIE))
        rtmsg_fib(RTM_DELROUTE, f, z, tb->tb_id, n, req);
    if (f->fn_state&FN_S_ACCESSED)
        rt_cache_flush(-1);
        free_node(f);
        fz->nent--;
} else {
    rt_cache_flush(-1);
}
rtmsg_fib(RTM_NEWROUTE, new_f, z, tb->tb_id, n, req);
return 0;
out:
fib_release_info(fi);
return err;
}
```

图 8.88 通过哈希表快速访问 FIB--删除条目：`linux/net/ipv4/fib_hash.c`。

```c
static int
fn_hash_delete(struct fib_table *tb, struct rmag *r, struct rta *rta,
            struct nlmsghdr *n, struct netlink_skparms *req)
{
    struct fn_hash *table = (struct fn_hash*)tb->tb_data;
    struct fib_node *fp = *del_fp, fp;
    int z = r->rtm_dest_len;
    struct fn_zone *fz;
    fn_key_t key;
    if (!matched)
        #if (CONFIG_IP_ROUTE_TOS)
            u8 tos = r->rtm_tos;
        #endif
    dprint("%d).delete: %d %08x/%d\n", tb->ib_id, r->rtm_type, rta->rta_dst ?
            *(u32*)rta_dst, 0, rta->rta_ois ? *rta->rta_ois : -1);
    if (z > 0)
        return -EINVAL;
    if ((fz = fn_hash_zones[z]) == NULL)
        return -ESRCH;
    fn_key_0(key);
    if (rta->rta_dst) {
        u32 dst;
        memcpy(&dst, rta->rtm_dst, 4);
        if (dst & FZ_MASK(fz))
            return -EINVAL;
            key = fn_key(dst, fz);
    }
    fp = fz_chain_p(fp, fz);
    FIB_SCAN(f, fp) {
        if (fn_key_leq(key, fp)->fn_key)
            break;
        if (fn_key(key, fz)
            return -ESRCH;
    }
}
```

图 8.89 通过哈希表快速访问 FIB--删除条目：`linux/net/ipv4/fib_hash.c`.

```c
#ifdef CONFIG_IP_ROUTE_TOS
    FIB_SCAN_KEY(f, fp, key) {
        if (f->fn_tos == tos &&
            break;
    }
#endif
```

### 路由

```c
matched = 0;
del_fp = NULL, tos;
FIB_SCAN_TOS(f, fp, key, tos) {
    struct fib_info *fi = FIB_INFO(f);
    if (fi->fib_priority <= FIB_INFO(f)->fib_priority)
        break;
    }
}
```

# TCP/IP 与 Linux 协议实现

> **图 8.91** 通过哈希-冲刷条目快速访问 FIB：`linux/net/ipv4/fib_hash.c`。

```c
711 extern __inline__ int
712 fn_flush_list(struct fib_node **fp, int z, struct fn_hash *table)
713 {
714     int found = 0;
715     struct fib_node *f;
716
717     while (f = *fp) {
718         struct fib_info *fi = FIB_INFO(f);
719
720         if (fi && (f->state&FN_S_ZOMBIE) || (f->fib_flags&RTNH_F_DEAD)) {
721             write_lock_bb(&fib_hash_lock);
722             *fp = f->fn_next;
723             write_unlock_bb(&fib_hash_lock);
724
725             fn_free_node(f);
726             found++;
727             continue;
728         }
729         fp = &f->fn_next;
730     }
731     return found;
732 }
734 static int fn_hash_flush(struct fib_table *tb)
735 {
736     struct fn_hash *table = ((struct fn_hash*)tb)->tb_data;
737     struct fn_zone *fz;
738     int found = 0;
739
740     fib_hash_zombies = 0;
741     for (fz = table->fz_list; fz; fz = fz->fz_next) {
742         int i;
743         int tmp = 0;
744         for (i=fz->fz_divisor-1; i>=0; i--)
745             tmp += fn_list_flush(&fz->fz_hash[i], fz->fz_order, table);
747             fz->fz_nent = tmp;
747             found += tmp;
748     }
749     return found;
750 }
```

# 管理

> **图 8.92** 访问 FIB–PROC fs 访问：`linux/net/ipv4/fib_hash.c`。

```c
755 static int fn_hash_get_info(struct fib_table *tb, char *buffer, int first, int count)
756 {
757     struct fn_hash *table = ((struct fn_hash*)tb)->tb_data;
758     struct fn_zone *fz;
759     int pos = 0;
c
int n = 0;
read_lock(&fib->hash_lock);
for (fz=table->zone_list; fz; fz=fz->next) {
  int i;
  struct fib_node *f;
  int maxslot = fz->fz_divisor;
  struct fib_node **fp = fz->hash;
  if (fz->fz_next == 0) 
    continue;
    if (pos + fz->fz_next <= first) {
```
