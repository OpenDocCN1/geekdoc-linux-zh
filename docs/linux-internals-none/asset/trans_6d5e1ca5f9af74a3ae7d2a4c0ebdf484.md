

```c
180 {
181     return (set->sig[0] & mask) != 0;
182 }
183
184 extern inline void siginitset(sigset_t *set, unsigned long mask)
185 {
186     set->sig[0] = mask;
187     switch (_NSIG_WORDS) {
188         default:
189             memset(&set->sig[1], 0, sizeof(long)*(_NSIG_WORDS-1));
190             break;
191         case 2: set->sig[1] = 0;
192         case 1:
193     }
194 }
195
196 extern inline void siginitsetinv(sigset_t *set, unsigned long mask)
197 {
198     set->sig[0] = ~mask;
199     switch (_NSIG_WORDS) {
200         default:
201             memset(&set->sig[1], -1, sizeof(long)*(_NSIG_WORDS-1));
202             break;
203         case 2: set->sig[1] = -1;
204         case 1:
205     }
206 }
207
208 #endif /* __HAVE_ARCH_SIG_SETOPS */
209
210 #endif /* __KERNEL__ */
211
212 #endif /* _LINUX_SIGNAL_H */
```

## 数据结构—include/linux/kernel.h

```c
 1 #ifdef _LINUX_KERNEL_H
 2 #define _LINUX_KERNEL_H
 3
 4 /*
 5  * 'kernel.h' contains some often-used function prototypes etc
 6  */
 7
 8 #ifdef __KERNEL__
 9
10 #include <stdarg.h>
11 #include <linux/linkage.h>
12
13 /* Optimization barrier */
14 /* The "volatile" is due to gcc bugs */
15 #define barrier() __asm__ __volatile__("" : : "memory")
16
17 #define INT_MAX ((int) (~0u>>1))
18 #define UINT_MAX (~0U)
19 #define LONG_MAX ((long) (~0UL>>1))
20 #define ULONG_MAX (~0UL)
21
22 #define STACK_MAGIC 0xdeadbeef
23
24 #define ARRAY_SIZE(x) (sizeof(x) / sizeof((x)[0]))
25
26 #define KERN_EMERG "<0>" /* system is unusable */
27 #define KERN_ALERT "<1>" /* action must be taken immediately */
28 #define KERN_CRIT "<2>" /* critical conditions */
29 #define KERN_ERR "<3>" /* error conditions */
30 #define KERN_WARNING "<4>" /* warning conditions */
31 #define KERN_NOTICE "<5>" /* normal but significant condition */
32 #define KERN_INFO "<6>" /* informational */
33 #define KERN_DEBUG "<7>" /* debug-level messages */
34
35 #define NORET_TYPE /**/
36 #define ATTRIB_NORET __attribute__((noreturn))
37 #define NORET_AND noreturn,
38
39 #ifdef __i386__
40 #define FASTCALL(x) x __attribute__((regparm(3)))
41 #else
42 #define FASTCALL(x) x
43 #endif
44
45 extern void math_error(void);
46 extern struct notifier_block *panic_notifier_list;
47 NORET_TYPE void panic(const char * fmt, ...)
48 __attribute__ ((NORET_AND format (printf, 1, 2)));
49 NORET_TYPE void do_exit(long error_code)
50 ATTRIB_NORET;
51 extern unsigned long simple_strtoul(const char *,char ** ,unsigned int);
52 extern long simple_strtol(const char *,char ** ,unsigned int);
53 extern int sprintf(char * buf, const char * fmt, ...);
54 extern int vsprintf(char *buf, const char * fmt, va_list);
55 extern int get_option(char **str, int *pint);
56 extern char *get_options(char *str, int nints, int *ints);
57
58 extern int session_of_pgrp(int pgrp);
59
60 asmlinkage int printk(const char * fmt, ...)
61 __attribute__ ((format (printf, 1, 2)));
62
63 #if DEBUG
64 #define pr_debug(fmt,arg...) \
65 	printk(KERN_DEBUG fmt,##arg)
66 #else
67 #define pr_debug(fmt,arg...)
68 	do { } while (0)
69 #endif
70
71 #define pr_info(fmt,arg...) \
72 	printk(KERN_INFO fmt,##arg)
73
74 /*
75  *      Display an IP address in readable format.
76  */
77
78 #define NIPQUAD(addr) \
79 	((unsigned char *) &addr)[0], \
80 	((unsigned char *) &addr)[1], \
81 	((unsigned char *) &addr)[2], \
82 	((unsigned char *) &addr)[3]
83
84 #endif /* __KERNEL__ */
85
86 #define SI_LOAD_SHIFT   16
87 struct sysinfo {
88 	long uptime;                  /* Seconds since boot */
89 	unsigned long loads[3];       /* 1, 5, and 15 minute load averages */
90 	unsigned long totalram;       /* Total usable main memory size */
91 	unsigned long freeram;        /* Available memory size */
92 	unsigned long sharedram;      /* Amount of shared memory */
93 	unsigned long bufferram;      /* Memory used by buffers */
94 	unsigned long totalswap;      /* Total swap space size */
95 	unsigned long freeswap;       /* swap space still available */
96 	unsigned short procs;         /* Number of current processes */
97 	unsigned long totalhigh;      /* Total high memory size */
98 	unsigned long freehigh;       /* Available high memory size */
99 	unsigned int mem_unit;        /* Memory unit size in bytes */
100 	char _f[20-2*sizeof(long)-sizeof(int)]; /* Padding: libc5 uses this.. */
101 };
102
103 #endif
```

# 信号处理

## 第 8 章

## kHTTPd

kHTTPd 是一个 HTTP 守护进程，也是 Linux 的 Web 服务器。kHTTPd 与其他 Web 服务器的不同之处在于它作为模块（设备驱动程序）在 Linux 内核内部运行。

kHTTPd 仅处理*静态*（基于文件）的 Web 页面，并将所有对非静态信息的请求传递给常规用户空间的 Web 服务器，例如 Apache 或 Zeus。静态 Web 页面虽然服务起来并不复杂，但仍然非常重要。这是因为几乎所有图像都是静态的，很大一部分 HTML 页面也是静态的。“常规”Web 服务器对静态页面几乎没有额外价值；它仅仅是一个“将文件复制到网络”的操作。Linux 内核非常擅长这一点——例如，网络文件系统（NFS）守护进程也在内核中运行。

在内核中*加速*提供静态页面的简单情况，可以让用户空间守护进程专注于它们非常擅长的任务：生成用户特定的动态内容。像 Apache 这样的用户空间 Web 服务器通常加载了许多功能并拥有大量的执行路径，因此无法像 kHTTPd 那样快速。然而，有一些 Web 服务器与 kHTTPd 一样简单，但实现于用户空间，即使与 kHTTPd 相比，它们也不是处理器周期的昂贵消耗者。

kHTTPd 非常简单；它不处理动态内容。因此，它将你对那些通过名为 *dynamic* 的 *sysctl* 配置目录的所有请求代理到一个功能完整的用户空间 Web 服务器，例如 Apache。

出于这个原因，kHTTPd 仅对静态页面更快。动态页面在 kHTTPd Web 服务器下会产生稍多的延迟，因为它们需要转发到像 Apache 这样的另一个 Web 服务器。但这是一个全局性的胜利，因为常见 Web 服务器的大部分传输都是图像，这些绝对是静态的。

从原理上讲，kHTTPd 实际上与普通的 HTTP 守护进程没有太大区别。主要区别在于它绕过了系统调用层。通常你有这样的代码：

```
socket(..)
bind(..)
listen(..)
accept(..)
```

每个调用都必须进入内核，根据传入的参数查找内核结构，将信息返回到用户空间，等等。

kHTTPd 直接运行此类系统调用的内部逻辑，因为它本身是一个内核守护进程，直接接口于涉及的相关内部内核结构，并完全避免了用户空间与内核之间的交互。同样，因为它是内核守护进程，它避免了 switch_mm 和 TLB 刷新。最后但同样重要的是，它避免了所有的进入和退出内核开销。

kHTTPd 的数据结构并不多。它们位于 net/kHTTPd/structure.h 中。第一个是每个连接的结构。第二个是每个 kHTTPd 线程的结构，通过它可以排队许多 http_requests：

```c
struct http_request
{
    /* Linked list */
    struct http_request *Next;

    /* Network and File data */
    struct socket *sock;
    struct file *filp;

    /* Raw data about the file */
    int FileLength; /* File length in bytes */
    int Time; /* mtime of the file, unix format */
    int BytesSent; /* The number of bytes already sent */
    int IsForUser space; /* 1 means let User space handle this one */

    /* Wait queue */
    wait_queue_t sleep; /* For putting in the socket’s waitqueue */

    /* HTTP request information */
    char FileName[256]; /* The requested filename */
    int FileNameLength; /* The length of the string representing the filename */
    char Agent[128]; /* The agent-string of the remote browser */
    char IMS[128]; /* If-modified-since time, rfc string format */
    char Host[128]; /* Value given by the Host: header */
    int HTTPVER; /* HTTP-version; 9 for 0.9, 10 for 1.0 and above */

    /* Derived date from the above fields */
    int IMS_Time; /* if-modified-since time, unix format */
    char TimeS[64]; /* File mtime, rfc string representation */
    char LengthS[14]; /* File length, string representation */
    char *MimeType; /* Pointer to a string with the mime-type based on the filename */
    __kernel_size_t MimeLength; /* The length of this string */
};

/*
```

