
## `getprotoent(3)`

`#include <netdb.h>`

```c
struct protoent *getprotoent(void);
void setprotoent(int stayopen);
void endprotoent(void);

struct protoent *getprotobyname(const char *name);
struct protoent *getprotobyname_r(const char *name, struct protoent *protoent, char *buffer, size_t buflen, struct protoent **result);
struct protoent *getprotobynumber(int proto);
```

### 标准 I/O 支持

`#include <stdio.h>`

```c
FILE *fdopen(int fildes, const char *mode);

int fileno(FILE *stream);

int setbuf(FILE *stream, char *buf);

int setlinebuf(FILE *stream);

int setvbuf(FILE *stream, char *buf, int mode, size_t size);
```

`mode`：

- `_IOFBF` 完全缓冲。
- `_IOLBF` 行缓冲。
- `_IONBF` 无缓冲。

### 主机名支持

`uname(2)`

`#include <sys/utsname.h>`

```c
int uname(struct utsname *buf);
```

`gethostname(2)`

`#include <unistd.h>`

```c
int gethostname(char *name, size_t len);
```

`getdomainname(2)`

`#include <unistd.h>`

```c
int getdomainname(char *name, size_t len);
```

`gethostbyname(3)`

`#include <netdb.h>`

```c
extern int h_errno;

void herror(const char *msg);

const char *hstrerror(int err);

struct hostent *gethostbyname(const char *name);
struct hostent *gethostbyaddr(const char *addr, int len, int type);
```

`sethostent(3)`

`#include <netdb.h>`

```c
void sethostent(int stayopen);
void endhostent(void);
```

## 套接字相关结构体参考

### 套接字地址结构体

`sockaddr`

`#include <sys/socket.h>`

```c
struct sockaddr {
    sa_family_t sa_family; /* 地址族 */
    char sa_data[14]; /* 地址数据。 */
};
```

`sockaddr_un`

`#include <sys/un.h>`

```c
struct sockaddr_un {
    sa_family_t sun_family; /* 地址族 */
    char sun_path[108]; /* 路径名 */
};
```

`sockaddr_in` 和 `in_addr`

`#include <netinet/in.h>`

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

### `sockaddr_x25` 和 `x25_address`

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

### `sockaddr_in6` 和 `in6_addr`

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

### `sockaddr_atalk` 和 `at_addr`

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

### `full_sockaddr_ax25`、`sockaddr_ax25` 和 `ax25_address`

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

`servent`

```c
struct servent {
     char          *s_name;     /* 官方服务名称 */
     char         **s_aliases;  /* 别名列表 */
     int           s_port;      /* 端口号 */
     char         *s_proto;     /* 使用的协议 */
};
```

`protent`
