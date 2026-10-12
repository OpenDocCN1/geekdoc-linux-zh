
当您工作时，可能会出现很多问题：如果不确定是硬件还是软件问题，像 `lsof` 这样的工具可以帮助您找到问题的源。以下命令显示所有网络信息：

```
lsof -i
```

## 03 哪个程序监听端口？

第一个问题将轻松回答哪个 Linux 机器上的 TCP 端口。要找出特定的端口，请运行：

```
$ lsof -iP -t
```

TCP 连接的其他可能状态包括 `CLOSED`、`SYN-SENT`、`ESTABLISHED`、`CLOSE-WAIT`、`CLOSING` 和 `TIME-WAIT`。

## 04 重复模式

如果转换 ID 名称工作正常，你可以使用 `-n` 禁用它。使用 `-r` 选项运行 `lsof` 进入重复模式，每秒运行一次。当 `lsof` 处于重复模式时，它每秒打印一次，默认值为 5 秒。你可以在 `-r` 之后更改值。

## 05 用户 ID

以下命令将列出所有本地 SSH 连接：

```
lsof | grep ssh
```

以下版本将提供相同的信息：

```
lsof -i | grep EST
```

## 06 查找 SSH 连接

你可以运行以下命令找到访问 `/var/run/mysqld.sock` 的进程：

```
lsof /var/run/mysqld.sock
```

如果你对访问文件的 ID 感兴趣，使用 `-t` 选项：

```
lsof -t /var/run/mysqld.sock
```

进程 ID 可杀死杀死。`linux.com`

# 教程

![](img/2f9ef091d4813dbe86196f72ccfd0107_27_0.png)

![](img/2f9ef091d4813dbe86196f72ccfd0107_27_1.png)

![](img/2f9ef091d4813dbe86196f72ccfd0107_27_2.png)

| PID | USER | GROUP | NAME | STAT | START | TIME |
|---|---|---|---|---|---|---|
| 1 | root | root | systemd | S | 00:01 | 2h |
| 2 | root | root | `kworker/u0` | S | 00:01 | 2h |
| 3 | root | root | `kworker/u1` | S | 00:01 | 2h |
| 4 | root | root | `kworker/u2` | S | 00:01 | 2h |
| 5 | root | root | `kworker/u3` | S | 00:01 | 2h |
| 6 | root | root | `kworker/u4` | S | 00:01 | 2h |
| 7 | root | root | `kworker/u5` | S | 00:01 | 2h |
| 8 | root | root | `kworker/u6` | S | 00:01 | 2h |
| 9 | root | root | `kworker/u7` | S | 00:01 | 2h |
| 10 | root | root | `kworker/u8` | S | 00:01 | 2h |
| 11 | root | root | `kworker/u9` | S | 00:01 | 2h |
| 12 | root | root | `kworker/u10` | S | 00:01 | 2h |
| 13 | root | root | `kworker/u11` | S | 00:01 | 2h |
| 14 | root | root | `kworker/u12` | S | 00:01 | 2h |
| 15 | root | root | `kworker/u13` | S | 00:01 | 2h |
| 16 | root | root | `kworker/u14` | S | 00:01 | 2h |
| 17 | root | root | `kworker/u15` | S | 00:01 | 2h |

## 使用 lsof 获取网络信息

通过识别进程来排查网络故障

| 命令 | 类型 | 大小/偏移 | 节点 |
| --- | --- | --- | --- |
| `lsof -i -C /./` | | | | |
| `md 222 cwd` | `REG` | 200 | 4096 |
| `md 222 root` | `REG` | 200 | 4096 |
| `md 25906 root` | `REG` | 4096 | 4096 |
| `md 25906 root` | `REG` | 4096 | 6358 |
| `md 23906 root` | `REG` | 4096 | 16488 |
| `md 23906 root` | `REG` | 4096 | 30512 |
| `u/libattr.so.1.4` | `REG` | 17132 | 5668 |
| `u/libcap.so.22` | `REG` | 81620 | 126808 |
| `u/security/pam.so` | `REG` | 6000 | 5947 |
| `u/security/perm_mit.so` | `REG` | 6000 | 5947 |
| `u/security/deny.so` | `REG` | 5912 | 5947 |
| `u/libssl.so.11` | `REG` | 35184 | 6418 |
| `u/libcrypt.so` | `REG` | 50656 | 5960 |
| `u/security/unix.so` | `REG` | 18240 | 5942 |
| `u/security/pam_mail.so` | `REG` | 14368 | 6398 |
| `u/security/dev_env.so` | `REG` | 10248 | 6448 |
| `u/libsel.so` | `REG` | 122632 | 5648 |
| `u/security/root.so` | `REG` | 6016 | 5947 |
| `u/lib_linux-file-23.so` | `REG` | 20716 | 6428 |
| `u/libgcc-la-13.so` | `REG` | 43560 | 6478 |
| `md 25906 root` | `REG` | 80956 | 6418 |
| `md 23906 root` | `REG` | 31584 | 6413 |
| `md 23906 root` | `REG` | 14765 | 6395 |
| `md 23906 root` | `REG` | 163068 | 6356 |

## 16 正则表达式

你可以处理 `lsof` 的输出并创建摘要。借助 `awk`，可以很容易找到 TCP 和 UDP 连接的数量。以下命令可以轻松解决问题：

```bash
lsof -i -nP | grep "80" | uniq -c
```

`lsof` 命令列出所有连接，`awk` 提取字段并对其进行排序。`uniq -c` 统计每行出现的次数。最后，`grep` 删除包含 `"UDP"` 字符串的行。你可以使用以下命令获取关于 `lsof` 的所有信息：

```bash
lsof -i -nP | grep ESTABLISHED | awk '{1,$5}' | sort
```

## 17 有用技巧

与其他任何工具一样，`lsof` 并不完美，因为它无法看到所有的网络问题。对于相关问题，你可能需要的其他工具包括：`netstat`、`iptables`、`tcpdump`、`Wireshark`、`tshark` 或 `trace`。`lsof` 工具的作用范围是有限的。

`lsof` 支持正则表达式。为了找到所有字符，你可以使用这个：正则表达式以斜杠开头和结束。`^` 字符表示行首，`$` 表示行尾。每个点号代表一个字符。

## 在 IPv4 和 IPv6 之间选择

`lsof` 默认支持 IPv4 和 IPv6，你可以选择要显示的连接类型。下一个命令显示：

## 禁用 DNS 和端口

`lsof` 使用 `/etc/services` 文件中的数据将端口映射到服务。你可以使用 `-P` 关用此功能：`-n`。

`lsof` 使用 DNS 显示主机名而不是其 IP 地址。你可以通过其功能将其关闭：

## 关于 lsof 输出的更多信息

`lsof` 的输出显示各种列。`COMMAND` 列包含进程相关的命令。`PID` 列显示进程 ID。`USER` 列显示用户名。`FD` 列显示文件描述符。`TYPE` 列显示文件、目录或字节的类型。`SIZE` 列包含大小。`DEVICE` 列包含用逗号分隔的设备号。`NODE` 列显示挂载点名称或 `FILE` 列显示文件名或以字节计算的文件偏移。

这是 LaTeX 项目的主网站，你可以在那里找到更多信息：`linux.com`

`LaTeX` 是一个高质量的排版系统，专为技术和科学文档的制作而设计。`LaTeX` 是科学文档出版和分发的行业标准。它可以作为免费软件提供。

## 产品

该项目完全关于这一点，不过，请看我们对 `LaTeX` 的简要介绍。我们为很久以前的每个 `LaTeX` 版本都提供了 PDF。

## LaTeX 项目
