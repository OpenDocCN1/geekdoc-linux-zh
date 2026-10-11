

## getprotoent(3)

#include <netdb.h>

```c
struct protoent *getprotoent(void);
void setprotoent(int stayopen);
void endprotoent(void);

struct protoent *getprotobyname(const char *name);
struct protoent *getprotobyname_r(const char *name, struct protoent *protoent, char *buffer, size_t buflen, struct protoent **result);
struct protoent *getprotobynumber(int proto);
```

### 标准 I/O 支持

#include <stdio.h>

```c
FILE *fdopen(int fildes, const char *mode);

int fileno(FILE *stream);

int setbuf(FILE *stream, char *buf);

int setlinebuf(FILE *stream);

int setvbuf(FILE *stream, char *buf, int mode, size_t size);
```

mode：
- _IOFBF 完全缓冲。
- _IOLBF 行缓冲。
- _IONBF 无缓冲。

### 主机名支持

**uname(2)**

#include <sys/utsname.h>

```c
int uname(struct utsname *buf);
```

**gethostname(2)**

#include <unistd.h>

```c
int gethostname(char *name, size_t len);
```

**getdomainname(2)**

#include <unistd.h>

```c
int getdomainname(char *name, size_t len);
```

**gethostbyname(3)**

#include <netdb.h>

```c
extern int h_errno;

void herror(const char *msg);

const char *hstrerror(int err);

struct hostent *gethostbyname(const char *name);
struct hostent *gethostbyaddr(const char *addr, int len, int type);
```

**sethostent(3)**

#include <netdb.h>

```c
void sethostent(int stayopen);
void endhostent(void);
```

## 套接字相关结构体参考

### 套接字地址结构体

**sockaddr**

#include <sys/socket.h>

```c
struct sockaddr {
    sa_family_t sa_family; /* 地址族 */
    char sa_data[14]; /* 地址数据。 */
};
```

**sockaddr_un**

#include <sys/un.h>

```c
struct sockaddr_un {
    sa_family_t sun_family; /* 地址族 */
    char sun_path[108]; /* 路径名 */
};
```

**sockaddr_in 和 in_addr**

#include <netinet/in.h>

```c
struct sockaddr_in {
    sa_family_t sin_family; /* 地址族 */
    uint16_t sin_port; /* 端口号 */
    struct in_addr sin_addr; /* 互联网地址 */
    unsigned char sin_zero[8]; /* 填充字节 */
};

struct in_addr {
    uint32_t s_addr; /* 互联网地址 */
};
```

### 特殊 IPv4 地址

```c
adr.sin_addr.s_addr = ntohl(INADDR_ANY);
adr.sin_addr.s_addr = ntohl(INADDR_LOOPBACK);
```

### sockaddr_x25 和 x25_address

```c
#include <linux/x25.h>

struct sockaddr_x25 {
    sa_family_t  sx25_family;  /* 必须为 AF_X25 */
    x25_address  sx25_addr;     /* X.121 地址 */
};

typedef struct {
    char  x25_addr[16];
} x25_address;
```

### sockaddr_in6 和 in6_addr

```c
struct sockaddr_in6 {
    sa_family_t  sin6_family;   /* AF_INET6 */
    uint16_t     sin6_port;     /* 端口号 */
    uint32_t     sin6_flowinfo; /* 流信息 */
    struct in6_addr sin6_addr;  /* IPv6 地址 */
};

struct in6_addr {
    union {
        uint8_t    u6_addr8[16];
        uint16_t   u6_addr16[8];
        uint32_t   u6_addr32[4];
    } in6_u;
};
```

### sockaddr_atalk 和 at_addr

```c
#include <netatalk/at.h>

struct sockaddr_atalk {
    sa_family_t  sat_family;
    u_char       sat_port;      /* 端口 */
    struct at_addr sat_addr;    /* 网络/节点 */
};

struct at_addr {
    u_short      s_net;
    u_char       s_node;
};
```

### full_sockaddr_ax25、sockaddr_ax25 和 ax25_address

```c
struct full_sockaddr_ax25 {
     struct sockaddr_ax25 fsa_ax25;
     ax25_address fsa_digipeater[AX25_MAX_DIGIS];
};

struct sockaddr_ax25 {
     sa_family_t     sax25_family;
     ax25_address    sax25_call;
     int             sax25_ndigis;
};

typedef struct {
     /* 6 位呼号 + SSID (移位 ascii) */
     char            ax25_call[7];
} ax25_address;

#define sax25_uid         sax25_ndigis
```

### 其他结构体

**servent**

```c
struct servent {
     char          *s_name;     /* 官方服务名称 */
     char         **s_aliases;  /* 别名列表 */
     int           s_port;      /* 端口号 */
     char         *s_proto;     /* 使用的协议 */
};
```

**protent**

```c
struct protent {
     char          *p_name;     /* 官方协议名称 */
     char         **p_aliases;  /* 别名列表 */
     int           p_proto;     /* 协议号 */
};
```

**utsname**

#include <sys/utsname.h>

```c
struct utsname {
    char sysname[SYS_NMLN];
    char nodename[SYS_NMLN];
    char release[SYS_NMLN];
    char version[SYS_NMLN];
    char machine[SYS_NMLN];
    char domainname[SYS_NMLN];
};
```

**hostent**

```c
struct hostent {
    char *h_name; /* 主机的官方名称 */
    char **h_aliases; /* 别名列表 */
    int h_addrtype; /* 主机地址类型 */
    int h_length; /* 地址长度 */
    char **h_addr_list; /* 地址列表 */
};

/* 为了向后兼容 */
#define h_addr h_addr_list[0]
```

**timeval**

```c
struct timeval {
    long tv_sec; /* 秒 */
    long tv_usec; /* 微秒 */
};
```

**linger**

```c
struct linger {
    int l_onoff;
    int l_linger;
};
```

### I/O 相关结构体

**iovec**

#include <sys/uio.h>

```c
struct iovec {
    ptr_t iov_base; /* 起始地址 */
    size_t iov_len; /* 以字节为单位的长度 */
};
```

**msghdr**

```c
struct msghdr {
    void *msg_name;
    socklen_t msg_namelen;
    struct iovec *msg_iov;
    size_t msg_iovlen;
    void *msg_control;
    size_t msg_controllen;
    int msg_flags;
};
```

**cmsghdr**

```c
struct cmsghdr {
    socklen_t cmsg_len;
    int cmsg_level;
    int cmsg_type;
    /* u_char cmsg_data[]; */
};
```

## 附录 C

## 有用的网络表格

**表 C.1：互联网地址类别**

| 类别 | 最低值 | 最高值 | 网络位 | 主机位 |
| :--- | :--- | :--- | :--- | :--- |
| A | 0.0.0.0 | 127.255.255.255 | 7 | 24 |
| B | 128.0.0.0 | 191.255.255.255 | 14 | 16 |
| C | 192.0.0.0 | 223.255.255.255 | 21 | 8 |
| D | 224.0.0.0 | 239.255.255.255 | 28 | N/A |
| E | 240.0.0.0* | 247.255.255.255 | 27 | N/A |

**表 C.2：按 IP 类别划分的子网掩码值**

| 类别 | 最低值 | 最高值 | 子网掩码 |
| :--- | :--- | :--- | :--- |
| A | 0.0.0.0 | 127.255.255.255 | 255.0.0.0 |
| B | 128.0.0.0 | 191.255.255.255 | 255.255.0.0 |
| C | 192.0.0.0 | 223.255.255.255 | 255.255.255.0 |

**表 C.3：私有 IP 地址分配**

| 类别 | 最低值 | 最高值 | 子网掩码 |
| :--- | :--- | :--- | :--- |
| A | 10.0.0.0 | 10.255.255.255 | 255.0.0.0 |
| B | 172.16.0.0 | 172.31.255.255 | 255.255.0.0 |
| C | 192.168.0.0 | 192.168.255.255 | 255.255.255.0 |

**表 C.4：业余无线电保留 IP 地址**

| 类别 | 最低值 | 最高值 | 子网掩码 |
| :--- | :--- | :--- | :--- |
| A | 44.0.0.0 | 44.255.255.255 | 255.0.0.0 |

**表 C.5：/proc/sys/net/ipv4/tcp_stdurg 设置**

| **值** | **解释** |
|:---:|:---|
| 0 | BSD 解释方式（Linux 默认） |
| 1 | RFC793 解释方式 |

**表 C.6：/etc/inetd.conf 配置记录**

| **字段号** | **描述** | **示例** |
|:---:|:---:|:---:|
| 1 | 互联网服务名称 | telnet（这也可能是一个端口号） |
| 2 | 套接字类型 | stream 或 dgram |
| 3 | 协议 | tcp 或 udp |
| 4 | 标志 | nowait 或 wait |
| 5 | 要使用的 UserID | root 或 nobody |
| 6 | 可执行文件的路径名 | /usr/sbin/in.telnetd |
| 7 | 服务器参数 | in.telnetd |

## 术语表

**地址族 (address family)**：用于特定网络协议的一组可接受的地址格式。

**辅助数据 (ancillary data)**：随数据包中的正常数据一起发送或接收的控制数据。辅助数据通常包括通过 `PF_LOCAL`/`PF_UNIX` 套接字传输的用户凭据或文件描述符。

**API**：应用程序编程接口。

**ARPA**：高级研究计划局。

**辅助数据 (auxiliary data)**：辅助数据的另一个名称。

**AX.25**：CCITT X.25 网络协议的业余无线电适配版本，用于数字无线电传输。另请参阅 *X.25*。

**大端 (big-endian)**：端序特性描述了特定数字硬件的字节顺序。大端意味着最高有效字节在物理排列中位于最前。

**BPQ**：在本书中，BPQ 指以太网上的 AX.25 支持，由 John Wiseman（无线电呼号 G8BPQ）开发。

**规范主机名 (canonical hostname)**：网络上的主机可以通过几个不同的名称来标识。然而，每个主机必须有一个官方主机名。所有其他主机名都被视为规范主机名的别名。

**CCITT**：国际电报电话咨询委员会的缩写，这是一个标准化机构。这现在已经并入 ITU-T（国际电信联盟）标准化机构。

**面向连接的协议 (connection-oriented protocol)**：一种要求建立通信通道的协议。只有在建立连接之后才能进行通信。这种通信形式就像打电话，必须先联系到对方才能开始对话。

**无连接协议 (connectionless protocol)**：一种无需预先建立连接的协议。这种协议形式就像邮寄信件；信息被发送，期望它们到达指定的目的地。

