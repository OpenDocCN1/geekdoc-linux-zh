

# TCP/IP 与 Linux 协议实现

```
1022  int len=0;
1023  off_t pos=0;
1024  int size;
1025  char hbuffer[HBUFFERLEN];
1026  int i,j,k;
1027  const hexbuf[] = "0123456789ABCDEF";
1028
1029  size = sprintf(buffer,"IP address HW type Flags HW address Mask Device="%s");

1030
1031  pos+=size;
1032  len+=size;

1033
1034  for(i=0; i<NEIGH_HASHMASK; i++) {
1035    struct neighbour *n;
1036    read_lock_bh(&arp_tbl[i]);
1037    for (n=arp_tbl[i].hsb_buckets[j]; n; n=n->next) {
1038      struct net_dev *dev = n->dev;
1039      int intype = dev->type;

1040
1041      /* 不要将用户的 "arp -a" 与魔术项混淆 */
1042      if ((n->nud_state&NUD_NOARP))
1043        continue;
1044  }

1045
1046  read_lock(kn->lock);
```

![](img/06c11ba8be5c1c24aa633e12618e2ebd_361_0.png)

```
1047  /*
1048   * 将硬件地址转换为 XX:XX:XX ... 格式。
1049   */
1050  #if defined(CONFIG_AX25) || defined(CONFIG_AX25_MODULE)
1051    if (intype == ARPHRD_AX25 || intype == ARPHRD_NETROM)
1052      asc2c((ax25_address)n->ha, hbuffer);
1053    else {
1054
1055  endif
1056  for (k=0; k<HBUFFERLEN-3 && dev->addr_len>j; j++) {
1057    hbuffer[k++]=hexbuf[n->ha[j]]>>4];
1058    hbuffer[k++]=hexbuf[n->ha[j]&15];
1059    hbuffer[k++]=';';

1060
1061  }
1062  hbuffer[k--]=0;
1063  }
1064  #if defined(CONFIG_AX25) || defined(CONFIG_AX25_MODULE)
1065  #endif

1066
1067  {
1068    char tbuffer[16];
1069    sprintf(tbuffer,"%Xu.%Xu.%Xu.%Xu",NIPQUAD(*(u32*)n->primary_key));
1070    size = sprintf(buffer+len,"X-%16s 0x-%10x-%10xs",
```

```
tbuf,
hatype,
arp_state_to_flags(n),
hbuffer,
dev->name);
}
read_unlock(an->lock);
len += size;
pos += size;
if (pos <= offset) {
len=0;
if (pos >= offset+length) {
read_unlock_bb(&arp_tbl.lock);
goto done;
}
}
read_unlock_bb(&arp_tbl.lock);
```

# 图 6.139 ARP--用户接口--进程入口点--表：linux/net/ipv4-arp.c.

```
for (i=0; i<=PNEIGH_HASHMASK; i++) {
  struct peigh_entry *n;
  for (arp_tbl->phaas_buckets[i]; n; n=n->next) {
    struct net_dev *dev = n->dev;
    int hatype = dev ? dev->type : 0;

    char tbuf[16];
    sprintf(tbuf, "%hu,%xu,%xu,%xu+(%hu", NIPQUAD((u32)n->key));
    size = snprintf(buffer+len, "-16s 0x%02x-0x%02x * %s\n",
    tbuf,
    hatype,
    ATF_PUBL|ATF_PERM,
    "%00:00:00:00:00:00",
    dev ? dev->name : "s");
  }
}
len += size;
pos += size;

if (pos <= offset) {
len=0;
if (pos >= offset+length) {
goto done;
```

# 308 TCP/IP 与 Linux 协议实现

```
1121 done:

1122
     *start = buffer-len-(pos-offset);  /* 数据起始 */
1124 len = pos-offset;      /* 偏移 */
1125 if (len<length)
1126     len = length;          /* 结束 */
1127     if (len<0)
1128         len = 0;
1129         return len;

1130 
}
1131 #endif
```

图 6.140 ARP-接口关闭：linux/net/ipv4/arp.c.

```
1133 /* 注意，它不在通知链上。
1134 在路由缓存被刷新后调用此例程是必要的。
1136 */
1137 void arp_ifdown(struct net_device *dev)
1138 {
1139     neigh_ifdown(&arp_tbl, dev);
1140 }
```

# ARP 初始化与用法

图 6.141 ARP-初始化：linux/net/ipv4/arp.c.

```
1147 static struct packet_type arp_packet_type =
1148 {
     htons(ETH_P_ARP),
1150     /* 所有设备 */
1151     arp_rcv,
1152     (void*)i,
1153     NULL
1154 };
1155 void __init_arp(void)
1156 {
     neigh_table_init(&arp_tbl);

1158     dev_add(&arp_packet_type);

1159
     proc_create("arp", 0, arp_get_info);
1161 #ifdef CONFIG_SYSCTL
1162     neigh_sysctl_register(NULL, &arp_tbl.params, NET_IPV4, NET_IPVIGH, "ipv4");
1163 #endif
1164 }
```

图 6.142 ARP-X25字符串转换：linux/net/ipv4/arp.c.

```
1170 #ifdef CONFIG_FS
1171 #if defined(CONFIG_AX26) || defined(CONFIG_AX26_MODULE)
1172  /*
1173  X25 ASCII 转换
1174  */
1175  char *ax25_asc(ax25_address, *ama, char *buf)
1176 {
1177     char c, *s;
1178     int n;
1179     for (n = 0, s = buf; n < 6; n++) {
1180         c = (ax26_call[n] >> 1) & 0x7F;
1181         if (c != ' ') s++ = c;
1182     }
1183     *s++ = '-';
1184     if ((n = (ax26_call[n] >> 1) & 0x0F) > 9) {
1185         s++ = '1';
1186         n = 10;
1187     }
1188     *s++ = n + '0';
1189     *s++ = '\0';
1190     if (*buf == '\0' || *buf == '-') {
1191         return "*";
1192     }
1193     return buf;
1194 }
1195 #endif
1204 #endif
```

# 6.4 网络层调试–ICMP

图 6.143 ICMP，主机要求符合性：linux/net/ipv4/icmp.c.

- RFC 1122（主机要求 – 通信层）状态：（有很多关于 ICMP 的规则）
- 3.2.2（通用 ICMP 内容）
- 必须丢弃未知类型。（OK）
- 必须复制违规包的前 8 个字节

# TCP/IP 与 Linux 协议实现

- 在发送 ICMP 错误时。（废弃）—— RFC 1812
- 必须将 ICMP 错误传递到协议层。（OK）
- 应发送 TOS = 0 的 ICMP 错误。（废弃）-- RFC 1812）
- 不得在回复中发送 ICMP 错误：
- ICMP 错误（OK）
- 广播/组播数据报（OK）
- MAC 广播（OK）
- 非初始分片（OK）
- 源地址不是单个主机的数据报。（OK）
- 3.2.2.1（目标不可达）
- 所有规则都支配 IP 层，并在 ip.c 中处理，而非此处。
- 3.2.2.2（重定向）
- 主机不发送 ICMP_REDICTS。（OK）
- 响应主机或网络重定向时必须更新路由表。
-（主机 OK，网络废弃）
- 如果重定向不是来自直接连接的网关，应丢弃（OK —— 我们丢弃它不是我们的旧网关，这足够了）

图 6.144 ICMP，主机增强符合性：linux/net/ipv4/icmp.c.

- 3.2.2.3（源塞交通）
- 必须将入的 SOURCE_QUENCH 传递到传输层（OK）
- 其他要求由传输层处理。
- 3.2.2.4（时间超时）
- 必须将 TIME_EXCEEDED 传递到传输层。（OK）
- 其他要求在 IP 层处理（生成 TIME_EXCEEDED）。
- 3.2.2.5（参数问题）
- 应生成这些（OK）
- 必须将收到的 PARAPPROBLEM 传递到传输层（尚未实现）
- [Solaris 2.X 在发生时似乎断言 EPROTO] —— AC
- 3.2.2.6（回声请求/回复）
- 必须响应 ECHO_REQUEST，并交给应用程序处理 ECHO 事情（OK. 可通过 sysctl 配置。）
- 必须向请求相同的源地址进行回复。（符合 ECHO 的（尚未实现））
- 必须将回复传递到传输/用户层。（OK）
- 3.2.2.7（信息请求）
- 必须实现此。（我猜意思是静默丢弃……？）（OK）
- 3.2.2.8（时间戳请求/回复）
- 可以实现（OK）
- 应在内核中处理以实现“最小变性”
- 应丢弃广播请求。（OK，请参见一致性问题）

# 基础设施协议 311

- 3.2.2.9（地址请求/回复）
- 可以实现（OK）
- 应在内核中处理以实现“最小变性”
- 应丢弃广播请求。（OK，请参见一致性问题）
- 必须向请求相同的源地址进行回复。（符合 ECHO 的（尚未实现））

