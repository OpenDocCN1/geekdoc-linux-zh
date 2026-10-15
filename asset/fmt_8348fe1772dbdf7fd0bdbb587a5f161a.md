
### 8. 获取单个曲目条目

下一个函数以与`get_cdc_entry`相同的方式实现，参数是目录指针和曲目号。

```c
cdt_entry get_cdt_entry(const char *catalog_ptr, const int track_no)
{
    cdt_entry entry_to_return;
    char entry_to_find[CAT_CAT_LEN + 10];
    datum local_data_datum;
    datum local_key_datum;

    memset(entry_to_return, '\0', sizeof(entry_to_return));

    if (!cdc_dbm_ptr || !cdt_dbm_ptr) return (entry_to_return);
    if (!catalog_ptr) return (entry_to_return);
    if (strlen(catalog_ptr) > CAT_CAT_LEN) return (entry_to_return);
    /* 设置搜索键，它是目录条目和曲目号的复合键 */
    memset(entry_to_find, '0', sizeof(entry_to_find));
    sprintf(entry_to_find, "%s %d", catalog_ptr, track_no);

    local_key_datum.dptr = (void *)entry_to_find;
    local_key_datum.dsize = sizeof(entry_to_find);

    memset(&local_data_datum, '\0', sizeof(local_data_datum));
    local_data_datum = dbm_fetch(cdt_dbm_ptr, local_key_datum);
    if (local_data_datum.dptr) {
        memcpy(&entry_to_return, (char *)local_data_datum.dptr,
            local_data_datum.dsize);
    }
    return (entry_to_return);
}
```

### 9. 添加新的目录条目

下一个函数`add_cdc_entry`添加一个新的目录条目：

```c
int add_cdc_entry(const cdc_entry *entry_to_add)
{
    char key_to_add[CAT_CAT_LEN + 1];
    datum local_data_datum;
    datum local_key_datum;
    int result;
}
```

# 第 7 章

```c
/* 检查已初始化且参数有效 */
if (!cdc_dbm_ptr || !cdt_dbm_ptr) return (0);
if (strlen(entry_to_add.catalog) >= CAT_CAT_LEN) return (0);

/* 确保搜索键只包含有效字符串和空字符 */
memset(&key_to_add, 0, sizeof(key_to_add));
strcpy(key_to_add, entry_to_add.catalog);

local_key_datum.dptr = (void *) key_to_add;
local_key_datum.dsize = sizeof(key_to_add);
local_data_datum.dptr = (void *) &key_to_add;
local_data_datum.dsize = sizeof(entry_to_add);

result = dbm_store(cdc_dbm_ptr, local_key_datum, local_data_datum, DBM_REPLACE);

/* dbm_store() 使用 0 表示成功 */
if (result == 0) return (1);
return (0);
```

### 10. 添加新的曲目条目

`add_cdt_entry`添加一个新的曲目条目。访问键是由目录字符串和曲目编号构成的复合键。

```c
int add_cdt_entry(const cdt_entry_to_add *)
{
    char key_to_add[CAT_CAT_LEN + 10];
    datum local_data_datum;
    datum local_key_datum;
    int result;

    if (!cdc_dbm_ptr || !cdt_dbm_ptr) return (0);
    if (strlen(entry_to_add.catalog) >= CAT_CAT_LEN) return (0);

    memset(&key_to_add, 0, sizeof(key_to_add));
    sprintf(key_to_add, "%s %d", entry_to_add.catalog, entry_to_add.track_no);

    local_key_datum.dptr = (void *) key_to_add;
    local_key_datum.dsize = sizeof(key_to_add);
    local_data_datum.dptr = (void *) &key_to_add;
    local_data_datum.dsize = sizeof(entry_to_add);

    result = dbm_store(cdt_dbm_ptr, local_key_datum, local_data_datum, DBM_REPLACE);

    /* dbm_store() 使用 0 表示成功，负数表示错误 */
    if (result == 0)
        return (1);
    return (0);
}
```

### 11. 删除目录条目

如果我们能添加内容，那么我们最好也能删除它们。这个函数用于删除目录条目：

```c
int del_cdc_entry(const char *cd_catalog_ptr)
{
    char key_to_del[CAT_CAT_LEN + 1];
    datum local_key_datum;
    int result;

    if (!cdc_dbm_ptr || !cdt_dbm_ptr) return (0);
    if (strlen(cd_catalog_ptr) >= CAT_CAT_LEN) return (0);

    memset(key_to_del, 0, sizeof(key_to_del));
    strncpy(key_to_del, cd_catalog_ptr, sizeof(key_to_del));

    local_key_datum.dptr = (void *)key_to_del;
    local_key_datum.dsize = sizeof(key_to_del);

    result = dbm_delete(cdc_dbm_ptr, local_key_datum);

    /* dbm_delete() 使用 0 表示成功 */
    if (result == 0) return (1);
    return (0);
}
```

### 12. 删除曲目条目

这里是删除曲目的对应函数。记住曲目键是目录条目和曲目编号的复合索引。

```c
int del_cdt_entry(const char *cd_catalog_ptr, int track_no)
{
    char key_to_del[CAT_CAT_LEN + 10];
    datum local_key_datum;
    int result;

    if (!cdc_dbm_ptr || !cdt_dbm_ptr) return (0);
    if (strlen(cd_catalog_ptr) >= CAT_CAT_LEN) return (0);

    memset(key_to_del, 0, sizeof(key_to_del));
    sprintf(key_to_del, "%s %d", cd_catalog_ptr, track_no);

    local_key_datum.dptr = (void *)key_to_del;
    local_key_datum.dsize = sizeof(key_to_del);

    result = dbm_delete(cdt_dbm_ptr, local_key_datum);

    /* dbm_delete() 使用 0 表示成功 */
    if (result == 0) return (1);
    return (0);
}
```

### 13. 搜索函数

最后，我们还有一个简单的搜索函数。它并不复杂，但演示了如何在预先不知道键的情况下扫描`dbm`条目。由于我们预先不知道有多少条目，因此我们实现的该函数每次调用只返回一个条目。如果没有找到，则条目将为空。为了扫描整个数据库，我们通过一个整数指针`first_call_ptr`调用该函数，在第一次调用时该值应为 1。在随后的调用中，变量为 0，函数将在找到上一个条目后继续搜索。当我们需要用不同的目录条目重新启动时，必须将`first_call_ptr`设置为真。在调用之间，函数维护着某些内部状态。这隐藏了继续搜索的复杂性。如果搜索指向空，则认为所有条目都匹配。

```c
cdc_entry search_cdc_entry(const char *cd_catalog_ptr, int *first_call_ptr)
{
    static int local_first_call = 1;
    cdc_entry entry_to_return;
    datum local_data_datum;
    static datum local_key_datum; /* 注意这里是 static */

    memset(&entry_to_return, 0, sizeof(entry_to_return));
```

### 14. 合法性检查

通常，我们首先进行合法性检查：

```c
if (!cdc_dbm_ptr || !cd_catalog_ptr || !first_call_ptr) return (entry_to_return);
if (strlen(cd_catalog_ptr) >= CAT_CAT_LEN) return (entry_to_return);
/* 防止传递空 first_call_ptr */
if (local_first_call) {
    local_first_call = 0;
    *first_call_ptr = 1;
}
```

### 15. 搜索逻辑

如果调用此函数时`first_call_ptr`设置为真，我们需要从数据库开头开始（或重启）搜索。如果`first_call_ptr`不是真，我们只需移动到数据库中的下一个键：

```c
if (*first_call_ptr) {
    *first_call_ptr = 0;
    local_key_datum = dbm_firstkey(cdc_dbm_ptr);
} else {
    local_key_datum = dbm_nextkey(cdc_dbm_ptr);
}
if (local_key_datum.dptr != NULL) {
    /* 找到了一个条目 */
    local_data_datum = dbm_fetch(cdc_dbm_ptr, local_key_datum);
    if (local_data_datum.dptr) {
        memcpy(&entry_to_return, (char *)local_data_datum.dptr, local_data_datum.dsize); /* ... */
    }
}
```

# 数据管理

### 16. 搜索检查

我们的搜索功能是一个非常简单的检查，用于查看搜索字符串是否出现在当前目录条目中。

```c
/* 检查搜索字符串是否出现在条目 */
if (!strstr(entry_to_return.catalog, cd_catalog_ptr)) {
    memset(&entry_to_return, 0, sizeof(entry_to_return));
    local_key_datum = dbm_nextkey(cdc_dbm_ptr);
}
while (local_key_datum.dptr && local_data_datum.catalog[0] == '\0') {
    return (entry_to_return);
}
/* search_cdc_entry / */
```

我们现在可以将一切与库整合在一起了。现在不需要太担心，因为我们在下一章将查看它是如何运行的。目前，请将其输入并保存为`Makefile`。

```makefile
all: application

INCLUDE=/usr/include/gdbm
LIBS=-gdbm
CFLAGS=

app_ui.o: app_ui.c cd_data.h
gcc $(CFLAGS) -c app_ui.c

access.o: access.c cd_data.h
gcc $(CFLAGS) -I$(INCLUDE) -c access.c

application: app_ui.o access.o
gcc $(CFLAGS) -o application app_ui.o access.o -l$(LIBS)
```

```makefile
clean:
rm -f application *.o

dbmfiles:
rm -f *.dir *.pag
```

记住，根据你的系统配置，可能需要替换`LIBS=`和`INCLUDE=`。

要编译新的`cd`，在提示符处输入：

```bash
$ make
```

如果一切顺利，应用程序将被编译并放在当前目录下。

## 总结

在本章中，我们学习了数据管理的三个方面。首先，我们学习了 Linux 内存系统以及它的使用方法，尽管需求分页虚拟内存的内部实现相当复杂。我们还发现它是如何保护操作系统和其他程序免受非法内存访问尝试的。

随后，我们研究了文件锁定如何允许多个程序协作访问数据。我们首先查看了一个简单的二进制信号量方案，然后查看了一个更复杂的情况，即对文件的不同部分进行共享或排斥锁定。接下来，我们查看了`dbm`库以及它使用非常灵活的索引安排存储和高效检索任意数据块的能力。

最后，我们重新设计并实现了示例 CD 数据库应用程序，使用`dbm`库作为其数据存储技术。

## 第 8 章

## 安装

无论你倾向于哪种 Linux 发行版，它可能都带有一个版本的`MySQL`。Slackware、Red Hat、SuSE 和 Debian 在其当前版本中包含了它。这将是快速启动并运行`MySQL`的简单方法。如果你的发行版没有提供`MySQL`软件包，或者你想获取最新版本，可以从 MySQL 网站`www.mysql.com`下载二进制包或源码包。

通常，你发行版的`MySQL`软件包将包含一些与`init.d`配合运行启动脚本。在其他情况下，你需要显式告诉`MySQL`你希望它自动启动。以 Red Hat 9 为例，在服务器设置（Server Settings）> 下，检查`mysql`服务是否已启动。（注意，只有在安装了软件包后，`MySQL`服务才会出现在此列表中。）

## 预编译程序包

如果由于某种原因，你需要下载`MySQL`而不是使用捆绑版本，RPM 提供了安装软件的最简单方法。RPM 包被拆分为不同数量的包，其中四个对本章非常重要：

- 主服务器包，名称如`MySQL-server-<version>.<architecture>.rpm`，包含预编译的二进制文件、手册页形式的文档以及一些用于国际化的支持文件。在编写此时，软件包 4.0.14 包含`MySQL-server-4.0.14.1386.rpm`。
- 客户端包，名称如`MySQL-client-<version>.<architecture>.rpm`。此包包含基础`MySQL`客户端，允许你以命令行方式实时与服务器进行交互，在保持静态连接打开的同时发布查询。还包含了其他几个快速访问`MySQL`的外围客户端。这些程序通常用于简化与维护`MySQL`服务器相关的平庸管理任务。
- 共享组件包，名称如`MySQL-shared-<version>.<architecture>.rpm`，包含某些外部组件使用的共享库。
- 开发包，名称类似于`MySQL-devel-<version>.<architecture>.rpm`。作为开发者，我们特别感兴趣其中包含用于开发与`MySQL`服务器通信的应用程序的额外头文件和库文件。

你可能还会看到可选“Max”和“Debug”包。Max 包包含额外功能，例如支持更多不常见的存储文件类型。对于本章而言，以及对于大多数开发或生产用途，你不需要 Max 包。Debug 包在编译时带有额外的调试代码和信息；除非进行低级调试，否则你不需要！不要在生产环境中使用 Debug 版本；额外的调试支持会导致性能下降。

为了开发`MySQL`应用程序，你应该在系统上安装所有这些包，可以使用 GUI 工具或直接使用`rpm`命令。通常情况下，只需将四个 RPM 文件下载到空目录，然后以超级用户身份执行以下命令：

```bash
rpm -i *.rpm
```

## MySQL
