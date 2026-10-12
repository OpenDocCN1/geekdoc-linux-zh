
在列表 47 中，我们回显了一行并将其管道传输到 `awk` 以使用 `:` 作为字段分隔符提取第一个 `($1)` 和第三个 `($3)` 字段。我们使用的 `cut` 和 `awk` 示例之间最显著的区别在于，`cut` 只能接受单个字符作为字段分隔符，而 `awk` 如列表 47 所示，具有更大的灵活性。作为一般经验法则，当你的命令开始涉及多个 `cut` 操作时，你可能需要考虑切换到 `awk`。

- 59 (Wikipedia, 2019), https://en.wikipedia.org/wiki/AWK
- 60 (GNU, 2019), https://www.gnu.org/software/gawk/manual/gawk.html

### 3.3.5 实用示例

让我们来看一个将我们之前探索过的许多命令结合在一起的实用示例。

我们提供了一个 Apache HTTP 服务器日志 (`http://www.offensive-security.com/pwk-files/access_log.txt.gz`)，其中包含攻击的证据。我们的任务是使用 Bash 命令检查该文件并发现各种信息，例如攻击者是谁以及服务器上确切发生了什么。

首先，我们将使用 `head` 和 `wc` 命令快速查看日志文件以了解其结构。`head` 命令显示文件的前 10 行，而 `wc` 命令配合 `-l` 选项显示文件中的总行数。

```
kali@kali:~$ gunzip access_log.txt.gz
kali@kali:~$ mv access_log.txt access.log

kali@kali:~$ head access.log
201.21.152.44 -- [25/Apr/2013:14:05:35 -0700] "GET /favicon.ico HTTP/1.1" 404 89 "-"
"Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.31 (KHTML, like Gecko) Chrome/26.0.1410.64 Safari/537.31" "random-site.com"
70.194.129.34 -- [25/Apr/2013:14:10:48 -0700] "GET /include/jquery.jshowoff.min.js HTTP/1.1" 200 2553 "http://www.random-site.com/" "Mozilla/5.0 (Linux; U; Android 4.1.2; en-us; SCH-I535 Build/JZ054K) AppleWebKit/534.30 (KHTML, like Gecko) Version/4.0 Mobile Safari/534.30" "www.random-site.com"

kali@kali:~$ wc -l access.log
1173 access.log
```

> 列表 48 - 查看 `access.log` 文件以了解其结构

请注意，该日志文件是基于文本的，包含由空格分隔的不同字段（IP 地址、时间戳、HTTP 请求等）。这是一个完美的“*grep 友好*”文件，适用于我们迄今介绍的所有工具。我们将首先搜索发送到服务器的 HTTP 请求中记录在此日志文件中的所有 IP 地址。我们将通过管道传输 `cat` 命令的输出到 `cut` 和 `sort` 命令来实现这一点。这可能会给我们关于需要处理的潜在攻击者数量的线索。

```
kali@kali:~$ cat access.log | cut -d " " -f 1 | sort -u
201.21.152.44
208.115.113.91
208.54.80.244
208.68.234.99
70.194.129.34
72.133.47.242
88.112.192.2
98.238.13.253
99.127.177.95
```

> 列表 49 - 管道命令以从文件中获取所需信息

我们可以看到日志文件中记录了不到十个 IP 地址，尽管这仍然没有告诉我们任何关于攻击者的信息。接下来，我们使用 `uniq` 和 `sort` 来显示唯一行，进一步细化我们的输出，并根据每个 IP 地址访问服务器的次数对数据进行排序。`uniq` 的 `-c` 选项会在输出行前添加出现次数。

```
kali@kali:~$ cat access.log | cut -d " " -f 1 | sort | uniq -c | sort -urn
     1038 208.68.234.99
       59 208.115.113.91
       22 208.54.80.244
       21 99.127.177.95
        8 70.194.129.34
        1 201.21.152.44
```

> 列表 50 - 使用 `uniq` 命令获取文件中每个 IP 地址的计数

有几个 IP 地址脱颖而出，但我们首先关注访问频率最高的地址。为了过滤出 `208.68.234.99` 地址并显示及计数由该 IP 请求的资源，我们可以使用以下序列：

```
kali@kali:~$ cat access.log | grep '208.68.234.99' | cut -d """ -f 2 | uniq -c
     1038 GET //admin HTTP/1.1
```

> 列表 51 - 探索特定 IP 地址访问的资源

从输出结果来看，IP 地址 `208.68.234.99` 似乎专门在访问 `/admin` 目录。让我们进一步检查。

```
kali@kali:~$ cat access.log | grep '208.68.234.99' | grep '/admin ' | sort -u
208.68.234.99 - - [22/Apr/2013:07:51:20 -0500] "GET //admin HTTP/1.1" 401 742 "-" "Teh Forenst Lobster"
208.68.234.99 - admin [22/Apr/2013:07:51:25 -0500] "GET //admin HTTP/1.1" 200 575 "-"
```

#### 3.3.5.1 练习

- 1. 使用 `/etc/passwd`，提取你的 Kali 机器上所有 shell 设置为 `/bin/false` 的用户的用户字段和主目录字段。请务必使用 Bash 单行命令将输出打印到屏幕上。输出应类似于下方的清单 53：

```bash
kali@kali:~$ YOUR COMMAND HERE...
The user mysql home directory is /nonexistent
The user Debian-snap home directory is /var/lib/snmp
The user speech-dispatcher home directory is /var/run/speech-dispatcher
The user Debian-gdm home directory is /var/lib/gdm3
```

清单 53 - shell 为 `/bin/false` 的用户的主目录

- 2. 将 `/etc/passwd` 文件复制到你的主目录（`/home/kali`）。
- 3. 使用 `cat` 编写一个单行命令，打印 `/kali/passwd` 的输出，并将所有 “Gnome Display Manager” 字符串替换为 “GDM”。

## 3.4 从命令行编辑文件

接下来，让我们看看命令 shell 环境中的文件编辑。这是一个极其重要的 Linux 技能，尤其是在渗透测试过程中，如果你恰好获得了类 Unix 操作系统的访问权限时更是如此。

虽然像 `gedit` 和 `leafpad` 这样的文本编辑器因其图形用户界面可能看起来更美观，但我们将专注于基于文本的终端编辑器，它们强调速度和通用性。

在文本编辑器方面，每个人似乎都有自己的偏好，但我们将介绍两种最常见选项的基本用法：`nano` 和 `vi`。

### 3.4.1 nano

`nano` 是最易用的文本编辑器之一。要打开一个文件并开始编辑，只需运行 `nano`，并将文件名作为可选参数传入：

```bash
kali@kali:~$ nano intro_to_nano.txt
```

清单 54 - 使用 `nano` 编辑器打开文件

文件打开后，我们可以立即开始对文件进行任何必要的更改，就像在图形编辑器中一样。如图 5 所示，命令菜单位于屏幕底部。需要记住的一些最常用命令包括：`Ctrl+O` 将更改写入文件，`Ctrl+K` 剪切当前行，`Ctrl+U` 取消剪切一行并将其粘贴到光标位置，`Ctrl+W` 进行搜索，以及 `Ctrl+X` 退出。

![](img/ec25e59d75726b7041242a56d3376832_60_0.png)

有关 `nano` 的更多信息，请参阅其在线文档。

### 3.4.2 vi
