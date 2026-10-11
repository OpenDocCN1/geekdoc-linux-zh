

### 21.2.12.2. rpmFreeSignature()—释放由 rpmReadPackageInfo() 读取的自由签名

此函数用于释放签名 h：

```c
#include <rpm/rpm-lib.h>
#include <rpm/header.h>

void rpmFreeSignature(Header h);
```

### 21.2.13. 头部操作

头部是 rpm-lib 中的关键数据结构之一。本节中的函数执行对头部的基本操作。

头部实际上是一种数据结构。不必完全理解其实际数据结构，但有必要了解头部所基于的基本概念。

头部充当一种微型数据库。可以搜索特定信息，然后轻松检索它们。与数据库一样，头部包含的信息大小各异。

#### 21.2.13.1. headerRead()—读取头部

此函数从文件 fd 中读取头部，将其从网络字节序转换为主机系统的字节序：

```c
#include <rpm/rpm-lib.h>
#include <rpm/header.h>

Header headerRead(int fd,
                  int magicp);
```

如果 `magicp` 被定义为 `HEADER_MAGIC_YES`，`headerRead()` 将期望头部存在魔数，如果不存在则返回错误。同样，如果 `magicp` 被定义为 `HEADER_MAGIC_NO`，`headerRead()` 将不检查头部的魔数，如果存在则返回错误。

出错时，此函数返回 **NULL**。

#### 21.2.13.2. headerWrite()—写入头部

此函数将头部 h 写入文件 fd，将其从主机字节序转换为网络字节序。如果 `magicp` 被定义为 `HEADER_MAGIC_YES`，`headerWrite()` 将为正在写入的头部添加适当的魔数。如果 `magicp` 被定义为 `HEADER_MAGIC_NO`，`headerWrite()` 将不包含魔数：

```c
#include <rpm/rpm-lib.h>
#include <rpm/header.h>

void headerWrite(int fd,
    Header h,
    int magicp);
```

#### 21.2.13.3. headerCopy()—复制头部

此函数返回头部 h 的副本：

```c
#include <rpm/rpmlib.h>
#include <rpm/header.h>

Header headerCopy(Header h);
```

#### 21.2.13.4. headerSizeof()—计算头部大小

此函数返回头部 h 在磁盘上占用的字节数。注意，在 RPM 2.3.3 之前的版本中，此函数还会更改头部中数据的位置。结果是，`headerGetEntry()` 返回的指针将不再有效。因此，在调用 `headerSizeof()` 之前获取的任何指针都应被丢弃：

```c
#include <rpm/rpmlib.h>
#include <rpm/header.h>

unsigned int headerSizeof(Header h,
    int magicp);
```

#### 21.2.13.5. headerNew()—创建新头部

此函数返回一个新的头部。

```c
#include <rpm/rpmlib.h>
#include <rpm/header.h>

Header headerNew(void);
```

#### 21.2.13.6. headerFree()—释放头部

此函数释放由 h 指定的头部：

```c
#include <rpm/rpmlib.h>
#include <rpm/header.h>

void headerFree(Header h);
```

#### 21.2.13.7. headerDump()—以人类可读形式打印头部结构

此函数将头部 h 的结构打印到文件 f。如果 flags 参数被定义为 HEADER_DUMP_INLINE，则还会打印头部的数据：

```c
#include <rpm/rpmlib.h>
#include <rpm/header.h>

void headerDump(Header h,
    FILE *f,
    int flags);
```

### 21.2.14. 头部条目操作

本节中的函数提供了操作头部条目所需的基本操作。当前定义的以下头部条目类型：

- `RPM_NULL_TYPE`—此类型未使用。
- `RPM_CHAR_TYPE`—条目包含单个字符。
- `RPM_INT8_TYPE`—条目包含一个 8 位整数。
- `RPM_INT16_TYPE`—条目包含一个 16 位整数。
- `RPM_INT32_TYPE`—条目包含一个 32 位整数。
- `RPM_INT64_TYPE`—条目包含一个 64 位整数。
- `RPM_STRING_TYPE`—条目包含一个空终止的字符串。
- `RPM_BIN_TYPE`—条目包含 rpmlib 不会解释的二进制数据。
- `RPM_STRING_ARRAY_TYPE`—条目包含一个空终止字符串的数组。

#### 21.2.14.1. headerGetEntry()—从头部获取条目

此函数从头部 h 中检索与 tag 匹配的条目：

```c
#include <rpmlib.h>
#include <rpm/header.h>

int headerGetEntry(Header h,
                    int_32 tag,
                    int_32 *type,
                    void **p,
                    int_32 *c);
```

条目的类型在 `type` 中返回，指向数据的指针在 `p` 中返回，数据的大小在 `c` 中返回。`type` 和 `c` 都可以是 `NULL`，在这种情况下该数据不会被返回。注意，如果条目类型是 `RPM_STRING_ARRAY_TYPE`，在使用完数据后必须对 `p` 执行 `free()`。

此函数成功时返回 1，失败时返回 0。

#### 21.2.14.2. headerAddEntry()—向头部添加条目

此函数向头部 h 添加一个新条目：

```c
#include <rpmlib.h>
#include <rpm/header.h>

int headerAddEntry(Header h,
                   int_32 tag,
                   int_32 type,
                   void *p,
                   int_32 c);
```

条目的标签由 tag 参数指定，条目的类型由 type 参数指定。

条目的数据由 p 指向，数据的大小由 c 指定。此函数始终返回 1。

> **注意**  
> 在 RPM 2.3.3 之前的版本中，headerAddEntry() 只能成功用于由 headerCopy() 和 headerNew() 产生的头部。特别是，当用于向由 headerRead() 产生的头部添加条目时，不支持 headerAddEntry()。后续版本的 RPM 解除了此限制。

#### 21.2.14.3. headerIsEntry()—确定条目是否在头部中

如果头部 h 中存在带有标签 tag 的条目，此函数返回 1。如果标签不存在，此函数返回 0：

```c
#include <rpm/rpmlib.h>
#include <rpm/header.h>

int headerIsEntry(Header h,
	int_32 tag);
```

### 21.2.15. 头部迭代器支持

迭代器用作逐步遍历整个头部每个条目的一种手段。本节中的函数用于创建、使用和释放迭代器。

#### 21.2.15.1. headerInitIterator()—创建迭代器

此函数为头部 h 返回一个新创建的迭代器：

```c
#include <rpm/rpmlib.h>
#include <rpm/header.h>

HeaderIterator headerInitIterator(Header h);
```

#### 21.2.15.2. headerNextIterator()—前进到下一个条目

此函数前进到在创建迭代器 iter 时指定的头部中的下一个条目（使用 headerInitIterator() 创建）：

```c
#include <rpm/rpmlib.h>
#include <rpm/header.h>

int headerNextIterator(HeaderIterator iter,
	int_32 *tag,
	int_32 *type,
	void **p,
	int_32 *c);
```

下一个条目的标签、类型、数据和大分别在 tag、type、p 和 c 中返回。注意，如果条目类型是 `RPM_STRING_ARRAY_TYPE`，在使用完数据后必须对 p 执行 free()。

此函数成功时返回 1，如果头部中没有更多条目则返回 0。

#### 21.2.15.3. headerFreeIterator()—释放迭代器

此函数释放迭代器 iter 使用的资源：

```c
#include <rpm/rpm-lib.h>
#include <rpm/header.h>

void headerFreeIterator(HeaderIterator iter);
```

## 21.3. 示例代码

在本节中，我们将研究使用 rpm-lib 执行各种常见必需操作的示例程序。我们将代码片段与连续的评论穿插在一起，以减少翻页。

### 21.3.1. 示例 #1

在此示例中，我们将使用 rpm-lib 的多个头部操作函数。

这里我们包含了 `rpm-lib.h`，这是所有使用 rpm-lib 的程序所必需的：

```c
#include <errno.h>
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>
#include <string.h>

#include <rpm/rpm-lib.h>
```

这里我们定义了程序的存储。特别注意 HeaderIterator、Header 和 int_32 数据类型：

```c
void main(int argc, char ** argv)
{
    HeaderIterator iter;
    Header h, sig;
    int_32 iterTag, type, count;
    void *p = NULL;
    char *blather;
    char * name;

    int fd, stat;
```

