
```c
#include <rpmlib.h>
#include <rpm/header.h>

int headerAddEntry(Header h,
                   int_32 tag,
                   int_32 type,
                   void *p,
                   int_32 c);
```

条目的标签由 `tag` 参数指定，条目的类型由 `type` 参数指定。

条目的数据由 `p` 指向，数据的大小由 `c` 指定。此函数始终返回 `1`。

> **注意**
>
> 在 RPM 2.3.3 之前的版本中，`headerAddEntry()` 只能成功用于由 `headerCopy()` 和 `headerNew()` 产生的头部。特别是，当用于向由 `headerRead()` 产生的头部添加条目时，不支持 `headerAddEntry()`。后续版本的 RPM 解除了此限制。

### 21.2.14.3. `headerIsEntry()`—确定条目是否在头部中

如果头部 `h` 中存在带有标签 `tag` 的条目，此函数返回 `1`。如果标签不存在，此函数返回 `0`：

```c
#include <rpm/rpmlib.h>
#include <rpm/header.h>

int headerIsEntry(Header h,
	int_32 tag);
```

### 21.2.15. 头部迭代器支持

迭代器用作逐步遍历整个头部每个条目的一种手段。本节中的函数用于创建、使用和释放迭代器。

#### 21.2.15.1. `headerInitIterator()`—创建迭代器

此函数为头部 `h` 返回一个新创建的迭代器：

```c
#include <rpm/rpmlib.h>
#include <rpm/header.h>

HeaderIterator headerInitIterator(Header h);
```

#### 21.2.15.2. `headerNextIterator()`—前进到下一个条目

此函数前进到在创建迭代器 `iter` 时指定的头部中的下一个条目（使用 `headerInitIterator()` 创建）：

```c
#include <rpm/rpmlib.h>
#include <rpm/header.h>

int headerNextIterator(HeaderIterator iter,
	int_32 *tag,
	int_32 *type,
	void **p,
	int_32 *c);
```

下一个条目的标签、类型、数据和大分别在 `tag`、`type`、`p` 和 `c` 中返回。注意，如果条目类型是 `RPM_STRING_ARRAY_TYPE`，在使用完数据后必须对 `p` 执行 `free()`。

此函数成功时返回 `1`，如果头部中没有更多条目则返回 `0`。

#### 21.2.15.3. `headerFreeIterator()`—释放迭代器

此函数释放迭代器 `iter` 使用的资源：

```c
#include <rpm/rpm-lib.h>
#include <rpm/header.h>

void headerFreeIterator(HeaderIterator iter);
```

### 21.3. 示例代码

在本节中，我们将研究使用 `rpm-lib` 执行各种常见必需操作的示例程序。我们将代码片段与连续的评论穿插在一起，以减少翻页。

#### 21.3.1. 示例 #1

在此示例中，我们将使用 `rpm-lib` 的多个头部操作函数。

这里我们包含了 `rpm-lib.h`，这是所有使用 `rpm-lib` 的程序所必需的：

```c
#include <errno.h>
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>
#include <string.h>

#include <rpm/rpm-lib.h>
```

这里我们定义了程序的存储。特别注意 `HeaderIterator`、`Header` 和 `int_32` 数据类型：

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

这部分代码很常规。第一个参数应该是一个 RPM 软件包文件，这里将其打开。如果命令行中没有参数，程序将改用标准输入（stdIn）：

```c
if (argc == 1) {
    fd = 0;
} else {
    fd = open(argv[1], O_RDONLY, 0644);
}

if (fd < 0) {
    perror("open");
    exit(1);
}
```

到这里事情开始变得有趣了！签名和头文件从刚刚打开的软件包文件中读取。注意在前面的代码中，我们将 `sig` 和 `h` 定义为 `header` 类型。这意味着我们可以对它们使用 rpmlib 中与此类相关的函数。经过少量的错误检查后，是时候继续往下走了……

```c
stat = rpmReadPackageInfo(fd, &sig, &h);
if (stat) {
    fprintf(stderr,
        "rpmReadPackageInfo error status: %d\n%s\n",
        stat, strerror(errno));
    exit(stat);
}
```

现在我们已经获取了软件包的头部信息，接下来获取软件包名称（由调用 `headerGetEntry` 时的 `RPMTAG_NAME` 指定）。然后，我们检查该软件包是否有预安装（`RPMTAG_PREIN`）或后安装（`RPMTAG_POSTIN`）脚本。如果有，我们就打印一条消息，并附上软件包名称：

```c
headerGetEntry(h, RPMTAG_NAME, &type, (void **) &name, &count);

if (headerIsEntry(h, RPMTAG_PREIN)) {
    printf("There is a preinstall script for %s\n", name);
}

if (headerIsEntry(h, RPMTAG_POSTIN)) {
    printf("There is a postinstall script for %s\n", name);
}
```

转到我们读取的另一个 Header 结构，以人类可读的形式打印软件包的签名。完成后，我们释放签名块：

```c
printf("Dumping signatures...\n");
headerDump(sig, stdout, 1);

rpmFreeSignature(sig);
```

我们现在为软件包的头部设置一个迭代器。这将允许我们遍历头部中的每个条目：

```c
printf("Iterating through the header...\n");

iter = headerInitIterator(h);
```

这个循环使用 `headerNextIterator()` 返回每个条目的标签、类型、数据和大小的值。通过对标签使用 switch 语句，我们可以对头部中每种类型的条目执行不同的操作：

```c
while (headerNextIterator(iter, &iterTag, &type, p, &count)) {
    switch (iterTag) {
    case RPMTAG_SUMMARY:
        blather = p;
        printf("The Summary: %s\n", blather);
        break;
    case RPMTAG_FILENAMES:
        printf("There are %d files in this package\n", count);
        break;
    }
}
```

这是程序的清理部分。首先释放我们一直使用的迭代器，最后释放头部本身：

```c
headerFreeIterator(iter);
headerFree(h);
}
```

在软件包上运行此程序会给出以下输出：
