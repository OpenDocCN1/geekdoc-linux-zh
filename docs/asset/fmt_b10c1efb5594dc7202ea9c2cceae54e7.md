
![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_150_0.png)

## 7.3 DirBuster

`DirBuster`是一个多线程 Java 应用，旨在爆破 Web/应用程序服务器上的索引和名称。通常情况下，看起来处于默认设置的 Web 服务器并非如此，而是隐藏了页面和应用程序。`DirBuster`试图发现这些内容。然而，这类工具的效果通常取决于它们随附的索引和记录列表。制作该工具采用了不同的方法：该列表是在没有任何外部帮助的情况下，通过爬取互联网并收集设计师实际使用的注册和记录创建的！`DirBuster`总共包含 9 条独特的记录，这使得`DirBuster`在寻找那些隐藏的文档和索引方面非常成功。此外，

### Secbay 出版

如果这还不够，`Distuster`同样可以选择进行完全不加饰的野兽级强制，这使得隐藏的注册表和文档无处遁形。

## 7.3.1 安装 durbuster

```
# sudo apt-get install durbuster
[sudo] password for user:
Reading package lists...Done
Building dependency tree...Done
Reading state information...Done
0 to upgrade, 1 new to be installed, 0 not to remove
durbuster-1.0-rc1.1~ubuntu20.04.1:amd64 libarchive-dev:0.9.27-13ubuntu20.04.1:amd64 libarchive5:0.9.27-13ubuntu20.04.1:amd64 libicu-dev:6.61.1-2ubuntu20.04.1:amd64 libicu66:6.61.1-2ubuntu20.04.1:amd64 libbz2-dev:1.53.9-2ubuntu20.04.1:amd64 libbz2-1:1.53.9-2ubuntu20.04.1:amd64 libcurl4-dev:7.68.0-1ubuntu20.04.1:amd64 libcurl4-openssl-dev:7.68.0-1ubuntu20.04.1:amd64 libcurl4-openssl:7.68.0-1ubuntu20.04.1:amd64 libcap2-dev:2.28-4ubuntu2.2.22.1:amd64 libcap2:2.28-4ubuntu2.2.22.11:amd64 libffi-dev:3.3.1-8ubuntu2.2.22.1:amd64 libffi7:3.3.1-8ubuntu2.2.22.1:amd64 libz1g-dev:1.8.6-2ubuntu20.04.1:amd64 libz1g1:1.8.6-2ubuntu20.04.1:amd64 libreadline-dev:8.2-3ubuntu20.04.1:amd64 libreadline8:8.2-3ubuntu20.04.1:amd64 libsqlite3-dev:3.31.1-0ubuntu0.20.0:amd64 libsqlite3:3.31.1-0ubuntu0.20.0:amd64 libncurses5-dev:6.2-20ubuntu2.2.22.1:amd64 libncurses5:6.2-20ubuntu2.2.22.1:amd64 libncursesw5-dev:6.2-20ubuntu2.2.22.1:amd64 libncursesw5:6.2-20ubuntu2.2.22.1:amd64nSetting autoremove... done
Cleaning previously unneeded packages... done
0 upgraded, 1 installed, 0 to remove and 0 not upgraded.
```

## 7.3.1 durbuster 的用法

```
durbuster-cli $ durbuster -h
durbuster -j Durbuster-1.0-RC1 -u URL http://example.com/ [Options]

Options:
-h 显示此帮助信息
-H 以无头模式启动 Durbuster（无界面），报告将在退出时保存
-l 指定基于驱动扫描的列表文件路径。默认值：/home/klpt/directory-list-2.3.5-small.txt
-c 指定报告的文件名。默认值：/home/klpt/duster-report.html
-t 连接到线程的数量。默认值：10
-s 指定扫描范围。默认值：/
-v 详细输出，默认值：未设置
-p 不提示 html，默认值：未设置
-F 不覆盖文件，默认值：未设置
-r (locations) : 保存报告的文件。默认值：/home/klpt/Durbuster-Report-[hostname].[port].txt
```

示例：

```
在无头模式下运行 Distuster
java -jar Durbuster-1.0-RC1.jar -u https://www.target.com/
```

```
使用提议目标启动 GET
java -jar Durbuster-1.0-RC1.jar -u https://www.target.com/
```

在实时目标上运行 `durbuster`

```
$ kali@kali:~$ http://certifiedhacker.com
$ diruster -u http://certifiedhacker.com -options -D swing.aatext=true
正在以无头模式启动 Diruster 1.0-RC1
at java.io.FileNotFoundException: /home/kali/Diruster/list-2-small.txt (No such file or directory)
at java.base/java.io.FileInputStream.open(FileInputStream.java:216)
at java.base/java.io.FileInputStream.init(FileInputStream.java:153)
at java.base/java.io.FileInputStream.openInput((FileInputStream.java:191)
at java.base/java.io.FileChannel.open(FileChannel.java:291)
at com.diruster.Utils.getNumberOfLineInFile(Utils.java:44)
at com.diruster.Start.main(Start.java:111)
at com.diruster.Utils.getNumberOfLineInFile(Utils.java:67)
at com.diruster.Start.main(Start.java:344)

来自来自 Diruster 的错误
报告已保存至 /home/kali/Diruster-Report-certifiedhacker.com.txt
享受剩下的 Diruster 通知，它会在扫描并生成报告的同时通知你。以下是报告的片段：
```

```
$ kali@kali:~
$ cat /home/kali/Diruster-Report-scanme.nmap.org-80.txt
Diruster 1.0-RC1 - 报告
报告生成于 2023年4月7日 10:16
```

![](8ce6ad08bbaee4f550e48ea7a3d6ee_152_0)

## diruster 的用法

## Nmap

`Nmap`（"网络映射器"）是一项用于系统揭示和安全审查的免费开源实用工具。许多框架和系统管理员认为它非常有价值。

### 7.4.1 Nmap 的功能

`Nmap`的功能包括：

- 1. 识别网络上的所有设备，如服务器、路由器。
- 2. 帮助识别运行在系统上的服务。
- 3. `Nmap`可以发现操作系统。
- 4. `Nmap`可以使用`Nmap`脚本引擎进行安全渗透测试。
- 5. `Zenmap`是`Nmap`的图形界面，它可以让你创建可视化映射。

### 7.4.2 安装 nmap

```
$ sudo apt-get install nmap
Reading package lists...Done
Building dependency tree...Done
Reading state information...Done
以下软件包将被自动移除且不再需要
map 7.80.1
以下将安装新软件包
nmap 7.80.1
0 个升级，1 个安装，0 个移除，0 个未升级。
运行'apt autoremove' 删除需要的软件包。
```
