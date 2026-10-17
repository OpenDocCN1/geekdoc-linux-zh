
#include <netinet/in.h>

#include <arpa/inet.h>

int inet_aton(const char *cp, struct in *inp);

unsigned long inet_addr(const char *cp);

unsigned int inet_network(const char *cp);

char *inet_ntoa(struct in_addr in);

struct in_addr inet_makeaddr(int in);

unsigned long inet_netof(struct in_addr in);

```
## 描述

`inet_aton()` 将标准点格式的 Internet 地址转换为二进制数据并存储在 `inp` 指向的结构中。如果有效则返回非零，否则返回 0。

`inet_addr()` 将点格式的 Internet 主机转换为网络字节序的二进制数据。如果无效则返回 -1。它是 `inet_aton()` 的过期接口；因为 -1 是有效地址（255.255.255.255）。

`inet_network()` 从点格式地址中提取网络字节序的网络号。如果无效则返回 -1。

`inet_ntoa()` 将网络字节序的 Internet 主机转换为标准点格式字符串。字符串返回在静态分配的缓冲区中，后续调用将覆盖它。

`inet_makeaddr()` 通过组合以主机字节序的网络号和本地主机名，创建一个网络字节序的 Internet 地址。

`inet_netof()` 返回 Internet 地址的网络号部分。网络号以主机字节序返回。

```
struct in_addr

as used in inet_aton(), inet_makeaddr(), inet_ntoa(), and inet_netof() is defined in netinet/in.h as

struct in_addr {

    unsigned long s_addr;

}
```

注意在 i80x86 上主机字节序是低位在前，而互联网上使用的网络字节序是大位在前。

## 符合

BSD 4.3

## 参见

gethostname(3), gettonet(3), hosts(5), networks(5)

> BSD, 1995年9月3日

## infnan

infnan—处理无限或非数字 (NaN)结果

## 概要

```c
#include <math.h>

double infnan(int error);
```

## 描述

ifnan() 函数为无穷和非数字（NaN）结果返回适当的值。错误值可以是 ERANGE 来表示无穷，或任何其他值来表示 NaN。同时会设置 errno。

# 返回值

如果错误为 ERANGE（无穷大），则返回 HUGE_VAL。

如果错误为 -ERANGE（负无穷），则返回 -HUGE_VAL。

如果错误为其他任何值，则返回 NaN。

# 错误

- ERANGE 错误值为正无穷或负无穷。
- EDOM 错误值为非数字（NaN)。

# 遵循

BSD 4.3

# ## initgroups

initgroups—初始化附加组访问列表

# 语法概要

```
#include <grp.h>
#include <sys/types.h>

initgroups(const char *user, gid_t group);
```

## 描述

initgroups() 通过读取组数据库 `/etc/group` 并使用用户所属的所有组来初始化组访问列表。额外的组 `group` 也会添加到列表中。

# 返回值

initgroups() 成功时返回 0，发生错误时返回 -1。

# 错误

- EPERM 调用进程没有足够的权限。
- ENOMEM 内存不足无法分配组信息结构。

# 文件

`/etc/group`: 组数据库文件

# 遵循

SVID 3, BSD 4.3

## 参见

getgroups(2), setgroups(2), ctlind(8), innd(8), libinn(3).

# isalnum, isalpha, isascii, isblank, iscntrl, isdigit, isgraph, islower, isprint, ispunct, isspace, isupper, isxdigit

# ## insque, remque

insque, remque—从队列中插入/移除项

# 语法概要

```
#include <stdlib.h>

void insque(struct qlem * elem, struct qlem * prev);
void remque(struct qlem *elem);
```

## 描述

insque() 和 remque() 是用于操作双向链表值的函数。列表中的每个元素都是 struct qlem 类型。

qlem 结构体定义如下

```
struct qlem {
struct qlem *q_fore;
struct qlem *q_back;
char *q_data[];
};
```

insque() 将 elem 指向的元素插入到 prev 指向的元素之后，prev 不能为 NULL。
remque() 从双向链表中移除 elem 指向的元素。

# 遵循

SVR4

## 缺陷

q_data 字段被定义为 char * 类型，在 Solaris 2.x 下，它似乎完全不存在。
在多个 UNIX 版本中，这些函数原型所在的位置不相同。某些系统将它们放在 `<search.h>` 中，另一些放在 `<string.h>` 中。Linux 将它们放在 `<stdlib.h>` 中，因为看起来最合理。
某些 UNIX 版本（如 HP-UX 10.x）没有定义 struct qlem，而是让 insque() 和 remque() 的参数类型为 void。

GNU, 1996年10月30日

# ## isalnum, isalpha, isascii, isblank, iscntrl, isdigit, isgraph, islower, isprint, ispunct, isspace, isupper, isxdigit

isalnum, isalpha, isascii, isblank, iscntrl, isdigit, isgraph, islower, isprint, ispunct, isspace, isupper, isxdigit—字符分类例程

# 语法概要

```
#include <ctype.h>

int isalnum (int c);
int isalpha (int c);
int isascii (int c);
int isblank (int c);
int iscntrl (int c);
int isdigit (int c);
int isgraph (int c);
int islower (int c);
int isprint (int c);
int ispunct (int c);
```

# 第三部分：库函数

```
int isspace (int c);
int isupper (int c);
int isdigit (int c);
```
