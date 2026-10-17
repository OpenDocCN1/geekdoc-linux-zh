
以下规则进入 `/etc/ipfw.rules`

```
############################################
# 在开始之前清空列表。
ipfw -f flush

# 设置规则命令前缀
cmd="ipfw -q add"
pif="dc0"      # 网卡的公共接口名称
                    # 面向公用互联网

############################################
# 对私有网络的内部 LAN 接口无限制
# 除非你有 LAN，否则不需要
# 将 x10 修改为你的 LAN 网卡接口名称
#$cmd 00005 allow all from any to any via x10

############################################
# 对环回接口无限制
############################################
$cmd 00010 allow all from any to any via lo0

############################################
# 如果数据包之前已经被 allow keep-state 语句
# 添加到“动态”规则表，则允许其通过。
################################################################
$cmd 00015 check-state

################################################################
# 面向公用互联网的接口（出站部分）
# 处理源自防火墙后私有网络或此网关
# 通往公用互联网的会话请求。
################################################
# 允许访问 ISP 的域名服务器。
# x.x.x 必须是你 ISP 的 IP 地址。
# 如果你的 ISP 有多个服务器，
# 复制这些行并从 /etc/resolv.conf 获取 IP 地址
$cmd 00110 allow tcp from any to x.x.x 53 out via $pif keep-state
$cmd 00110 allow udp from any to x.x.x 53 out via $pif keep-state

# 允许访问电缆/DSL 的 DNS 服务器。
# 对于用户 ppp 连接不需要此规则，
# 你可以删除整个组组。
# 使用以下规则并将 IP 地址放在范围之前。
$cmd 00120 allow tcp from any to 80 out via $pif keep-state

# 允许标准 www 功能
$cmd 00200 allow tcp from any to 80 out via $pif keep-state

# 允许通过 SSL 的安全 Web 功能
$cmd 00220 allow tcp from any to 443 out via $pif keep-state

# 允许发送邮件功能。
$cmd 00230 allow tcp from any to 25 out via $pif keep-state

# 允许 FTP（安装 & CVS 功能）
$cmd 00231 allow tcp from any to 110 out via $pif keep-state

# 基本上赋予 root 权限。
# 这是使用 SSH（安全外）
$cmd 00240 allow tcp from me to any out $pif keep-state

# 允许出 ping
$cmd 00250 allow icmp from any to any via $pif keep-state

# 允许出 Time
$cmd 00260 allow tcp from any to 37 out via $pif keep-state

# 允许出 ntp（例如新闻组）
$cmd 00270 allow tcp from any to any 119 out via $pif keep-state

# 允许安全的 FTP, Telnet 和 SCP
$cmd 00280 allow tcp from any to 22 out via $pif keep-state

# 允许出 whois
$cmd 00290 allow tcp from any to 43 out via $pif keep-state

# 阻止并日志其他尝试出站的内容。
# 该规则执行默认阻止逻辑。
$cmd 00299 deny log all from any to any via $sip

################################################
# 面向公用互联网的接口（入站部分）
# 处理源自公用互联网的
# 网关服务器或私有网络。
################################################
# 阻止来自不可路由地址空间的入站流量
$cmd 00300 deny log any from 192.168.0.0/16 to any via $pif #RFC 1918 私有 IP
$cmd 00301 deny log any from 172.16.0.0/16 to any via $pif #RFC 1918 私有 IP
$cmd 00302 deny log any from 10.0.0.0/8 to any via $pif #RFC 1918 私有 IP
$cmd 00303 deny log any from 127.0.0.0/8 to any via $pif #环回
$cmd 00304 deny log any from 0.0.0.0/8 to any via $pif #环回
$cmd 00305 deny log any from 169.254.0.0/16 to any via $pif #DHCP 自动配置
$cmd 00306 deny log any from 192.0.2.0/24 to any via $pif #预留文档
$cmd 00307 deny log any from 203.0.113.0/24 to any via $pif #Sun 集群互连
$cmd 00308 deny log any from 224.0.0.0/3 to any via $pif #D 类 & 多播

# 阻止公用 ping
$cmd 00310 deny icmp from any to any via $pif

# 阻止 ident
$cmd 00315 deny tcp from any to any 113 via $pif

# 阻止所有 Netbios 服务。137=name, 138=datagram 139=session
# Netbios 是 MS/Windows 共享服务。
# 阻止 MS/Windows 主机名请求
$cmd 00320 deny tcp from any to any 137 via $pif
$cmd 00321 deny tcp from any to any 138 via $pif
$cmd 00322 deny tcp from any to any 139 via $pif
$cmd 00323 deny tcp from any to any 81 via $pif

# 阻止任何延迟到达的数据包
$cmd 00330 deny all from any to any frag via $pif

# 允许 ISP 的 DHCP 服务器中的流量。此规则必须包含
# 你 ISP 的 DHCP 服务器的 IP 地址，因为它是发送
# 此数据类型的唯一授权源。
# 仅对电缆或 DSL 配置必要。
# 对于用户 ppp 连接不需要此规则，
# 连接到你在出站部分捕获
# 并使用的相同的 IP 地址。
$cmd 00360 allow udp from any to x.x.x 67 in via $sip keep-state

# 允许标准 Web 功能，因为我有 apache 服务器
$cmd 00400 allow tcp from any to me 80 in via $sip setup src-addr 2

# 允许从公用互联网进入安全的 FTP, Telnet 和 SCP
```

# 第 26 章 防墙

```bash
$cmod 00410 allow tcp from any to me 22 via $pif setup limit src-addr 2
```

# 允许来自公共互联网的非安全 Telnet 会话

# 标记为非安全的 ID 和密码将以明文形式在公网上上传输。

# 如果你没有启用 telnet，请删除此示例组。

$cmod 00420 allow tcp from any to me 23 in via $pif setup limit src-addr 2
