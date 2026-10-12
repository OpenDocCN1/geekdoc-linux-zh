
暴力破解是一种通过尝试错误来寻找有效信息的技术，包括 Web 服务器上的目录、用户名和密码组合，或者在本例中是有效的 DNS 记录。通过使用包含常用主机名的字典列表，我们可以尝试猜测 DNS 记录并检查响应以获取有效的主机名。

在之前的示例中，我们进行的是正向查找，即请求主机名的 IP 地址，并查询了有效和无效的主机。我们可以在 Bash 命令行中使用 `host` 命令自动化常用主机名的正向 DNS 查找。

首先，构建一个可能的主机列表：

```
kali@kali:-$ cat list.txt
www
ftp
mail
owa
proxy
router
```

> 列表 214 - 一个可能的主机的小列表

接下来，我们使用 Bash 命令行解析每个主机名：

```
kali@kali:-$ for ip in $(cat list.txt); do host $ip.megacorpome.com; done
.megacorpome.com has address 38.108.193.76
Host megacorpome.com not found: 3(NXDOMAIN)
mail.megacorpome.com has address 38.108.193.84
owa.megacorpome.com not found: 3(NXDOMAIN)
Host proxy.megacorpome.com not found: 3(NXDOMAIN)
router.megacorpome.com has address 38.108.193.71
```

> 列表 215 - 使用暴力破解进行 DNS 查找

通过这种简单的方法，我们发现了 'www'、'mail' 和 'router' 的条目。主机 'ftp'、'owa' 和 'proxy' 未被找到。更全面的字典列表可以通过 Seclists 项目获取。这些字典可以安装到 `/usr/share/seclists` 目录。

## 7.1.4 反向查找暴力破解

我们的 DNS 暴力破解枚举揭示了 `38.100.x` 范围内的 IP 地址。如果 `megacorpome.com` 配置了 PTR 记录，我们就可以通过反向查找获取该范围的主机名。现在我们使用循环和 `grep` 来过滤掉无效的结果：

```
kali@kali:~$ for ip in $(seq 50 100); do host $ip.38.100.in.arpa; done | grep -v "found"
69.100.in.arpa pointer beta.megacorp.com.
70.100.in.arpa pointer mail.megacorp.com.
71.100.in.arpa pointer admin.megacorp.com.
72.100.in.arpa pointer mail2.megacorp.com.
73.100.in.arpa pointer megacorp.com.
74.100.in.arpa pointer www.megacorp.com.
75.100.in.arpa pointer vpn.megacorp.com.
```

> 列表 216 - 使用暴力破解进行反向查找

我们通过反向查找成功解析了一组 IP 地址。如果 `megacorpome.com` 配置了 MX 记录，我们就可以扫描这些 IP。

## 7.1.5 DNS 区域传输

区域传输（Zone Transfer）基本上是将 DNS 从主服务器复制到从服务器。区域传输应该只允许授权的 DNS 服务器进行，但在许多情况下，它们可能被配置错误，允许任何人进行查询。执行区域传输的语法如下：

```
host -l <domain>
```

> 列表 217 - 使用 host 执行 DNS 区域传输

从我们的列表 210 中，我们注意到 `megacorpome.com` 有三个 DNS 服务器：`ns1`、`ns2` 和 `ns3`。让我们尝试对每一个进行区域传输：

```
kali@kali~~$ host -l megacorpome.com ns1.megacorpome.com
Using domain server:
Name: ns1.megacorpome.com
Address: 38.100.193.70#53
Aliases:
Host megacorpome.com not found: 5(REFUSED)
Transfer failed.
```

> 列表 218 - 尝试失败

不幸的是，第一个 DNS 服务器 `ns1` 不允许 DNS 区域传输，因此我们的尝试失败了。让我们使用第二个 DNS 服务器 `ns2` 尝试相同的步骤：

```
kali@kali~~$ host -l megacorpome.com ns2.megacorpome.com
Using domain server:
Name: ns2.megacorpome.com
Address: 38.100.193.80#53
Aliases:
megacorpome.com has name server ns1.megacorpome.com,
megacorpome.com has name server ns2.megacorpome.com,
megacorpome.com has name server ns3.megacorpome.com,
admin.megacorpome.com has address 38.100.193.83
beta.megacorpome.com has address 38.100.193.88
fs1.megacorpome.com has address 38.100.193.82
innet.megacorpome.com has address 38.100.193.87
mail.megacorpome.com has address 38.100.193.84
mail2.megacorpome.com has address 38.100.193.73
ns1.megacorpome.com has address 38.100.193.78
```

> 列表 219 - 使用 host 演示 DNS 区域传输

# 使用 Kali Linux 2.0 进行渗透测试

此服务器允许区域传输（zone transfers），并提供了 `megacorp.com` 域名的区域文件完整导出，提供了一份 IP 地址及其对应 DNS 主机名的便捷列表！

`megacorp.com` 域名有少数几个 DNS 服务器需要检查。然而，较大的组织会托管许多 DNS 服务器，或者我们可能想要对给定域名内的所有 DNS 服务器尝试区域传输请求。`Bash` 脚本可以帮助实现此点。

要使用 `host` 命令尝试区域传输，我们需要两个参数：名称服务器地址和域名。我们可以通过以下命令获取特定域名的名称服务器：

```
kali@~$ host - ns megacorp.com | cut -d " " -f 4
ns1.megacorp.com.
ns2.megacorp.com.
ns3.megacorp.com.
```

| 列表 220 - 使用 host 获取特定域名的 DNS 服务器 |

更进一步，我们可以编写一个 `Bash` 脚本来自动化识别相关的名称服务器的过程，并对每个名称服务器尝试区域传输：

```bash
#!/bin/bash

# 简单的区域传输 Bash 脚本
# $1 是在 bash 脚本后的第一个参数
# 检查是否提供了参数，如果没有，则打印用法

if [ -z "$1" ]; then
  echo "[+] 简单的区域传输脚本"
  echo "[+] 用法      : $0 <域名>"
  exit 0
fi

# 如果提供了参数，识别该域名的 DNS 服务器

for server in $(host -t ns megacorp.com | cut -d " " -f4); do
  # 对这些服务器中的每一个尝试区域传输
  host -l $server | grep "has address"
done
```

| 列表 221 - 我们的 Bash DNS 区域传输脚本 |

让我们让脚本变得可执行并针对 `megacorp.com` 运行它。
