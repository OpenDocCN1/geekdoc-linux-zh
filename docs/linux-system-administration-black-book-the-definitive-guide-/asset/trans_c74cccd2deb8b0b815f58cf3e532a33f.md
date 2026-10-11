

# squid.conf 文件

Squid 的配置文件是 squid.conf。在某些发行版中，你可以在 /etc/squid.conf 找到此文件，但在 Red Hat 中，它位于 /etc/squid/squid.conf。这个文件注释非常详尽，因此在此进行详细描述将是冗余的。该文件以长篇解释和已注释掉的命令排列。每个命令默认设置为解释末尾示例中列出的默认值，除非你取消注释并更改其值。

与其对 squid.conf 文件进行详细描述，本章接下来的部分将讨论设置 Squid 以提供你所需服务的各种方法。

## 14. Squid 互联网对象缓存

### 即时解决方案

### 安装 Squid

要安装 Squid 服务器，请执行以下操作：

1. 以 root 身份登录到你要运行 Squid 的机器。
2. 将 Red Hat CD-ROM 插入 CD-ROM 驱动器。
3. 输入 `mount /mnt/cdrom` 将 CD-ROM 挂载到文件系统。
4. 输入 `cd /mnt/cdrom/RedHat/RPMS` 切换到包含 CD-ROM 上 RPM 包的目录。
5. 输入 `rpm -ivh squid`，按 Tab 键展开文件名，然后按 Enter 键安装 RPM。

### 配置 Squid

安装后，要配置你的 Squid 服务器，请执行以下操作：

1. 以 root 身份登录到你安装了 Squid 的机器。
2. 输入 `vi /etc/squid/squid.conf` 打开 Squid 配置文件进行编辑。
3. 将光标向下移动至：
   ```
   #http_port 3128
   ```
4. 执行以下操作之一：
   - 保留该命令为注释状态。如果你这样做，Squid 将保持默认设置，即监听端口 3128。
   - 取消注释该命令并在默认值后添加额外的端口。
   - 取消注释该命令并将端口更改为其他完全不同的值。

> *提示：* 在将端口号添加到任何服务器的配置文件时，务必检查 /etc/services 以确保这些端口未被其他服务所需。另外，注意不要选择 1024 以下的端口，因为通常这些端口是保留给其他服务使用的。即使你没有将这些端口用于其标准用途，其他机器也可能在该端口上查询那些标准服务。

5. 将光标向下移动至：
   `#icp_port 3130`
6. 如果你想更改 Squid 监听 ICP 请求的默认端口，取消注释该行并更改值。
7. 继续向下移动至：
   `#http_port 4827`
8. 如果你想更改 Squid 监听 HTTP 查询的默认端口，取消注释该行并更改值。
9. 向下移动至：
   `#tcp_incoming_address 0.0.0.0`
   `#tcp_outgoing_address 0.0.0.0`
   `#udp_incoming_address 0.0.0.0`
   `#udp_outgoing_address 0.0.0.0`
10. 这些每一项都用于特定目的。要更改 Squid 用于监听 HTTP 或缓存请求的 IP 地址或 host.domain.extension，取消注释 tcp_incoming_address 行并进行编辑。例如：
    `tcp_incoming_address squid.animals.org`
11. 要更改 Squid 发送 HTTP 或缓存请求所经过的 IP 地址或 host.domain.extension，取消注释 tcp_outgoing_address 行并进行编辑。例如，要使用 squid.animals.org 发送出站 TCP 数据包，可以使用以下配置：
    `tcp_outgoing_address squid.animals.org`

> **注意：** 你可以为这四个项目使用相同的地址，每个使用不同的地址，或者分散使用。

12. 要更改 Squid 监听传入 ICP 查询的 IP 地址或 host.domain.extension，编辑 udp_incoming_address 行。例如，要使用地址 squid.animals.org 接收传入 UDP 数据包，可以使用以下配置：
    `udp_incoming_address squid.animals.org`
13. 要更改 Squid 发送 ICP 数据包所经过的 IP 地址或 *host.domain.extension*，编辑 **udp_outgoing_address** 行。例如，要为出站 UDP 数据包使用 squid.animals.org 的相同地址，可以使用以下配置：
    `udp_outgoing_address squid.animals.org`
14. 输入 `/icp_query_timeout` 并按 Enter 键跳转至以下内容：
    `#icp_query_timeout 0`
15. 如果你想手动设置 Squid 在 ICP 查询超之前等待多久，取消注释该行并将 0 更改为应等待的毫秒数。例如：
    `icp_query_timeout 4000`
16. 如果你有不希望被缓存的项目，首先输入 `/acl` 跳转至以下两行：
    `#acl QUERY urlpath_regex cgi-bin \`
    `#no_cache deny QUERY`
17. 要为不希望你被缓存的项目创建访问控制列表语句（**acl**），请按照以下格式构建语句：
    `acl *name type item*`
    
    其包含以下组成部分：
    - *name*——与此 ACL 定义对应的名称。
    - *type*——此定义中包含的项目类型，如表 14.1 中所述。
    - *item*——适用于该 ACL 类型的参数。可以列出多个参数。

如果你选择 **time** 类型，你需要知道如何构建正确的时间参数。要设置要监视的星期几，请使用表 14.2 中列出的字母之一。

然而，如果你想设置要监视的时间范围，请使用此格式：

`*hour1:minute1-hour2:minute2*`

**表 14.1 Squid ACL 语句类型。**

| 类型 | 用途 | 值 |
| :--- | :--- | :--- |
| browser | 指定要查找的浏览器 | 选择合适浏览器的正则表达式 |
| dst | 指定要查找的远程机器 IP 地址、网络地址或地址范围 | IP 地址、网络/子网掩码组合或 IP/子网掩码组合 |
| dstdomain | 指定要监视的远程 host.domain.extension 或 domain.extension | 一个或多个名称 |
| ident | 指定要监视的用户登录 | 用户名 |
| method | 指定要监视的请求类型 | HTTP 三种动作中的一个或多个：GET、HEAD 或 POST |
| port | 指定要监视的端口 | 端口号 |
| proto | 指定要监视的协议 | 协议本身，例如 HTTP |
| src | 指定要查找的本地 IP 地址、网络地址或地址范围 | IP 地址、网络/子网掩码组合或 IP/子网掩码组合 |
| srcdomain | 指定要监视的远程 host.domain.extension 或 domain.extension | 一个或多个名称 |
| time | 指定要监视的时间信息 | 以下两个中的一个或两者，按呈现顺序：日期指定（有关如何确定这两个变量的详细信息，请参见本表后的文本） |
| url_regex | 指定用于匹配 URL 的正则表达式 | 正则表达式 |

**表 14.2 Squid 中的 ACL 星期几设置。**

| 代码 | 星期 |
| :--- | :--- |
| S | 星期日 |
| M | 星期一 |
| T | 星期二 |
| W | 星期三 |
| H | 星期四 |
| F | 星期五 |
| A | 星期六 |

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_490_0.png)

18. 如果你构建了一个 **acl** 语句来告诉 Squid 不要在此机器上缓存特定信息，你需要在你的 **acl** 语句下方创建一个 **no_cache** 语句。使用以下格式：

```
no_cache deny aclName
```

19. 要定义你愿意为 Squid 的一些辅助功能分配的 RAM 量，首先向下移动到以下行：

```
#cache_mem 8 MB
```

20. 如果你想更改此值，因为这台机器专门用于缓存或拥有大量 RAM 且任务较少，那么取消注释并更改该数字。

21. 向下移动到：

```
#cache_swap_low 90
#cache_swap_high 95
```

22. 如果你想调节 Squid 何时开始清除缓存中的文件，取消注释这两行。当缓存达到 **cache_swap_high** 百分比的满容量时，Squid 开始删除使用频率最低的项目，直到其降至 **cache_swap_low** 百分比的满容量。如果你想更改这些值，取消注释这些行并编辑这些值。

23. 如果你想设置 Squid 不缓存特定大小或更大的文件，取消注释并更改分配给以下内容的值：

```
#maximum_object_size 4096 KB
```

24. 继续向下移动到：

```
#ipcache_size 1024
#ipcache_low 90
#ipcache_high 95
```

25. 如果你想更改 Squid 存储的 IP 地址解析值数量，取消注释并更改 **ipcache_size** 的值。

26. 如果你想更改导致 Squid 开始清除最少使用的 IP 地址解析信息的缓存满百分比，取消注释并更改 **ipcache_high** 的值。

