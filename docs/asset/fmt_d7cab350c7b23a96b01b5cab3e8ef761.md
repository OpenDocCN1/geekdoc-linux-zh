
## 使用 fsnort 和 psad 破坏 Metasploit 更新

配备了新的 Snort 规则后，我们可以使用 `fsnort` 和 `psad` 来识别并停止由 `svn update` 或 `msfupdate` 命令发起的 SSL 会话。当然，我们的规则不会停止更新 Metasploit 的其他方法，例如通过 SSH 对具有已更新数据库的外部机器进行 `rsync`。此外，除非发现 SSL 会话，否则我们不会部署可能干扰基本 DNS 查询或对 `metasploit.com` Web 请求的 `fsnort` 或 `psad` 响应。

如前所述，让 `fsnort` 停止 Metasploit 更新过程的第一步是将我们的新 Snort 规则翻译成等效的 `iptables` 规则。为此，我们将 `metasploit.rules` 文件复制到 `/etc/fsnort/snort_rules` 目录并运行 `fsort`。由于我们专注于停止 Metasploit 更新，我们使用 `--ipt-reject` 命令行参数：

```
iptablesfw# cp metasploit.rules /etc/fsnort/snort_rules

iptablesfw --fsnort --sid 90001 --ipt-reject

# Parsing Snort rules files...

# Found: 90001 in metasploit.rules

Successful translation

# logfile: /var/log/fsnort.log

iptables script: /etc/fsnort/fsnort.sh
```

虽然我们有信 `iptables` 不允许与 `metasploit.com` Web 服务器的单个 SSL 会话成功，但我们仍然希望在会话关闭时创建持久的 `iptables` 规则。为了实现这一点，我们通过在 `/etc/psad/psad.conf` 中设置以下配置变量来使用 `psad` 的自动阻塞功能：

```
ENABLE_AUTO_IDS      Y;

AUTO_IDS_DANGER_LEVEL 4;

AUTO_BLOCK_TIMEOUT    3600;

ENABLE_AUTO_IDS_REGEX  Y;

AUTO_BLOCK_REGEX      ESTAB;
```

接下来，我们让 `psad` 识别到新的 `metasploit.rules` 文件。为此，我们向 `/etc/psad/snort_rule.dl` 文件中添加一个条目，将 Snort 规则 ID `900001` 映射到危险级别 `4`（这样 Metasploit 更新过程就会触发 `AUTO_IDS_DANGER_LEVEL` 阈值）：

```
[iptablesfw]# cp /etc/fwsnort/snort_rules/metasploit.rules /etc/psad/
snort_rules
[iptablesfw]# echo "900001 4;" >> /etc/psad/snort_rule_dl
[iptablesfw]# /etc/init.d/psad start
* Starting...
```

现在，我们尝试从 `int_scanner` 客户端系统更新 Metasploit 漏洞数据库如下：

```
[int_scanner]$ cd framework-3.0
[int_scanner]$ svn update
svn: PROPPIND request failed on /svn/framework3/tags/framework-3.0
svn: PROPPIND of /svn/framework3/tags/framework-3.0: SSL negotiation failed: Connection reset by peer (<?metasploit.com>)
```

我们在 `iptables` 系统的 `syslog` 中看到了写入的以下消息。第一条消息表明 `fwsn` 规则已通过 TCP 重置包丢弃了 SSL 会话。随后的消息显示 `psad` 已针对 `metasploit.com` IP 地址 `216.75.15.231` 实例化了一个一小时的阻塞规则：

```
Jul 31 17:42:14 iptablesfw kernel: REL SID900001 ESTABLISHED IN=eth0 OUT=eth1
SRC=216.75.15.231 DST=192.168.10.200 LEN=1500 TTL=50 TCP=0x00 DX=0x00 TLE=77 ID=19762
PROTO=TCP SPT=443 DST=38528 WINDOW=64 RES=0x00 ACK=URGP=0
Jul 31 17:42:14 iptablesfw psad: src: 216.75.15.231 signature match: "Metasploit
exploit DB "update" (sid: 900001) tcp port: 38528 fwsnort: FORWARD
ESTAB rule: 1
Jul 31 17:42:14 iptablesfw psad: detected: 216.75.15.231 -> 192.168.10.200
tcp: [38528] flags: ACK tcp pkts: 1 DL: 4
Jul 31 17:42:14 iptablesfw psad: added iptables auto-block against 216.75.15.231
for 3600 seconds
```

结合 `psad` 和 `fwsnort` 209

## 注意

由于你的 Snort 规则检测到来自 `443` 端口的 Metasploit SSL 证书，`psad` 将流量的源视为连接的服务器端而不是客户端。因此，被 `iptables` 拦截的是 `metasploit.com` 的 IP 地址 `216.75.15.231`，而不是内部网络上的 IP 地址 `192.168.10.200`。`psad` 的后续版本将允许你定义是阻塞与 `fwsnlog` 日志相关的源 IP 还是目的 IP。尽管如此，你仍然可以通过上述“检测到扫描”的 `syslog` 消息识别出尝试 Metasploit 更新的客户端。

我们将在本章包含一封来自 `psad` 的关于尝试 Metasploit 更新细节的精彩邮件（完整格式见下）：

```
From: <root@cipherdyne.org>
Subject: [psad-alert] D4 src: metasploit.com dst: int_scanner
To: mbr@cipherdyne.org
Date: Thu, 31 Jul 2008 17:42:14-0400 (EDT)
```
