
脚本会在 `iptables` 目录下创建 `debug.txt` 文件。使用文本编辑器检查 `debug.txt` 内容以判断脚本是否运行成功。测试完成后，你可以安装 DShield。

## 安装 DShield

要安装客户端，将 `iptables` 目录中的文件移动到表 13-3 所示的新位置。你还应该阅读 `/usr/local/doc/dshield/README.txt` 内容，它解释了安装和配置过程。（这些在本本书出版后可能已经更新。）

### 表 13-3 DSHIELD 客户端位置

| 文件 | 路径 |
|---|---|
| changelog.txt | /usr/local/doc/dshield |
| CVS | /usr/local/doc/dshield |
| dshield.cnf | /etc |
| dshield-source-exclude.lst | /etc |
| dshield-source-port-exclude.lst | /etc |
| dshield-target-exclude.lst | /etc |
| dshield-target-port-exclude.lst | /etc |
| iptables | /usr/local/bin |
| README.txt | /usr/local/doc/dshield |
| test.cnf | /etc |
| test_wrapper.sh | /usr/local/bin |

## 自定义 DShield

DShield 的主配置文件是 `/etc/dshield.cnf`。你应该修改其日志指令指向系统日志文件，就像你之前在 `test.cnf` 中修改相同指令一样。除了日志指令外，你还应该修改这些指令：

# 第 13 章：管理防火墙 401

- `from` 应该指定您的回邮件地址。
- `userid` 应该指定您的 DShield ID。

您可以通过 DShield 网页注册获取 DShield ID。如果您想隐藏 IP 地址信息，可以将 `obfus` 指令的值从 N 改为 Y。否则，DShield 可能会将您的报告转发给攻击者 ISP 的滥用联系人，这可能导致您的 IP 地址以范围超出您预想的方式公开。

列表 13-3: dshield.cnf

```
from-nobody@nowhere.com

userid=0

to-report+hield.org

bcc=

bcc=

log=/var/log/messages

sendmail=/usr/sbin/sendmail -oi -t

whereeto=MAIL

source_exclude=/etc/dshield-source-exclude.lst

target_exclude=/etc/dshield-target-exclude.lst

source_port_exclude=/etc/dshield-source-port-exclude.lst

target_port_exclude=/etc/dshield-target-port-exclude.lst

obfus=N

linecnt=/tmp/dshield.cnt

verbose=N

debug=N

rotate=N
```

DShield 配置文件标识了影响 DShield 操作的辅助文件：

- dshield-source-exclude.ls
- dshield-target-exclude.ls
- dshield-source-port-exclude.lst
- dshield-target-port-exclude.lst

您可以修改这些文件来过滤掉本会被报告的日志记录。您可以根据 IP 地址、目标 IP 地址、源端口或目标端口进行过滤。地址和端口可以单独指定（每行一个）或指定范围。有关 DShield 配置指令的更多信息，请参见配置文件中的注释。

## 运行 DShield

DShield 不应配置为持续运行。将其作为每小时一次的 Cron 任务运行通常是最理想的。为此创建 `/etc/cron.hourly/dshield` 文件并包含以下内容：

```
#!/bin/sh
```

# 发邮件到 dshield.org，总结来自
# /var/log/messages 的 snort 警报。

```
#/usr/local/bin/iptables.pl
```

然后，赋予 root 用户该文件的执行权限。一小时后，登录 DShield 网站并查看您的“最近提交”（Recent Submissions）页面。验证页面是否正确反映了最近的系统活动，并调整配置文件以解决问题。

![](img/0f69b2a8749a24b957044e9f26f2d5b_431_0.png)

如果您的浏览器配置了缓存网页，您可能需要清除缓存才能查看“最近提交”页面的最新版本。

## Portsentry

Portsentry 是一个简单的入侵检测系统，可以配置监控未使用的端口。当远程主机访问受监控的端口时，Portsentry 会记录该事件。可选情况下，Portsentry 还可以：

- 将故障主机添加到 `/etc/hosts.deny` 文件，从而配置 TCP wrappers 来阻止访问受 TCP wrappers 保护的服务。
- 重新配置防火墙以阻塞来自故障主机的所有访问。

机攻击者可能会伪造 IP 地址以诱导 Portsentry 阻塞重要主机的访问。Portsentry 的配置选项包含一个文件，允许您识别信任主机，并忽略来自这些主机的明显攻击。

## 配置 Portsentry

Portsentry 需要 libcap RPM 包，它是 Red Hat Linux 发行版的一部分。尚未安装 libcap，应在安装 Portsentry 之前安装。您可以从 http://www.psionic.com/products/index.html 下载 Portsentry 的 TAR 包。下载文件后，使用如下命令进行解压：

```bash
tar zf portsentry-2.0b1.tar.gz
```

其中 `portsentry-2.0b1.tar.gz` 是下载的文件名。> 提示 Portsentry 曾作为 Red Hat Powertools 发布的一部分。然而，最好通过网络下载最新版本的 Portsentry。

一旦下载了文件，将工作目录更改到 `tar` 命令创建的目录。在那里，你会发现大约两个文件。其中包括：

- Makefile：用于编译和安装 Portsentry。
- portsentry.conf：Portsentry 配置文件。
- portsentry.ignore：识别不应归类为攻击者的主机和网络。
- README.install：包含详细安装说明。

准备编译和安装 Portsentry 请执行以下步骤：

1. 修改 Makefile，将文件顶部的
```
CFLAGS = -O -Wall
```
替换为
```
CFLAGS = -O -Wall -I/usr/include
```

2. 修改 portsentry.conf，将文件顶部的
```
INTERFACE="auto"
```
替换为
```
INTERFACE="eth0"
```
其中 `eth0` 是 Portsentry 应该监听的网络接口。还将将
```
INTERFACE_ADDRESS="XXX.XXX.XXX"
```
替换为指定网络接口的 IP 地址，例如：
```
INTERFACE_ADDRESS="192.0.34.72"
```
您还应该检查 `TCP_PORTS` 和 `UDP_PORTS` 中的值，移除与本地主机运行的所有端口。

3. 修改 portsentry.ignore 文件，添加您不希望被视为攻击者的主机 IP 地址。可以使用第 2 章说明的 CIDR 符号指定整个网络。portsentry.ignore 文件至少应：

- 本地网络 127.0.0/24
- 与本地接口相关的 IP 地址
- 路由器的 IP 地址

如果指定的条目过多，Portsentry 可能无法报告实际攻击。但是，如果指定的条目太少，Portsentry 可能会因误封重要主机而导致您的网络中断。

## 构建并安装 Portsentry

要构建 Portsentry，执行这些命令：

```bash
make
make install
```

## 运行 PORENTRY

启动 Portsentry，执行命令：

```
/usr/local/psionic/portsentry
```
