
在`Leafpad`中保存更改后，现在在`Kali Linux`中点击`Applications`（应用程序）。

- `Applications`（应用程序） -> `sniffing and spoofing`（嗅探与欺骗） -> `network sniffing`（网络嗅探） -> `Ettercap graphical`（`Ettercap`图形界面）。

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_234_1.png)

- 选择`ts`列表（目标列表）。

- 现在选择网络接口。如果使用局域网（`LAN`），选择`eth0`。

# `Secbay` Press

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_235_0.png)

- 开启目标机器并在虚拟机上的`IP`。
- 然后在`Ettercap`上开始扫描主机（`scan hosts`）。
- 并找到主机列表。

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_235_1.png)

- 现在选择目标`IP`并将其添加目标 1（`target 1`）。
- 找到默认网关并将其作为目标 2（`target 2`）。

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_235_2.png)

# `Secbay` Press

- 点击`MITM`（中间人攻击）并选择`ARP poisoning`（`ARP`毒化）。

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_236_0.png)

选择`ARP poisoning`下的两个选项：

- `Sniff remote connections`（嗅探远程连接）
- `Only one way poisoning`（仅单向毒化）

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_236_1.png)

- 点击`plugins`（插件），选择`manage plugins`（管理插件）并双击`'dns_spoof'`。

- 现在转到`start`（开始），点击`start sniffing`（开始嗅探）。

# `Secbay` Press

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_237_0.png)

嗅探完成后，在受害者机器上启动浏览器并输入`google.co.in`，页面将重定向到`hackthissite.org`网站。

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_237_1.png)

## `10.4` `XArp`

`XArp`是一种网络安全技术。它能识别防火墙无法检测的主要网络威胁。

真正的解释是`XArp`采用了复杂的方法来识别`ARP`攻击，例如`ARP`欺骗。这些攻击发起简单但效果显著，且能规避防火墙。

### `10.4.1` 为什么我需要`XArp`？

因为基于`ARP`的攻击被严重低估了。攻击者可以通过`ARP`欺骗窃听你所有的网络流量，包括电子邮件和密码。这一切都在完全不被察觉的情况下。为了识别此类攻击，`XArp`同时采用了主动和被动两种方法方法。

### `10.4.2` 我在什么种网络环境下需要`XArp`？

因为基于`ARP`的攻击被严重低估了。攻击者可以通过`ARP`欺骗窃听你所有的网络流量，包括电子邮件和密码。这一切都在完全不被察觉的情况下。为了识别此类攻击，`XArp`同时采用了主动和被动两种方法方法。

### `10.4.3` 当`XArp`检测到攻击时该怎么办？

最好的建议是立即关闭所有互联网和网络连接。关闭所有浏览器、电子邮件客户端和网络客户端。联系你的网络管理员。他可以评估`Xarp`日志以确定需要哪些操作。

### `10.4.4` 安装`XArp`？

1. 在安装`XArp`之前，你需要安装依赖项`xarp as libxces-c3.1`和`artables`。
2. 然后在编辑器的网站`http://www.xarp.net/`下载包。
   ```
   wget -O xarp-2.2.2-i68.deb www.xarp.net/?download=10343
   ```
3. 然后安装包。
4. 如果出错，执行以下命令：
   ```
   #apt-get install libxces-c3.1 artables
   ```
   ```
   #dpkg -i xarp-2.2.2-i68.deb
   ```
   ```
   #apt-get install -f
   ```

## `10.5` 网络钓鱼 (`Phishing`)

网络钓鱼是一种欺诈行为，旨在通过将电子通信伪装成受信实体，来获取敏感信息（包括用户名、密码和信用卡详情），通常出于恶意目的。

网络钓鱼通常通过伪造电子邮件或即时消息完成，并经常引导用户在虚假网站上输入个人信息（凭据），该网站的外观和感受非常真实。

网络钓鱼通常通过伪造电子邮件或即时消息完成，并经常引导用户在虚假网站上输入个人信息（凭据），该网站的外观和感受非常真实。

网络钓鱼通常通过伪造电子邮件或即时消息完成，并经常引导用户在虚假网站上输入个人信息（凭据），该网站的外观和感受非常真实。

网络钓鱼攻击者可以通过伪造邮件发送恶意信息，引导用户在虚假网站上输入凭据。

网络钓鱼的几种方法包括：
- 局域网：攻击者通过伪造邮件引导用户在虚假网站上输入凭据。
- 远程：攻击者通过伪造邮件发送一个看起来像真实网站的链接，引导用户在虚假网站上输入凭据。
- 攻击者通过伪造邮件发送恶意网站的链接，引导用户在伪造网站上输入凭据。

网络钓鱼的类型包括：
- 鱼叉式钓鱼 (`Spear Phishing`)
- 克隆式钓鱼 (`Clone Phishing`)
- 针对高管的钓鱼 (`Whaling`)

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_239_0.png)

第 2 步：选择负载（`PAYLOAD`）类型（可以定义为安装在受害者或用户上的恶意文件）。

| 名称 | 描述 |
| :--- | :--- |
| 1) `Windows Reverse TCP Shell` attacker | 在受害者上启动命令 shell 并将其发送回给攻击者 |
| 2) `Windows Meterpreter Reverse TCP` attacker | 在受害者上启动`meterpreter`并将其发送回给攻击者 |
| 3) `Windows Reverse VNC DLL` | 在受害者上启动`VNC`服务器并发送回给攻击者 |
| 4) `Windows Reverse TCP Shell` (`x64`) | `Windows X64`命令壳，反向`TCP`内联 |
| 5) `Windows Meterpreter Reverse TCP` (`X64`) | 连接回攻击者（`Windows x64`），`Meterpreter` |
| 6) `Windows Shell Bind TCP` (`X64`) | 执行负载并在远程上创建一个接受连接的端口 |
| 7) `Windows Meterpreter Reverse HTTPS` | 通过`HTTP SSL`隧道进行通信并使用`Metploit` |

> 注意：这将创建一个`Word`文档，该文档将导致缓冲区溢出并使我们能够在受害者机器上放置监听器或`rootkit`。

第 3 步：攻击者将获取生成的负载以部署在受害者的机器上，并可以选择将其发送给多个接收者进行群发邮件攻击，或发送给单个接收者。

> 注意：文件已重命名为“`Report`”的`payload`。

```
phishing> New filename:Report

Filename changed, moving on...

Social Engineering Toolkit Mass E-Mailer

这里群发邮件发送器上有两个选项，第一个是

向单个个人发送电子邮件。第二个选项

将允许你导入列表，并向列表中的你想发送的任何人数发送邮件。

你想做什么：

- 邮件攻击 单个邮件地址

- 邮件攻击 群发邮件器

- 返回主菜单。

phishing>
```

第 4 步：攻击者可以使用一次性使用或预定义的负载。在这里，我将使用单次使用邮件发送器。

# `Secbay` Press

```
will allow you to import a list and send it to as many people as

you want within that List.

What do you want to do:

1. 邮件攻击 单个邮件地址

2. 邮件攻击 群发邮件器

99. 返回主菜单。

set:phishing=2

你是否想使用预定义模板或制作一个

一次性邮件模板。

1. 预定义模板

2. 一次性邮件模板

set:phishing=2

set:phishing:Subject of the email: We are here to say that the organization has

to send you the report of sales of last month. Thank you.
```
