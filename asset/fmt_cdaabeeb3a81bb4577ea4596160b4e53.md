
`chmod go-rwx`

`rm foo`

`crontab -l > foo`

接下来，决定一个在 `crontab` 调用你的恢复脚本 `rc.fw.offsafe` 之前你能够忍受等待的平均时间。还要决定你测试“真实”防火墙脚本需要多久。通常情况下，我测试的内容不起作用。我会发现失败的原因是 `cronab` 将系统恢复回了安全模式。如果在密集开发期间，10 分钟的平均等待时间是有效的

将这 10 分钟翻倍，因为从统计上看，挂起通常发生在两次 `cronab` 调用之间。因此，`crontab` 条目应该每 20 分钟调用一次。以下命令将添加正确的：

```
cd /root

echo "0,20,40 * * * * /etc/rc.d/rc.fw.offsafe \"

  > /dev/null 2>&1 >> foo

crontab foo

/bin/rm foo
```

### 12. 按时间更改规则

计算机安全的核心在于降低风险，即降低某些事件发生的概率。任何特定的黑客都可能只尝试攻击你系统的一个或多个端口一次，如果他的扫描程序没有发现任何有趣的内容，他很可能再也不会打扰你了。毕竟，互联网上上有 100,000,000 个系统供他尝试。即使管理层允许员工在白天居家办公，但在凌晨 3 点，会有多少人在居家办公并需要访问公司所有的内部系统呢？然而，大多数公司会允许 24 小时 7 天不间断的访问和远程攻击。这为攻击、暴力破解密码和类似的漏洞创造了大量机会。

为什么会有这些风险？简单来说，在不需要时关闭不必要的访问。假设 Web 管理员在白天工作，但很少在办公时间之外工作，并且假设你是一个电子商务网站，因此 Web 服务器的安全至关重要。可以使用 `date` 程序来确定当前的小时和星期几。我们将允许在早上 8 点到下午 5:59 之间通过 SSH 访问 Web 服务器。修改 `/etc/rc.fw` 脚本可以实现此功能：添加 `/etc/rc.fw`

```bash
#!/bin/sh

IPT=/sbin/iptables

EXTIF=eth0

hour="/bin/date +%h"

dayw="/bin/date +%w"

# 在工作日期间允许访问 Web 服务器 SSH

# if [ $hour -ge 8 -a $dayw -le 17 ]; then

  -A FORWARD -i $EXTIF -p tcp \
-d www.pentacorp.com \
  --dport 22 -j ACCEPT

  -A FORWARD -o $EXTIF -p tcp \
-s www.pentacorp.com \
  --sport 22 --syn -j ACCEPT

fi
```

此脚本可以在周一至周五的早上 8 点和下午 6 点（0800 和 1800 小时）调用，通过以下更新 root `crontab`：

```bash
cd /root

crontab -l > foo

echo "0 8,18 * 1-5 /etc/rc.d/rc.fw \" \
  /dev/null 2>>&1" >> foo

crontab foo

/bin/rm foo
```

## 13. 通过 VPN 路由 DMZ 流量

大多数用户和系统管理员很少考虑他们的邮件是在互联网上以明文传输的，且不应包含机密信息。即使是那些知道这一点并很谨慎的人，可能也假设发送给公司内部其他人的邮件是机密的。当然，如果他们知道不同办公室之间有 VPN，邮件就会通过 VPN 传输。不是吗？咳，额，好吧，可能不是。

通常，VPN 是设置到每个办公室的内部 IP 掩码网络（NAT）的。然而，通常总部的 DMZ 中有一个邮件服务器，例如 `mail.pentacorp.com`，那么当分支机构的用户向员工发送邮件或获取其邮件时，由于它不是总部私有网络中的 IP，因此它不会通过 VPN 路由。相反，它将以明文形式在互联网上传传输，任何人都可以看到。

与其说是防火墙问题，不如说是路由问题。奥尔尼办公室防火墙上的 VPN 接口是 `ppp0`，只需添加命令：

```bash
/sbin/route add -host mail.pentacorp.com dev ppp0
```

显然，这将导致所有发往公司邮件服务器的数据包从奥尔尼办公室发送到 VPN。当它们在总部弹出时，它们仍然带有 `mail.pentacorp.com` 的目的地址，那里的 VPN 应该将它们路由到 DMZ。响应数据包的目的地址是内部系统，并将自动通过 VPN 返回。我们漏掉了什么吗？

好吧，如果 VPN 掉线，接口就会消失，我们刚刚添加的路由也会之消失。到邮件服务器的数据包将开始以明文在互联网传输。我们可能需要通过拒绝此类数据包来防止这种情况。奥尔尼办公室的以下行可以实现这一点：

```bash
EXTIF=eth0

/sbin/iptables -A FORWARD -o $EXTIF \
-d mail.pentacorp.com -j REJECT

/sbin/iptables -A OUTPUT -o $EXTIF \
-d mail.pentacorp.com -j REJECT
```

## 14. 查看 IP 链规则对特定数据包的作用

IP 链 `-c` 选项允许检查特定数据包将如何处理。它有助于将问题缩小到特定的链。大多数应用程序涉及两个链，每个链至少经过两条链。测试到 Web 服务器的流量，可以如下：

```bash
IPC=/sbin/iptchains

$IPC -C input -i eth0 -p tcp -y -s 1.2.3.4 1025 -d www.penta-corp.com 80
```

# 490 第 12 章 · 加固你的系统

## 20. 为具有多个 IP 地址的主机构建规则

获取主机名完整 IP 地址列表的首选方法是使用 `dig` 或 `nslookup` 命令并将主机名作为参数，然后查看输出中的 answer（回答）部分。。对于一个有趣的案例，请尝试：

```bash
dig www.yahoo.com
```

你不仅会获得很多 IP 地址，远在 1000 英外的伙伴也会获得不同的 IP 地址。15 这是 Bourne shell 命令的一个很好的应用。以下示例说明了这一点：

```bash
IPT=/sbin/iptables

EXTIF=eth0

BIGWW*="64.58.76.178 64.58.76.176 64.58.76.225"

for i in $BIGWW;

dn Rules

done
```
