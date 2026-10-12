
列表 416：在 Kali Linux 中启动 BeEF 服务

我们可以使用默认密码 `beef/beef` 访问 `http://127.0.0.1:3000/ui/panel` 并登录框架的主界面。

| 身份验证 |  |
|---|---|
| 用户名: | beef |
| 密码: | **** |

图 258：BeEF 主登录页面

登录后，我们需要挂钩（hook）一个目标浏览器。由于高级挂钩超出了本模块的范围，我们将通过点击高亮的演示页面链接使用框架提供的演示页面。这将允许 BeEF 挂钩我们的浏览器。

## 已挂钩浏览器

一旦浏览器被挂钩，它将出现在左侧的“挂钩浏览器（Hooked Browsers）”面板中。根据它们请求框架的时间，挂钩浏览器将显示在线或离线状态。

# 攻击性安全
www.offensivesecurity.com

Kali Linux 2.0 渗透测试

## 14.2.2.4 Metasploit 框架

```
kali@kali:~ sudo msfconsole -q
```

列表 417 - 启动 Metasploit 框架

该框架的使用将在另一个模块中介绍，因此我们将简单地关注于使用 `search` 命令列出框架内的漏洞利用程序（exploits）。

为了进行演示，请考虑对流行的 MS08_067 漏洞进行如下搜索：

```
msf > search ms08_067
```

### 匹配模块

| Name | Disclosure Date | Description |
|---|---|---|
| exploit/windows/smb/ms08_067_netapi | 2008-10-28 | MS08_067 Microsoft Server Relative Path Stack Corruption |

列表 418 - 在 Metasploit 中搜索 ms08_067 漏洞

> ^376 (Rapid, 2019), https://www.metasploit.com
> ^377 (Microsoft, 2019), https://docs.microsoft.com/en-us/security-updates/securitybulletins/2008/ms08-067

Metasploit 搜索命令包含许多关键词，帮助我们找到特定的漏洞利用程序。
要列出所有选项，请配合 `-h` 选项运行 `search`：

```
msf5 > search -h

Usage: search [ options ] <keywords>
```

OPTIONS：

- `-h` 显示帮助信息
- `-o <file>` 将输出发送到 csv 格式的文件
- `-S <string>` 用于行过滤的搜索字符串
- `-u` 如果只有一个结果，则使用该模块

关键词：

- `aka` 具有匹配 AKA（别名）名称的模块
- `author` 由此作者编写的模块
- `arch` 影响此架构的模块
- `bid` 具有匹配 Bugtrag ID 的模块
- `cve` 具有匹配 Exploit ID（漏洞利用程序标识符）的模块
- `edb` 支持 'check' 方法的模块
- `check` 具有匹配发布日期的模块
- `date` 具有匹配描述的模块
- `full_name` 具有匹配全称的模块
- `mod_time` 具有匹配修改日期的模块
- `name` 具有匹配性名称的模块
- `path` 具有匹配路径的模块
- `platform` 影响此平台的模块
- `port` 具有匹配端口的模块
- `rank` 具有匹配排名（可以是描述性的：如 'good'）或名称的模块
- `ref` 具有匹配 ref 的模块
- `reference` 具有匹配引用的模块
- `target` 影响此目标的模块
- `type` 特定类型的模块（exploit, payload, auxiliary, encoder, we）

示例：
`search cve:2009 type`

## 14.3 整合实战

在涵盖了所有资源后，让我们演示一下在真实场景中将会是。我们将攻击专用 Linux 内核，该内核托管了一个存在公共漏洞的应用。

我们通过运行 `nmap` 开始枚举过程，以确定机器向网络暴露了哪些服务：

```
kali@kali:~ sudo nmap 10.11.0.128 -p - -sV -vv --open --reason

...
Scanning 10.11.0.128 [ports]

Discovered open port 3389/tcp on 10.11.0.128

Discovered open port 118/tcp on 10.11.0.128

Discovered open port 25/tcp on 10.11.0.128

Discovered open port 22/tcp on 10.11.0.128
```

Discovered open port 119/tcp on 10.11.0.128
Discovered open port 4555/tcp on 10.11.0.128
Completed SYN Stealth Scan at 14:23, 49.03s elapsed (65535 total ports)
Initiating scan at 14:22
Scanning 6 services on 10.11.0.128
Completed scan at 14:23, 11.47s elapsed (6 services on 1 host)
NSE: Script scanning 10.11.0.128.

Nmap scan report for 10.11.0.128
Host is up, received arp-response (0.15s latency).
Scanned from 2019-04-13 14:22:57 EEST for 6 hosts
Not shown: 65304 closed ports, 225 filtered ports
Reason: 65534 requests and 220 non-responses

某些关闭的端口被报告为过滤，由于 ---defeat-ratelimit

| PORT | STATE | REASON | VERSION |
|---|---|---|---|
| 22/tcp | open | | |
| 25/tcp | open | | |
| 118/tcp | open | | |
| 119/tcp | open | | |
| 3389/tcp | open | | |
| 4555/tcp | open | | |
