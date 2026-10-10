
## 本地网络配置

`acl localnet 10.0.0.0/8` # RFC 1918 local

private network (LAN)

--snip--

## 允许从本地网络访问的示例规则

根据需要列出你的（内部）IP 网络，这些网络应允许浏览

```bash
acl localnet src 0.0.0.1-0.255.255.255 # RFC 1122 "this"
network (LAN)
acl localnet 10.0.0.0/8 # RFC 1918 local
private network (LAN)
--snip--
```

The next section of the configuration file relates to your local network as opposed to the internet:

```bash
--snip--
## 允许从本地网络访问的示例规则。
# 根据需要在 ACL 部分中列出你的（内部）IP 网络，
## 这些网络应允许浏览
#http_access allow localnet
http_access allow localhost
# 最后拒绝对此代理的所有其他访问
http_access deny all
--snip--
```

## 监听端口配置

If you want to change the port on which Squid listens for requests, modify the following line in your configuration file:

```bash
--snip--
# Squid 正常监听端口 3128
http_port 3128
--snip--
```

Your devices will use this port to connect to the proxy server so they can send requests, receive traffic, and generally browse the internet.

Once you've finished your edits, save and close the configuration file. Reload the updated Squid configuration using the following command so the changes take effect (be aware, though, reloading the configuration can interrupt any open connections):

```bash
$ sudo systemctl reload squid
```

You can now make sure that Squid was able to start successfully and is running with the following command:

```bash
$ sudo systemctl status squid
squid.service - Squid Web Proxy Server
Loaded: loaded (/lib/systemd/system/squid.service)
enabled; vendor preset: enabled
Active: active (running); 2min 5s ago
--snip--
```

`squid.service` 前面有一个绿点且状态为 `active (running)` 表示 Squid 正在按预期运行。如果 Squid 由于错误未能正常启动，你将看到 `squid.service` 前有一个红点并显示 `failed` 消息：

```bash
$ sudo systemctl status squid
squid.service - Squid Web Proxy Server
Loaded: loaded (/lib/systemd/system/squid.service)
enabled; vendor preset: enabled
Active: failed (Result: exit-code); 2min 5s ago
--snip--
```

返回并检查您的配置，或使用此命令验证您的配置文件：

```bash
$ squid -k parse
2024/05/06 00:44:06| Processing: acl denylist dstdomain 
.twitter.com
2024/05/06 00:44:06| Processing: http_deny denylist
2024/05/06 00:44:06| /etc/squid/squid.conf:1406
unrecognized: 'http_deny'
2024/05/06 00:44:06| Processing: anonymous_headers deny 
From Referrer Server
2024/05/06 00:44:06| /etc/squid/squid.conf:1408
unrecognized: 'anonymize_headers'
2024/05/06 00:44:06| Processing: anonymous_headers deny 
User-Agent Ww-Authenticate
2024/05/06 00:44:06| /etc/squid/squid.conf:1409
unrecognized: 'anonymize_headers'
2024/05/06 00:44:06| Processing: http_access allow localnet
--snip--
```
