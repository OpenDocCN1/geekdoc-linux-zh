
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
-s $IPADDR --port 22 \
--dport SSH_PORTS -j ACCEPT

fi

```
```bash
####################################################################
# ftp (TCP 端口 21, 20)
```
## 本地客户端到远程服务器的出的请求
```bash
# 发往端口 21 的控制连接
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport 21 -m state --state NEW -j ACCEPT
fi
```
```bash
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport 21 -j ACCEPT
```
```bash
$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
--port 21 \
-d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```
```bash
# 来自端口 20 的进入端口模式数据通道连接
if [ "$CONNECTION_TRACKING" = "1" ]; then
# 如果使用了 ip_conntrack_ftp
# 模块，则此规则是不必要的。
$IPT -A INPUT -i $INTERNET -p tcp \
--port 20 \
-d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
fi
```
```bash
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport 20 -j ACCEPT
```
```bash
# 非权端口之间的出的被动模式数据通道连接
if [ "$CONNECTION_TRACKING" = "1" ]; then
# 如果使用了 ip_conntrack_ftp
# 模块，则此规则是不必要的。
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport $UNPRIVPORTS -m state --state NEW -j ACCEPT
fi
```
```bash
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport $UNPRIVPORTS -j ACCEPT
```
## 第 5 章中独立系统的 iptables 防墙
```bash
$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
--sport $UNPRIVPORTS \
--d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```
## 远程客户端到本地服务器的进入请求
```bash
if [ "$FTP_SERVER" = "1" ]; then
```
```bash
# 端口 21 的进入控制连接
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
--d $IPADDR --dport 21 \
--m state --state NEW -j ACCEPT
fi
```
```bash
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
--d $IPADDR --dport 21 -j ACCEPT
```
```bash
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
-s $IPADDR --dport 21 \
--dport $UNPRIVPORTS -j ACCEPT
```
```bash
# 发往端口 20 的端口模式数据通道连接
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --dport 20 \
--dport $UNPRIVPORTS -m state --state NEW -j ACCEPT
fi
```
```bash
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --dport 20 \
--dport $UNPRIVPORTS -j ACCEPT
```
```bash
$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
--sport $UNPRIVPORTS \
--d $IPADDR --dport 20 -j ACCEPT
# 非权端口之间的进入被动模式数据通道连接
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
--d $IPADDR --dport $UNPRIVPORTS \
--m state --state NEW -j ACCEPT
fi
```
```bash
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
--d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```
```bash
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
-s $IPADDR --dport $UNPRIVPORTS -j ACCEPT
fi
```
## 324 附录 B 防墙示例与支持脚本
```bash
############################
# HTTP 流量 (TCP 端口 80)
# 本地客户端到远程服务器的出的请求
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport 80 -m state --state NEW -j ACCEPT
fi
```
```bash
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport 80 -j ACCEPT
```
```bash
$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
--sport $UNPRIVPORTS \
--d $IPADDR --dport 80 -j ACCEPT
```
## 远程客户端到本地服务器的进入请求
if [ "$WEB_SERVER" = "1" ]; then
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
--d $IPADDR --dport 80 \
--m state --state NEW -j ACCEPT
fi
```
```bash
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
--d $IPADDR --dport 80 -j ACCEPT
```
```bash
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
-s $IPADDR --sport $UNPRIVPORTS \
--dport 80 -j ACCEPT
fi
```
