
# Linux 菜谱：日常使用的技巧与技术

以下方案描述了用于在新闻组（netnews）阅读和发布文章的工具。

## 33.3.1 选择新闻阅读器

选择新闻阅读器。
查找主题的新闻组。

### 33.3.2 为主题查找新闻组

## 33.3.1 选择新闻阅读器

允许你在组中读取和发布的应用程序被称为新闻阅读器。以下是一些适用于基于 Linux 系统的新闻阅读器。

### 新闻阅读器说明

- `gnus`
`Gnus` 是一个用于 `Emacs` 的强大且功能齐全的新闻阅读器。你也可以用它来读取邮件。@[Debian]: `gnus` @[WWW]: http://www.gnus.org/

- `knews`
一个用于 `X` 的图形化阅读器。其功能包括以图形树的形式显示文章线程，以及在慢速连接上阅读新闻的功能。@[Debian]: `knews` @[WWW]: http://www.matematik.se/~kj/

- `mozilla`
从历史上看，网页浏览器也内置新闻阅读器，这种功能在 `Mozilla` 浏览器中仍然存在。@[Debian]: `mozilla` @[WWW]: http://www.mozilla.org/

- `nn`
`nn` 的格号是“没有新闻是好事，但 nn 更好”；它是一个老（且非常受欢迎）的新闻阅读器，旨在在最短的时间内阅读尽可能的内容。@[Debian]: `nn` @[WWW]: http://www.math.edu-berlin.de/~gucks/

- `pan`
“Pump A** Newsreader”是一种为速度设计的的新一代新闻阅读器。它对初学者易于用，可以在带有 `GNOME` 的 `X` 中运行。@[Debian]: `pan` @[WWW]: http://www.supernimp.org/

- `peruser`
`NewsUser` 是一组用于 `X` 的小型工具，方便你在离线时阅读和编写新闻文章——在系统在线时下载新闻。@[Debian]: `peruser` @[WWW]: http://www.ibiblio.org/Pub/Linux/system/news/readers/

- `slrn`
`slrn` 基于最老的新闻阅读器之一，针对拨号连接（如家用调制解调器）进行了优化。@[Debian]: `slrn` @[WWW]: http://www.slrn.org/

## 33. 其他互联网服务

Linux 菜谱：日常使用的技巧与技术

### 33.3.2 为主题查找新闻组

@sf(Debian): `nn`
@sf(WWW): http://ftp.uwa.edu.au/pub/nn/beta/
使用 `ngroup` 查找匹配特定模式的新闻组名称。这对于查找特定主题的组很有用。

- 要输出所有匹配模式 `society` 的新闻组列表，输入：

```
$ nngroup society RET
```

使用 `-u` 选项仅搜索未订阅的组。如果你已经订阅了许多组，并且只想寻找未订阅的组，那么这很有用。

- 要输出所有匹配模式 `society` 的未订阅新闻组列表，输入：

```
$ nngroup society RET
```

在上一个例中，如果你已经订阅了 `alt.society.neutropia` 组，该组将不会显示；但其他匹配 `society` 且你未订阅的组将被列出。

## 33.4 列出在线系统和用户活动

以下工具用于列出网上其他用户和系统的活动——显示它们是否在线，并显示关于它们的更多信息。

- 33.4.1 检查系统是否在线
- 33.4.2 检查用户是否在线
- 33.4.3 列出谁登录了系统
- 33.4.4 查找主机名的 IP 地址
- 33.4.5 查找 IP 地址的主机名
- 33.4.6 列出域名的所有者

- 该系统在线吗？
该用户在线吗？
谁在该系统上？
该系统的 IP 地址是什么？
该 IP 地址的名称是什么？
谁在域名背后？

### 33.4.1 检查系统是否在线

使用 `ping` 确定特定系统当前是否连接到互联网。

输入 `ping` 后跟要检查的系统名称或数字 IP 地址；如果你的系统在线且目标系统也在线，`ping` 应该持续输出行，告知两个系统之间的延迟（以毫秒计）。输入 `C-c` 中断并停止 `ping`。

- 要 `ping` `bfi.org`，输入：

```
$ ping bfi.org RET

PING bfi.org (209.196.135.250): 56 data bytes

64 bytes from 209.196.135.250: icmp_seq=0 ttl=63 time=190.0 ms

64 bytes from 209.196.135.250: icmp_seq=1 ttl=63 time=159.9 ms

64 bytes from 209.196.135.250: icmp_seq=2 ttl=63 time=190.1 ms

64 bytes from 209.196.135.250: icmp_seq=3 ttl=63 time=190.0 ms

--- bfi.org ping statistics ---

4 packets transmitted, 4 received, 0% packet loss, time 3004ms

rtt min/avg/max/mdev = 159.9/182.5/190.1/14.5 ms
```

在此例中，输出显示该系统是可用的。延迟以毫秒为单位测量，`time` 值告诉数据包传输到服务器并返回的确切所需时间。

### 33.4.2 检查用户是否在线

使用 `finger` 检查用户是否在线。如果用户已登录，命令将显示有关其会话的信息。如果他们未登录，通常会返回未找到该用户的消息。

# Linux 菜谱：日常使用的技巧与方法：

`jezebel Jezebel Cate *rl 14 Sep 28 08:42 (dialup-YY.uu.net)`
`bradley Bradley Milton t2 2 Sep 28 09:35 (splj.org)`

### 33.4.4 查找主机名的 IP 地址

当你知道某个特定主机的名称并想要找到对应的 IP 地址时，可以 `ping` 该主机；这将在括号中输出主机的 IP 地址（参见“检查系统是否在线”章节）。

你也可以使用 `dig` 工具，它是一个“域名信息查询器”工具。将主机作为参数输出关于该主机的信息，包括在标记为“ANSWER SECTION”（回答部分）的章节中的 IP 地址。

- 若要查找主机 `linart.net` 的 IP 地址：

```
$ dig linart.net RET

...output messages...

;; ANSWER SECTION:

linart.net             1D IN A             64.240.156.195

...output messages...

$
```

在此例中，`dig` 输出 `64.240.156.195` 为主机 `linart.net` 的 IP 地址。

### 33.4.5 查找 IP 地址的主机名

若要查找给定 IP 地址的主机名，请使用带有 `-x` 的 `dig`。将 IP 地址作为参数输出该地址的信息，包括在标记为“ANSWER SECTION”（回答部分）的章节中的主机名。

- 若要查找 IP 地址 `216.92.9.215` 对应的主机名，输入：

```
$ dig -x 216.92.9.215 RET

...output messages...

;; ANSWER SECTION:

215.92.216.in-addr.arpa.     2H IN PTR     rumored.com.

...output messages...
```
