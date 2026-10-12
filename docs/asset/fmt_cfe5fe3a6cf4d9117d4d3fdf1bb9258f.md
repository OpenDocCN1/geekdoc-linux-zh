
# Pyrit

## 描述
`Pyrit` 允许创建大型数据库，在空间时间权衡下预计算 IEEE 802.11 WPA/WPA2-PSK 认证阶段的一部分。通过 ATI-Stream、`Nvidia CUDA` 和 `OpenCL` 利用多核平台及其他平台的计算能力，它目前是针对全球最常用安全协议之一最强大的攻击工具。

## 用法
`pyrit [options] command`

## 选项
`https://code.google.com/p/pyrit/wiki/ReferenceManual`

### 示例
`pyrit -e NETGEAR verify`

`pyrit -r /test/kismet_dump -o small_dump.pcap stripLive`

`pyrit -r "large_dumps_*.pcap" -e MyNetwork -o tiny_compressed_dump_MyNetwork.dump.gz strip`

`pyrit -r test.pcap -b 00:de:ad:be:ef:00 -i words.txt attack passthrough`

`pyrit -i dirty_words.txt -e NETGEAR -o passthrough | cowpatty -d -r wpratestcapture.cap -s NETGEAR`

`pyrit -u sqlite:///var/local/pyrit.db relay`

`pyrit -u http://192.168.0.100:17934 batch`

# RainbowCrack

`RainbowCrack` 是一个用于生成用于密码破解的彩虹表的计算机程序。`RainbowCrack` 与“传统”暴力破解器的不同之处在于，它使用名为彩虹表的大型预计算表，从而大幅缩短破解密码所需的时间。`RainbowCrack` 由朱爽来开发，实现了一种源自 Philippe Oechlin 的 `Ophcrack` 的改进时间内存权衡密码分析攻击。

## 用法
`rcrack rainbow_table_pathname -h hash`

`rcrack rainbow_table_pathname -l hash_list_file`

`rcrack rainbow_table_pathname -f pwdump`

## 选项
`rainbow_table_pathname` 彩虹表（或多个表）的路径，支持通配符(`*`, `?`)

`-h hash` 使用原始哈希作为输入

`-l hash_list_file` 使用哈希列表文件作为输入，每行一个哈希

`-f pwdump_file` 使用 `pwdump` 文件作为输入，这将仅处理 LAN Manager 哈希

### 示例
`rcrack *.rt -h 5d514020abc4b2a76b9719d911017c592`

`rcrack *.rt -l hash.txt`

`rcrack *.rt -f hash.txt`

## rcracki_mt

### 描述
`rcracki_mt` 可对密码哈希进行彩虹表攻击。它用于索引化和完美的彩虹表，这些表主要由分布式项目 `www.freerainbowtables.com` 生成。

### 用法
`rcracki_mt [options] [hash]`

### 选项
`http://sourceforge.net/project/shownotes.php?release_id=682650`

### 示例
`rcracki_mt -h 5d41402abc4b2a76b9719d911017c592 -t 4 -o save.txt C:\md5`

`rcracki_mt -r -s my_personal_hashes`

# rsmangler

## 描述
`RSMangler` 将接收一个词列表并对其进行各种操作，类似于 `John the Ripper` 的操作，并额外了一些。主要的新功能是排列模式，它取列表中的每个单词并与其他单词结合，生成所有可能的排列（不是组合，顺序很重要）。

## 用法
`rsmangler.rb [OPTIONS]`

## 选项
`http://www.randomstorm.com/rsmangler-security-tool.php`

### 示例
`./rsmangler.rb -file wordlist.txt > new_wordlist.txt`

# samdump2

## 描述
`samdump2` 导出 Windows 2k/NT/XP/Vista 的密码哈希。

更多信息：`http://www.hackingdna.com/2012/05/learn-samdump2-on-backtrack-5.html`

## 用法
`samdump2 samhive keyfile`

### 示例
`/samdump2 SAM bootkey > hashes`

`samdump2 /mnt/Windows/Windows/System32/config/SAM syskey.txt`

`samdump2 /mnt/Windows/Windows/System32/config/SAM syskey.txt>hash`

`samdump2 /root/sda2/Windows/System32/config/SAM saved-syskey.txt > /root/pass1`

从 Windows 分区 `/dev/sda1` 提取 SAM 哈希的示例：

```
mkdir -p /mnt/sda1
mount /dev/sda1 /mnt/sda1
bkhive /mnt/sda1/Windows/System32/config/SYSTEM /tmp/saved-syskey.txt
samdump2 /mnt/sda1/Windows/System32/config/SAM /tmp/saved-syskey.txt /tmp/hashes.txt
```

# burpsuite

## 描述
`Burp Suite` 是一个用于 Web 应用程序安全测试的集成平台。它的各种工具无缝协作工作，支持整个测试过程，从对应用程序攻击面的初始映射和分析，一直到发现和利用安全漏洞。

`Burp Suite` 包含以下核心组件：

- 拦截代理（Proxy），允许你检查并修改你的浏览器与目标应用程序之间的流量。
- 应用程序感知型爬虫（Spider），用于爬取内容和功能。
- 进阶 Web 应用程序扫描器（Scanner），用于自动检测多种类型的漏洞。
- 入侵者工具（Intruder），用于执行强大的自定义攻击，以发现并利用异常的漏洞。
- 重复器工具（Repeater），用于操作和重新发送单个请求。
- 序列器工具（Sequencer），用于测试会话令牌的随机性。
- 保存工作并在稍后继续工作的能力。
- 可扩展性，允许你轻松编写自己的插件，以便在 Burp 中执行复杂且高度定制的任务。

更多信息：`http://portswigger.net/burp/`

## 用法
不适用；GUI 工具

## 示例
不适用；GUI 工具

# cewl

## 描述
`Cewl` 是一个 Ruby 应用，它会根据指定的深度爬取给定的 URL（可选地跟随外部链接），并返回单词列表，这些单词随后可以用于 `john the Ripper` 等密码破解器。

默认情况下，`Cewl` 仅限于你指定的站点，并进行到 2 层链接的深度，此行为可以通过传递参数来更改。如果设置了较大的深度并允许其访问站外内容，请小心，你可能会在许多其他域名之间跳转。所有三个字符及以上的单词都会输出到标准输出。此长度可以增加，并且单词可以写入文件而不是屏幕，以便程序自动化。

## 用法
`cewl [OPTION] ... URL`

## 选项
`http://www.digininja.org/projects/cewl.php`

### 示例
`/cewl.rb -w passwords.txt http://www.digininja.org/projects/cewl.php` 从 `http://www.digininja.org/projects/cewl.php` 创建密码文件并保存到 `passwords.txt` 中

# cisco-auditing-tool

## 描述
Cisco Auditing Tool - 一个用于扫描 Cisco 路由器常见漏洞的 Perl 脚本。检查默认密码、易猜的社区名称（community names）以及 IOS 历史漏洞。支持插件和扫描多个主机。

## 用法
`./-CAT [options]`

- `-h hostname` 用于扫描单个主机
- `-f hostfile` 用于扫描多个主机
- `-p port #` 默认端口为 23
- `-w wordlist` 用于猜测社区名称的字典
- `-a passlist` 用于猜测密码的字典
- `-i [ioshist]` 检查 IOS 历史漏洞
