
```
;; mailhost.syngress.com. IN A 155.212.56.77

;; spool.convert.net. 576 IN A 155.212.2.61

ns1.convert.net. 3600 IN A 216.41.101.15

ns2.convert.net. 3600 IN A 216.41.101.17

;; Total query time: 102 msec

;; FROM:

;; WHEN: Nov 17 17:37:41 2005

;; MSG SIZE sent: 30 rcvd: 203

prox#$
```

## 开源工具

尽管看起来可能有些矛盾，但 Windows 操作系统也有一些非常优秀的开源工具可用。我们在侦察阶段使用的某些开源工具将在接下来的节中进行讨论。

> 地下室笔记：Windows 开源工具的兴起

多年来，用于渗透测试的 PERL 和 Java 工具已适用于 Windows 和 Unix 环境。遗憾的是，脚本编写者倾向于使用 shell 转义来执行复杂任务，这往往将我们用于侦察的工具限制在 Unix 环境。相反的是，随着 C 语言和 .NET 环境的出现，工具的流行似乎再次增长。这可能归于编码人员追求易用性和灵活性（例如易于图形化界面），但也仅仅是工具之间“共鸣”的一个简单案例。

### 第1章 • 侦察

#### 使用方法：
```
perl qtrace.pl [ip_address_file] [output_file]
```

#### 输入字段：
- 每行一个完整的 IP 地址
- 将结果输出到文件

典型用法：
```
perl qtrace.pl ip_list.txt outputfile.txt
```

输出格式：
网络范围 `10.10.1.1-10.10.28`

# 图 1.42 qtrace 输出示例

![](img/2714962ecb7769011405633c8d4d1fc9_108_0.png)

## BiLE Suite 套件 jarf-rev

`jarf-rev` 用于对 IP 范围执行反向 DNS 查询。所有匹配过滤文件的反向条目都会显示在屏幕上。输出显示为 DNS 名称，后紧跟 IP 地址。

#### 使用方法：
```
perl jarf-rev [subnetblock] [nameserver]
```

#### 输入字段：
- 指定的子块（Subblock）是网络地址的前三个字节
- 名称服务器（Nameserver）是要使用的名称服务器

#### 典型用法：
```
perl jarf-rev 192.168.37.1-192.168.37.118 10.10.15.60
```

#### 输出格式：
DNS 名称 : IP 数字

如果无法发现反向条目，则 DNS 名称为空。

# 图 1.43 jarf-rev 输出示例

![](img/2714962ecb7769011405633c8d4d1fc9_109_0.png)

```
prox$#1 jarf-rev 168.210.134.0-168.210.134.100 168.210.2.2 1

siteadmin.sennespost.com:168.210.134.4

168.210.134.0

pokied.sennespost.com:168.210.134.1

168.210.134.0

solfool.sennespost.com:168.210.134.3

snterly.sennespost.com:168.210.134.5

blowifh.sennespost.com:168.210.134.6

knoofmul.sennespost.com:168.210.134.2

dorjer.sennespost.com:168.210.134.7

merino.sennespost.com:168.210.134.8

retroner.sennespost.com:168.210.134.9

recazy.sennespost.com:168.210.134.10

techano.sennespost.com:168.210.134.11

kragamami.sennespost.com:168.210.134.12

apprishan1.sennespost.com:168.210.134.13

strongringe.sennespost.com:168.210.134.14

brodecore.sennespost.com:168.210.134.15

168.210.134.16

168.210.134.17

168.210.134.18

168.210.134.19

168.210.134.20

168.210.134.21

168.210.134.22
```

## `ipcalc`

`ipcalc.pl` 是一个简单的 Perl 脚本，我们用它来分析 IP 块的结构。工具所有者：“`ipcalc` 接收 IP 地址和子网掩码，并计算出相应的广播地址、网络地址、Cisco 通配掩码和主机范围。通过提供第二个网络，你可以设计子网络和超网络。它还被设计为一种教学工具，以易于理解的二进制值呈现结果。”

示例：
```
perl ipcalc.pl 192.168.1.0/28
```
