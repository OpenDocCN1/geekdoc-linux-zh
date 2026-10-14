
# 基础设施协议 379

```c
"%Interface BytesIn PktsIn BytesOut PktsOut Flags Local Remote\n",
pos=len;
read_lock(&kmrt_lock);
for (ct=0;ct<maxif;ct++)
  {
      char *name = "none";
      vif=&vif_table[ct];
      if(VIF_EXISTS(ct))
        continue;
      if (vif->dev)
          name = vif->dev->name;
```

```c
size = sprintf(buffer+len, "%2d-%10s %x1d %x1d %x1d %08x %08x %08x\n",
    ct, name, vif->bytes_in, vif->pkt_in, vif->bytes_out, vif->pkt_out,
    vif->flags, vif->local, vif->remote);
len+=size;
pos+=size;
if(pos<offset) {
    len=0;
    begin=pos;
    if(pos>offset+length) {
        break;
    }
}
read_unlock(&zrt_lock);
*start=buffer+(offset-begin);
len-==(offset-begin);
if (len<length) {
    len=length;
    if (len<0)
        len = 0;
}
return len;
```

图 2.244 IPMR–procs mfc reporting：`linux/net/ipv4/ipmr.c`。

```c
static int ipmr_mfc_info(char *buffer, char **start, off_t offset, int length)
{
    struct mfc_cache *mfc;
    int len=0;
    off_t pos=0;
    off_t begin=0;
    int size;
    int ct;
    len += sprintf(buffer,
        "Group Origin Ifn Pkts Bytes Wrong Oifs\n",
        pos=len);
    read_unlock(&zrt_lock);
    for (ct=0;ct<MFC_LINES;ct++) {
        for(mfc=mfc_array[ct]; mfc; mfc=mfc->next) {
            int n;
        }
    }
    /*
     * 接口转发映射
     */
    size = sprintf(buffer+len, "%08X %08X-%3d %x1d %x1d",
        (unsigned long)mfc->mfc_mcastgrp,
        (unsigned long)mfc->mfc_origin,
```

# 380 TCP/IP 与 Linux 协议实现

```c
mfc->mfc_parent,
mfc->mfc_un.res.pkt,
mfc->mfc_un.res.bytes,
mfc->mfc_un.res.wrong_if;
for(n=mfc->mfc_un.res.minv;n<mfc->mfc_un.res.maxv;n++)
{
if(VIP_Exists(n) && mfc->mfc_un.res.ttl[n] < 256)
size += sprintf(buffer+len, "%X2d-%3d", n, mfc->mfc_un.res.ttl[n]);
size += sprintf(buffer+len, "In");
len+=size;
pos+=offset;
if(pos<offset) {
len=0;
begin=pos;
}
if(pos>offset+length)
goto done;
}
}
```

图 6.245 IPMR-procs from mfc reporting：`linux/net/ipv4/ipmr.c`。

```c
spin_lock_bh(mfc_un_lock);
for(mfc=mfc_un_queue; mfc; mfc=mfc->next)
size = sprintf(buffer+len, "%08X %X-3d %8ld %8d\n",
(unsigned long)mfc->mfc_castgrp,
(unsigned long)mfc->mfc_origin,
-1,
(long)mfc->mfc_un.res.qlen,
OL);
len+=size;
pos+=size;
if(pos<offset) {
len=0;
begin=pos;
}
if(pos>offset+length)
break;
}
spin_unlock_bh(mfc_un_lock);
done:
read_unlock(kmrt_lock);
*start=buffer+(offset-begin);
len=(offset-begin);
if(len>length)
len=length;
```

```c
if (len < 0) {
  len = 0;
}
return len;
}
```

## 6.5.6 IP IP 组播

图 6.246—初始组播：`linux/net/ipv4/ipmr.c`。

```c
#ifndef CONFIG_IPISM_V2
struct inet_protocol pim_protocol = {
  pim_rcv,            /* PIM 处理程序 */
  NULL,               /* PIM 错误控制 */
  NULL,               /* 下一个 */
  IPPROTO_PIM,       /* 协议 ID */
  0,                  /* 拷贝 */
  NULL,               /* 数据 */
  "PIM",             /* 名称 */
};
#endif

/*
 * IP 组播路由
 */
void __init_ip_mr_init(void) {
  printk(KERN_INFO "Linux IP multicast router 0.0 plus PIM-SM\n");
  m_cache = kmem_cache_create("ip_mr_cache",
                                sizeof(struct mfc_cache),
                                0, SLAB_HWCACHE_ALIGN,
                                NULL, NULL);
  init_timer(&ipmr_expire_timer);
  ipmr_expire_timer.function=ipmr_expire_process;
  register_netdevice_notifier(&ip_mr_notifier);
  #ifdef CONFIG_PROF_PIM
  proc_net_create("ip_mr_vif",ipmr_vif_info);
  proc_net_create("ip_mr_cache",0,ipmr_mfc_info);
#endif
```

## 6.6 NAT、隧道和其他技巧

这三种技术（NAT、IP 中的 IP 和 GRE）非常相似——组播支持也十分相似。第 10 章将详细介绍网络地址翻译。

## 6.7 网络地址翻译

网络地址翻译在地址不足的地方非常流行，也经常作为简单站点安全的一部分，特别是与防火墙配合使用。
