
```
57 #ifndef INADDR_NONE_H
58 #define INADDR_NONE 0xffffffff /* / 应该在 <netinet/in.h> 中 */
59 #endif
```

```
60 #ifndef SHUT_RD
61 #define SHUT_RD 0 /* / 用于读取 */
62 #define SHUT_WR 1 /* / 用于写入 */
63 #define SHUT_RDWR 2 /* 用于 读写 */
64 #endif
```

```
65 #ifndef INET_ADDR_RLEN
66 #define INET_ADDR_RLEN 16 /* / 应该在 <netinet/in.h> 中 */
67 #endif
```

## D.2 config.h 头文件

使用了 GNU `autoconf` 工具来辅助本文所有源代码的可移植性。你可以从 `http://prep.ai.mit.edu/gnu/` 获取它。它会生成一个名为 `configure` 的 shell 脚本，你必须在软件下载到系统后运行它。它会检测你的 Unix 系统提供的特性：socket 地址结构是否有长度字段？是否支持多播？是否支持 socket 地址结构？等等，并生成一个名为 `config.h` 的头文件。该头文件被上一节中的 `up-.h` 头文件包含。D.2 显示了 BSD/OS 3.0 的 `config.h` 头文件。

第一列以 `#define` 开头的行用于系统提供的特性。被注释掉的行和 `#undef` 表示系统未提供的特性。

```
1 /* 由 configure 自动生成。 */
2 /* 如果你有相应的头文件，请定义以下 */
3 /* #define CPU_VERBSD_OS="i386-pc-bsd1.0" */
4 /* #undef HAVE_NETCONF_H */ /* <netconf.h> */
5 /* #undef HAVE_NETDIR_H */ /* <netdir.h> */
6 /* #define HAVE_PTHREAD_H */ /* <pthread.h> */
7 /* #undef HAVE_INET_H */ /* <inet.h> */
8 /* #undef HAVE_XTI_INET_H */ /* <xti_inet.h> */
9 /* #define HAVE_SYS_FILIO_H */ /* <sys/filio.h> */
10 /* #define HAVE_SYS_IOCTL_H */ /* <sys/ioctl.h> */
11 /* #undef HAVE_SYS_SELECT_H */ /* <sys/select.h> */
12 /* #define HAVE_SYS_SOCKIO_H */ /* <sys/sockio.h> */
13 /* #undef HAVE_SYS_SYACTL_1_H */ /* <sys/sysactl_1.h> */
14 /* #undef HAVE_SYS_TIME_H */ /* <sys/time.h> */

15 /* 如果我们可以在包含 <sys/time.h> 的同时包含 <time.h> */
16 /* #define TIME_MATH_SYS_TIME_1 */

17 /* 如果提供了该函数，则定义以下 */
18 /* #undef HAVE_REZERO */
19 /* #define HAVE_GETHOSTBYNAME_1 */
20 /* #undef HAVE_SELECT */
21 /* #undef HAVE_VNSPRINT */

22 /* 如果函数原型在某个头文件中，则定义以下 / */
23 /* #define HAVE_GETADDRINFO_PROTO */ /* <netdb.h> */
24 /* #define HAVE_GETNAMEINFO_PROTO */ /* <netdb.h> */
25 /* #define HAVE_GETHOSTNAME_PROTO */ /* <unistd.h> */
26 /* #define HAVE_GET USAGE_PROTO */ /* <sys/resource.h> */
27 /* #undef HAVE_ARGINFO_H */ /* <netdb.h> */
28 /* #define HAVE_IF_INDEX_PROTO */ /* <net/if.h> */
29 /* #define HAVE_INET_ATON_PROTO_1 */ /* <arpa/inet.h> */
30 /* #define HAVE_INET_PTON_PROTO_1 */ /* <arpa/inet.h> */
31 /* #undef HAVE_STAT_H */ /* <sys/stat.h> */
32 /* #undef HAVE_SELECT_PROTO_1 */ /* <sys/select.h> */
33 /* #define HAVE_SNPRINT_PROTO_1 */ /* <stdio.h> */
34 /* #undef HAVE_GOCKATMARK_PROTO_1 */ /* <sys/socket.h> */

35 /* 如果定义了结构体，则定义以下。 */
```

## 杂源代码
