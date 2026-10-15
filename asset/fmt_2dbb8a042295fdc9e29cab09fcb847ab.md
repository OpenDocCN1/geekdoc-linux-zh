
```
ipchains -A output -src 192.168.1.0/24 -dst 192.168.1.0/24 -j MASQ
ipchains -A input -dst 192.168.1.12 -j ACCEPT
```

- A. `192.168.1.0/24` 网络正在被伪装 (`masq`)。
- B. `IP` 转发被禁用。
- C. `IP` 转发已启用。
- D. 访问 `192.168.1.12`

## 题目编号：76

使用哪个命令显示安装了哪些包？

- A. `rpm -l`
- B. `rpm -qa`
- C. `dpkg -l`
- D. `dpkg -l`

*(注：由于原文中存在大量重复，已按要求翻译了所有出现的行)*

**纠正：** 重新审视原文，发现其中确实存在大量完全相同的重复块（例如题目28-45重复出现了多次）。为了遵循“不要漏掉任何行”的指令，我将按照原文出现的顺序对每一行进行翻译：

### 题目编号：28

数据包过滤防火墙在哪个层级进行过滤？

- A. 物理层
- B. 数据链路层
- C. 网络层或传输层
- D. 应用层

### 题目编号：29

是什么告诉防火墙如何重组被拆分成数据包的数据流的？

- A. 源路由功能
- B. 头部中标识字段的数字
- C. 目的 `IP` 地址
- D. 数据包头部中的报部校验和字段

### 题目编号：30

防火墙需要是 `________`，以便它能够随着其保护的网络同步增长

- A. 健壮的 (`Robust`)
- B. 扩张的 (`Expansive`)
- C. 快速的 (`Fast`)
- D. 可扩展的 (`Scalable`)

# `Secbay Press`

### 题目编号：31

你想通过 `NFS` 提供目录 `/share`。本地网络上的所有用户都应该被允许读写文件。假设你的本地网络是 `192.168.1.0`，且你的机器属于 `DNS` 域 `mydomain.org`，以下哪项是正确的？

- A. `/local 192.168.1.0/255.255.255.0(rw)`
- B. `/local 192.168.1.0/*(rw)`
- C. `/local *.org(rw)`
- D. `/local ALL.mydomain.org(rw)`

### 题目编号：32

双层二进制包束包含可以直接用于文件的记录

- A. `.deb` 文件
- B. `.exe` 文件
- C. `.apt` 文件
- D. `.mp4` 文件

### 题目编号：33

这些是 `kali` 仓库的 3 种类

- A. `main`, `security`, `update`
- B. `main`, `contrib`, and `non-free`
- C. `contrib`, `security`, `free`
- D. `update`, `security`, `non-free`

### 题目编号：34

哪个 `kali` 仓库仅包含可安装的较新的包？

- A. `kali main`
- B. `kali rolling`
- C. `kali dev`
- D. `kali bleeding edge`

### 题目编号：35

哪个 `kali` 仓库包含未经过测试或审查的包？

- A. `kali rolling`
- B. `kali main`
- C. `kali bleeding edge`
- D. `kali dev`

### 题目编号：36

使用 `dpkg` 安装包的命令是什么？

- A. `dpkg –i`
- B. `dpkg –i`
- C. `dpkg –o`
- D. `dpkg –install`

### 题目编号：37

使用 `dpkg` 卸载包的命令是什么？

- A. `dpkg -l`
- B. `dpkg -r`
- C. `dpkg --remove`
- D. `dpkg --r`

### 题目编号：38

`apt-get` 的替代命令是什么？

- A. `Debian -r`
- B. `dpkg`
- C. `aptitude`
- D. `uname`

### 题目编号：39

`kali linux` 操作系统中存储列表存储在哪里？

- A. `/etc/apt/source.list`
- B. `/etc/source/source.list`
- C. `/var/www/html`
- D. `/etc/passwd`

### 题目编号：40

`RBAC` 的缩写是 `_________`

- A. `Rule-Based Accessing Control`
- B. `Role-Based Access Control`
- C. `Rule-Based Access Control`
- D. `Role-Based Accessing Control`

### 题目编号：41

哪个命令向系统添加了新的默认路由？

- A. `ifconfig add default gw 1.2.3.4`
- B. `route add gw 1.2.3.4`
- C. `route add default gw 1.2.3.4`
- D. `ifconfig add 0.0.0.0 mask 255.255.255.0 gw 1.2.3.4`

### 题目编号：42

哪个 `kali` 仓库不是供公开使用的？

- A. `kali rolling`
- B. `kali main`
- C. `kali dev`
- D. `kali bleeding edge`

### 题目编号：43

哪个工具是为了克服 `apt-get` 的设计缺陷而开发的？

- A. `apt-remove`
- B. `apt-get-install`
- C. `apt`
- D. `sudo`

### 题目编号：44

应该使用哪个命令允许主机 `norbert` 连接到本地 `X` 服务器？

- A. `xhost +`
- B. `cat norbert > .hosts`
- C. `xhost +norbert`
- D. `rhosts +norbert`

### 题目编号：45

以下 `ipchains` 链实现了什么？（选择所有适用项）

```
-F ipchains

echo 1 > /proc/sys/net/ipv4/ip_forward

ipchains -A output -src 192.168.1.0/24 -dst 192.168.1.0/24 -j MASQ

ipchains -A input -dst 192.168.1.12 -j ACCEPT
```
