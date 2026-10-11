
**答案：** `c) :q!`

## 69: 在 `vi` 中，哪个单个键允许你修改一行文本？

- a) `w`

- b) `i`

- c) `q`

- d) `n`

**答案：** `b) i`

## 70: 哪个命令将更改写入文件，而不退出 `vi`？

- a) `:wq`

- b) `:w!q`

- c) `:w`

- d) `:g`

**答案：** `c) :w`

## 71: 哪个文件包含首选 DNS 服务器列表，用于查找域名的 IP 地址？

- a) `/etc/dns`

- b) `/etc/sysconfig/networking`

- c) `/etc/resolv.conf`

- d) `/etc/sysconfig/dns`

**答案：** `c) /etc/resolv.conf`

## 72: 哪个文件控制显示给每个登录到服务器的用户的文本？

- a) `/etc/message`

- b) `/etc/motd`

- c) `/etc/warning`

- d) `/etc/bash_profile`

**答案：** `b) /etc/motd`

## 73: 哪个文件包含用户的 shell 变量设置以及每次登录时启动的脚本（BASH）？

- a) `/home/username/.bash_script`

- b) `/home/username/.bash`

- c) `/home/username/.bash_profile`

- d) `/home/username/.bash_history`

**答案：** `c) /home/username/.bash_profile`

## 74: 哪个命令会在另一个目录中的文件创建快捷方式？

- a) `ln -s /usr/local/something/something.sh /usr/bin/something.sh`

- b) `ln -h /usr/local/something/something.sh /usr/bin/something.sh`

- c) `ls -s /usr/bin/something.sh`

- d) `chmod a+x /usr/bin/something.sh`

**答案：**

`a) ln -s /usr/local/something/something.sh /usr/bin/something.sh`

## 75: 哪个命令会创建一个目录 `/home` 的 TAR 存档，并将该 TAR 备份存储为 `/backup/backup-home.tar`？

- a) `tar -cvf /home /backup/backup-home.tar`

- b) `tar -xvf /home /backup/backup-home.tar`

- c) `tar -cvf /backup/backup-home.tar /home`

- d) 以上均不是

**答案：**

`c) tar -cvf /backup/backup-home.tar /home`

## 76: 判断对错：'tar' 命令是否保留目录或文件的原始权限？

**答案：**

对

## 77: 你要使用哪个命令来复制整个目录（包括其内容）到另一个位置？

**答案：**

`cp -R directory /path/to/location`

## 78: 哪个命令会使用最大可用压缩率，并以 GZIP 格式压缩文件 'file.tar'？

**答案：**

`gzip -9 file.tar`

## Shell 与 Shell 脚本

## 79: 哪个文件包含用户的 shell 变量设置，并在每次登录时启动脚本（BASH）？

- a) `/home/username/.bash_script`

- b) `/home/username/.bash`

- c) `/home/username/.bash_profile`

- d) `/home/username/.bash_history`

**答案：**

`c) /home/username/.bash_profile`

## 80: 目前最流行的 shell 是什么？

**答案：**

BASH，或 Bourne Again Shell

## 81: 哪个命令可以打印运行脚本的用户可以看到的文本？

**答案：**

`echo`

## 82: 为了确保脚本中的行被正确执行，每个 shell 脚本的开头必须包含哪一行？

**答案：**

`#! /bin/sh`, or `#! /bin/bash`

## 83: 如果脚本给出“权限被拒绝”错误，需要执行哪个命令？

- a) `chmod a+r script.sh`

- b) `chown your_username script.sh`

- c) `chmod a+x script.sh`

- d) `ln -s script.sh script.sh`

**答案：**

`c) chmod a+x script.sh`

## 84: 在基础 shell 脚本中，行 "DAY=$date | cut -b 1-4" 会做什么？

**答案：**

创建一个名为“`DAY`”的变量，并将当前日期赋予它（例如 Mon, Tue, Wed 等）。

## 85: 在基础 shell 脚本中，哪个命令会发送退出状态 0？

**答案：**

`exit 0`

## 86: 如果脚本被设置为以脚本所有者身份运行，并具有脚本所有者的所有权限，那么说该脚本设置了哪个位？

- a) `setuid`

- b) `setroot`

- c) `chown`

- d) `owner`

**答案：**

`a) setuid`

## 87: 哪个命令可以设置脚本以脚本所有者身份运行，并具有该所有者的所有权限？

- a) `chmod 0755 script.sh`

- b) `chmod 2077 script.sh`

- c) `chmod 4755 script.sh`

- d) `chown username script.sh`

**答案：**

`c) chmod 4755 script.sh`

## 88: 哪个命令可以使脚本暂停执行 5 分钟，然后继续执行脚本？

**答案：**

`sleep 5m`

## 89: 哪个特殊设备允许丢弃所有输入？

- a) `/dev/zero`

- b) `/dev/null`

- c) `/dev/discard`

- d) `/dev/trash`

**答案：**

`b) /dev/null`

## 90: 哪个特殊设备包含真正的随机字符，并被许多人视为传统随机设备的替代品？

- a) `/dev/random`

- b) `/dev/dsp`

- c) `/dev/urandom`

- d) `/dev/null`

**答案：**

`c) /dev/urandom`

## 91: 在 shell 脚本中，哪个字符用作注释标识符？

- a) `%`

- b) `//`

- c) `#`

- d) `@`

**答案：**

`c) #`

## 92: 可以使用哪种语法手动执行一个未设置执行位的脚本？

**答案：**

`sh script.sh` OR `bash script.sh`

## 93: 哪个单一字符允许你在同一行放置两个独立的命令？

**答案：**

`;`

## 94: 请写出该行，它创建一个名为 "trees" 的元素，其单独值为 "elm, pine, spruce, fir, dogwood"。该元素的值将用作单独的值，不应设置为单个值。

**答案：**

`For trees in elm pine spruce fir dogwood`

## 95: 给出一个如何逐行打印这些单独元素的示例。

**答案：**

```
do
echo $trees
done
```

## 防火墙/路由

## 96: 哪个设备需要在网络接口之间启用数据包转发时设置为 "1"？

- a) `/proc/sys/net/ip/ip_forward`

- b) `/dev/sys/net/ipv4/ip_forward`

- c) `/proc/sys/net/ipv4/ip_forward`

- d) `/proc/sys/net/ip_forward`

**答案：**

`c) /proc/sys/net/ipv4/ip_forward`

## 97: 给出一个 iptables 命令示例，该命令将阻止所有网络接口上端口 25 的入站 TCP 流量。此规则应该是列表中的最后一条规则，它应该丢弃从外部主机接收到的 SYN 数据包。

**答案：**

```bash
/sbin/iptables -A INPUT -p tcp -dport 25 -j DROP
```

## 98: 给出一个 iptables 命令示例，当源地址为 209.181.6.8 时，阻止端口 25 的入站 TCP 流量。此规则应该是列表中的最后一条规则。

**答案：**

`/sbin/iptables -A INPUT -p tcp --dport 25 -s 209.181.6.8 -j DROP`
