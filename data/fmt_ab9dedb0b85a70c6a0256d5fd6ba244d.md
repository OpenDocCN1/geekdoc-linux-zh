
| travel | 用于旅行相关的 TLD |

顶级域名服务器被称为根域名服务器，因为它提供了关于域的信息。例如，如果你想搜索 `*.w.mhlenberg.com`，它会向根域名服务器查询 `.edu`，根域名服务器会将搜索引导到较低级别的域名服务器，直到找到信息。

在图 1 中，你使用 `dig` 命令搜索关于 `.edu` 的信息。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3ff_98_0.png)

图 1：在顶级根域名服务器中搜索 `.edu`

通过添加域名名称来继续搜索第二级域名，如图 2 所示：

# 第 4 章

vadmin@vadmin:~

```
File Edit View Help
(vadmin@vadmin:~ -15 dig muebleberg.org)
>>> dig 9.0.1-debug @8.8.8.8 +8.4 fr1 <<< muebleberg.org
>> global options:
>> get answer
>> query: QUERY; status: REFUSED; id: 54991
>> flags: qr QUERY: 1; ANSWER: 0; AUTHORITY: 0; ADDITIONAL: 0
>> WARNING: recursion requested not available

QUESTION SECTION
muebleberg.org. IN A

ANSWER SECTION
Server: 192.168.2.203 192.168.2.204
Time: Fri May 19 10:53:11 2023
MS: 5128 rcv: 32
```

图 2：二级域名的查询。

找到域名后，通过其本地域名服务器提供有关域名的信息。本地域名服务器有三种类型：

- *主服务器（Master）*：它被列为权威服务器，因为它包含了有关该域的所有信息，并在需要时提供这些信息。
- *从服务器（Slave）*：它维护主服务器的备用（包含与主服务器相同的信息）。当主服务器宕机或不可用时使用它。
- *缓存服务器（Caching）*：它用于向本地网络上的其他服务器和工作站提供信息。由于域名信息已存储在内存中，缓存服务器可以加快搜索。

在下一节中，你将学习主服务器和从服务器如何收集有关域名的信息。你必须配置服务器在需要时提供这些信息。

让我们学习如何配置服务器提供域名解析信息。

## 检查服务器配置文件

在配置服务器提供域名解析信息之前，你需要配置一些文件。这些文件取决于你系统中安装的 `BIND` 服务器。

- *`named.conf`*：该文件位于 `/etc/bind` 目录，包含全局属性和配置文件的来源。
- *`named.ca`*：该文件位于 `/var/named` 目录，包含根服务器的名称和地址。
- *`named.local`*：该文件位于 `/var/named` 目录，提供解析 `localhost` 回环地址的信息。

设置 `named` 服务器需要五个文件。它们如下：

- *`zone`（区域）*：该文件包含本地域内服务器和工作站的名称和地址，并提供这些名称到 IP 地址的映射。
- *`reverse zone`（反向区域）*：该文件提供将 IP 地址映射到名称的反向。

无论作为主服务器、从服务器还是仅缓存服务器，前三行都是必须的，最后两个文件是主域名服务器所需的。

要启动 `BIND` 服务器，使用 `/etc/rc.d/init.d/named` 脚本。

让我们详细讨论 `named.conf` 文件。

### named.conf

以下是 `/etc/named.conf` 文件的内容：

```
// named.conf
options {
    listen-on port 53 { 127.0.0.1 };
    listen-on port 53 { :1 };
    directory "var/named";
    dump-file "var/named/data/cache_dump.db";
    statistics-file "var/named/data/named_stats.txt";
    memastats-file "var/named/data/named_mem_stats.txt";
    allow-query { localhost };
}
logging {
    channelfile_debug {
        file "data/named.run";
        dynamic;
    }
    zone "." IN {
        type file;
        hint "named.ca";
        include "/etc/named.rfc1312.zones";
    }
}
```

以 `//` 开头的行是注释行。命令以语句的形式传递给文件。语句的信息包含在大括号 `{}` 中并以 `;` 结束。上面显示了几个命令。你可以在 `named.conf` 文件中拥有以下配置语句：

- *`options`*：它包含默认和全局配置。
- *`include`*：它包含来自另一个文件的信息。
- *`acl`*：它指定用于访问控制列表的 IP 地址。
- *`logging`*：它指定日志位置和内容。
- *`server`*：它提供远程服务器属性。
- *`zone`*：它提供区域信息。
- *`key`*：它指定用于身份验证的安全密钥。

让我们讨论这些语句。

# 第 4 章

## options

`options` 语句是 `named.conf` 的第一部分，用于指定 `named` 的工作目录。`named.conf` 文件中应定义一个 `options` 语句。`options` 语句定义了全局服务器配置选项并为其他语句设置默认值。你可以为 `options` 语句设置多个值。

`options` 语句使用以下语句：

```
options{
  value "property";
}
```

在上述语句中，`value` 指令被替换为有效的选项。在 `options` 语句中可以值列表是一个长列表；以下是常用的选项：

- *`allow-query`*：它指定允许查询域名服务器的主机。默认情况下，允许所有主机查询。
- *`allow-recursion`*：它适用于递归查询。默认情况下，允许所有主机对域名服务器执行递归查询。
- *`blackhole`*：它指定不允许查询的主机。
- *`directory`*：它指定 `named` 目录。
- *`forward`*：它指定转发行为。
- *`listen-on`*：它指定监听在哪些端口和接口进行查询（默认是 53）。
- *`notify`*：它控制当区域更新时通知从服务器。它接受 *yes* 或 *no*。
- *`pid-file`*：它指定持有进程 ID 的文件名。
- *`statistics-file`*：它指定统计文件的备用位置。默认情况下，`named` 统计保存在统计文件中。

### include

该语句允许在 `named.conf` 中包含任何文件的路径和名称。`include` 语句使用以下语法：

```
include "filename";
```

在此语句中，`filename` 被替换为路径。

### ACL

访问控制列表 `ACL` 定义了一个或多个 IP 地址列表。`acl` 语句定义了允许或拒绝访问服务器的主机组。

`acl` 语句采用以下形式：

```
acl <acl-name> {
  <match-element>; <match-element>; ...
};
```

在此语句中，将 `<acl-name>` 替换为访问列表的名称，将 `<match-element>` 替换为分号分隔的 IP 地址列表。

### Logging

在 `logging` 中，你指定服务器的日志选项。它可以包含通道（channel）和类别（category）。在通道中，你指定日志信息的位置。日志信息可以写入文件、发送到 `syslog` 或通过指定适当的命令丢弃。定义了自定义通道，类别选项用于对通道进行分类，并在 `named` 重启时启动日志。

以下是 `logging` 语句的语法：

```
logging {
channel<channel name {
  file-path to file>
  version<specify number>
  size<specify size in bytes> }
}
```

要丢弃信息，请选择 `null` 作为目标：

```
logging {
channel<channel name {
  null;
}
}
```

你需要替换上述语句中 `<>` 中的值。以下是使用类别语句的语法：

```
category category name {
channel name; channel name;
}
```
