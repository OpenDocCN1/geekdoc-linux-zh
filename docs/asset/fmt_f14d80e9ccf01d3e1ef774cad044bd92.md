
| `nis` 或 `yp` | 咨询 `NIS`。 |

| `dns` | 使用 `DNS` 服务器。 |

| `files` | 使用本地文件（通常是 `/etc/hosts`）进行名称解析。 |

| `db` | 使用本地数据库文件，`.db` 文件。 |

| `compat` | 使用兼容模式的 `NIS`。 |

| `[NOTFOUND=return]` | 停止搜索。 |

### `resolv.conf` 文件

`/etc/resolv.conf` 文件配置系统如何使用 `DNS`。示例如下：

```
    search the-nashes.net jasonnash.com
    nameserver 10.254.90.131
    nameserver 10.254.90.130
    nameserver 4.2.2.1
```

`search` 行指定了要搜索的域名（如果未指定其他域名的情况下）。例如，如果用户在 Web 浏览器中输入 `www`，系统将搜索 `www.the-nashes.net` 和 `www.jasonnash.com`。

`nameserver` 条目指定了最多三个用于查询的 `DNS` 服务器。由于服务器按顺序进行检查，因此应将最稳定的服务器放在顶部。服务器之间的超时时间明显较长，因此如果您在列表顶部放置了一个不稳定的服务器，您和您的用户将会注意到这一点。

### 使用 `DNS` 工具

可以使用几个命令行工具来排查和查询 `DNS` 数据库。这些工具如下：

- `nslookup`
- `dig`
- `host`

它们之间的某些功能是重叠的，因此选择使用哪一个有时取决于个人偏好。

> `Debian` 用户可能需要安装 `dnsutils` 软件包以获取这些工具。

#### `nslookup` 工具

`nslookup` 工具是一个强大的查询工具，可以作为非交互式命令行工具使用，也可以从交互式 shell 中使用。当你不带任何选项运行 `nslookup` 时，它会进入一个提示符，该提示符应如下所示：

```
Default Server: nsl.the-nashes.net
Address: 10.254.90.131
>
```

从提示符可用的命令如表 16-34 所示。使用非交互模式的语法如下：

```
nslookup [-option...] host-to-find [-server]
```

交互式模式下使用的相同选项也可以在命令行中指定。

##### 表 16-34

##### `nslookup` 命令行选项

| 命令 | 功能 |
|---|---|
| `<name>` | 打印请求名称的信息。 |
| `help` 或 `?` | 打印命令帮助。 |
| `exit` | 退出 `nslookup`。 |
| `server <host>` | 使用当前服务器将默认服务器设置为指定主机。 |
| `lserver <host>` | 类似于 `server`，但使用最初设置的服务器，而不是当前服务器。 |
| `set querytype=<type>` | 指定要查询的记录类型。 |
| `set debug` | 启用调试。 |
| `set d2` | 启用更多调试。 |
| `set domain=<domain>` | 更改默认域。 |
| `set retry=<number>` | 设置重试次数。 |
| `ls [option] <domain>` | 列出请求域的所有主机和地址映射。可以添加以下选项以仅列出某些主机类型：<br>- `-a` - 列出规范（别名）名称。<br>- `-h` - 列出主机信息。<br>- `-s` - 列出知名服务。这些是在 `DNS` 中用 `WKS` 资源记录列出的服务。<br>- `-d` - 列出所有记录。<br>- `-t <type>` - 列出指定的记录类型。 |
| `finger <user>` | 在默认主机上 `finger` 可选用户。 |
| `root` | 将当前默认服务器设置为根服务器。 |

#### `dig` 工具

`dig`（domain information groper，域名信息获取器）工具大致提供与 `nslookup` 相同的功能，但只能从命令行使用。语法如下：

```
dig [server] domain [query-type] [query-class] +<query-option> [-<dig-option>] [%comment]
```

表 16-35 和 16-36 显示了支持的查询类型和查询类别。查询和 `dig` 选项通常不使用，除非 `dig` 在批处理模式下运行。关于运行批处理模式的信息可以在手册页（`man` page）中找到。`dig` 的一个使用示例如下所示：

```
[root@redhat ~]# dig @ns1.the-nashes.net MX the-nashes.net

<<> Dig 8.2 <<> @ns1.the-nashes.net MX the-nashes.net
; (1 server found)
;; res options: init recurs defnam dnsrch
;; got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 6
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0,
; ADDITIONAL: 1
;; QUERY SECTION:
;; the-nashes.net. type = MX, class = IN

;; ANSWER SECTION:
the-nashes.net. 1H IN MX 10 mail.the-nashes.net.

;; ADDITIONAL SECTION:
mail.the-nashes.net. 1H IN A 216.254.90.131

;; Total query time: 87 msec
;; FROM: redhat.the-nashes.net to SERVER: ns1.the-nashes.net
216.254.90.131
;; WHEN: Sat Dec 9 22:40:26 2000
;; MSG SIZE sent: 32 rcvd: 69
```

如您所见，`dig` 提供了关于查询及其解析方式的大量信息。

##### 表 16-35

##### `dig` 支持的查询类型

| 查询类型 | 功能 |
| :--- | :--- |
| `a` | 主机地址（默认）。 |
| `any` | 指定域的任何信息。 |
| `mx` | 域的邮件交换器信息。 |
| `ns` | 关于域的姓名服务器信息。 |
| `soa` | 权威开始记录。 |
| `hinfo` | 主机信息记录。 |
| `axfr` | 请求区域传输。为了使其正常工作，必须查询权威服务器。 |
| `txt` | 文本字符串记录。 |

##### 表 16-36

##### `dig` 支持的查询类别

| 查询类别 | 功能 |
|---|---|
| `in` | 互联网地址（默认） |
| `any` | 任何类别 |

#### `host` 工具

`host` 工具比另外两个工具小，通常提供的信息较少；然而，在许多需要快速查询的情况下，它非常有用。`host` 的语法如下：

```
host [-adlrwv] [-t querytype] [-c class] host [server]
```

`host` 的示例如下：

```
[root@redhat ~]# host -v norbert.the-nashes.net
Trying null domain
rcode = 0 (Success), ancount=1
The following answer is not verified as authentic by the server:
norbert.the-nashes.net 3600 IN A 216.254.90.133
```

表 16-37 显示了可用的 `host` 选项。

##### 表 16-37

##### `host` 选项

| 选项 | 功能 |
|---|---|
| `-a` | 等同于 `-v -t *`。 |
| `-c` | 要查找的类别（如果不是 Internet）。 |
| `-d` | 启用调试信息。 |
| `-l` | 开启列表模式。 |
| `-r` | 禁用递归。被查询的服务器必须已经知道请求的数据。 |
| `-t` | 要查询的记录类型。可以使用 `*` 来列出所有类型。 |
| `-v` | 启用详细输出以获取更多信息。 |
| `-w` | 不要超时；而是永远等待回复。 |

### 管理 `DNS` 服务器

`BIND` 绝不应从 `inetsd` 运行。与其他服务一样，它通常通过 `rc` 脚本来启动和停止。在 `Red Hat` 上，此脚本如下：
