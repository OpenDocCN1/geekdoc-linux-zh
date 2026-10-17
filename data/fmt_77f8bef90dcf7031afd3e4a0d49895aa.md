
应该就是全部内容了。第一次获取将传输一个可用新闻组列表。随后 `Leafnode` 将监控用户请求的组，并在下次激活时适应这些请求。

ALT：`leafnode` 的替代方案是 `nntpcache`，下载地址为：

`ftp://ftp.suburbia.net/pub/nntcache/nntcache.tgz`

## 6 我如何自动化连接过程？

在 Linux 中实现新闻和邮件的自动化处理非常简单。

首先，应该创建一个 `/usr/lib/ppp/ppp-on` 脚本来启动 ISP 连接。通常，该文件仅包含以下内容：

```
/usr/sbin/pppd
```

进一步的将在 `/etc/ppp/options` 中完成：

```
connect "usr/lib/ppp/chat -v f /etc/ppp/chatscript"
crtscts
modem
defaultroute
asyncmap 00000000
user dirk
/dev/modem 38400
```

要结束连接，请使用提供的 `/usr/lib/ppp/ppp-off` 版本。

在测试了这两个脚本的功能后，必须编写执行各种任务的脚本。收集邮件的脚本之前描述过，我们在此假设它位于 `/home/dirk/pop`。

随后可以在 `/root/mail` 创建一个交换邮件的脚本：

```
# /bin/sh
#
# 交换邮件
# 10分钟超时：
TIMEOUT=600
DT=10

# 启动 sendmail:
sendmail -q &

# 获取邮件:
su dirk -c /home/dirk/pop

# 等待 sendmail 终止:
t=0
while mailq | grep -q "Mail queue is empty"; do
    t=$[$t+$DT]
    if [ $t -gt $TIMEOUT ]; then
        echo "sendmail -q ($TIMEOUT)"
        exit 1
    fi
    sleep $DT
done
exit 0
```

交换新闻的脚本可以存放在 `/usr/lib/news/news`：

```bash
#!/bin/sh
#
# 交换新闻
# 必须以 news 身份运行:
cd /usr/lib/news

# 更新传出的批 (C News):
/usr/lib/newsbin/input/newsrun < /dev/null

# 交换新闻:
/usr/lib/newsbin/news acme.acme news.acme

# 并冲刷传入的批:
/usr/lib/newsbin/input/newsrun < /dev/null
```

还需要一个连接各个部分的脚本，可以存放在 `/root/news+mail`：

```bash
#!/bin/sh
#
# 交换新闻和邮件
# 必须以 root 身份运行
#
if ! /usr/lib/ppp/ppp-on; then
    exit 1
fi

trap "/usr/lib/ppp/ppp-off" 1 2 3 15

# 交换新闻+邮件:
/root/mail &
su news -c "news/news"
wait

# 断开连接..
/usr/lib/ppp/ppp-off

# 更新导入的批 (C News):
su news -c /usr/lib/newsbin/input/newsrun < /dev/null &
exit 0
```

对上述内容进行扩展非常容易，仅在有传出的邮件和新闻时才建立连接。我们称之为 `/root/news+mail.cond`，并请注意传出的新闻队列名称必须更新以适应之：

```bash
#!/bin/sh
#n# 交换新闻和邮件，仅当有传出的新闻或邮件时
# (C News队列)
if [ -s /var/spool/news/output.going/acme/ ] || \
! ( mailq | grep -q "Mail queue is empty"); then
    /root/news+mail
fi
```

剩下的最后一件事是指定何时发生。这是通过 `crontab -e root` 命令完成的。假设我们希望每天早上 07:00 以及每隔 4 小时交换新闻和邮件（假设有传出的邮件和新闻）。

```
00 07 * * * /root/news+mail
00 11,19,23 * * * /root/news+mail.cond
```

在将它们连接在一起之前，确保每个组件都经过了测试。后来可以添加若干任务，例如调整时间（使用 `nptime`），以及将本地 `WWW` 和 `FTP` 文件自动镜像到 ISP（使用 `make` 和 `ftp`）。

ALT：在偏好中，也可以关闭此过程。每当启动 `PPP` 链路时，都会启动 `/etc/ppp/ip-up` 脚本。可以添加一个需要“魔法”来启动邮件和新闻交换的脚本。更多细节请参见 `man pppd`。

ALT：也可以在检测到网络流量时自动连接 `PPP`。这在许多方面是最优雅的解决方案，但它非常取决于良好的配置，以避免频繁（且昂贵的）连接。更多信息可以在此处找到：

```
http://www.dna.lth.se/erics/dial.html
```

`dial` 工具可用：

```
ftp://sunsite.unc.edu/ppp/Linux/system
```
