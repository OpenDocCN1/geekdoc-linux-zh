
## 9.1.4. inode 和文件内容

让我们在其中一个文件中放入一些数据。

```
paul@RHELv4u:~/test$ ls -li
total 16
817262 -drwxr-xr-x 1 paul 4096 Feb 15:38 ..
817270 -rw-rw-r-- 1 paul 4096 Feb 15:42 file2
817268 -rw-rw-r-- 1 paul 0 Feb 15:38 file3
paul@RHELv4u:~/test$ cat file2
现在是冬天，天气非常冷。
我们不喜欢冷冷，更喜欢炎热的夏夜晚。
paul@RHELv4u:~/test$
```

`cat` 命令显示的数据不在 `inode` 中，而是在磁盘上的某个地方。`inode` 包含一个指向该数据的指针。

## 9.2. 关于目录

### 9.2.1. 目录是一个表格

目录是一种特殊文件，包含一张将文件名映射到 `inode` 的表格。

使用 `ls -ali` 列出当前目录将显示目录文件的内容。

```
paul@RHELv4u:~/test$ ls -ali
total 32
817262 drwxr-xr-x 2 paul 4096 Feb 15:42 ..
800768 -rw-rw-r-- 1 paul 4096 Feb 15:42 .
817266 -rw-rw-r-- 1 paul 0 Feb 15:38 file1
817270 -rw-rw-r-- 1 paul 92 Feb 15:42 file2
817268 -rw-rw-r-- 1 paul 0 Feb 15:38 file3
paul@RHELv4u:~/test$
```

### 9.2.2. . 和 ..

你可以看到五个名字以及它们到五个 `inode` 的映射。`.` 是映射到自身的映射，而 `..` 是映射到父目录的映射。另外三个名字是映射到不同 `inode` 的映射。

## 9.3. 硬链接

### 9.3.1. 创建硬链接

当我们使用 `ln` 为文件创建硬链接时，目录中会增加额外的条目。新文件被映射到一个已存在的索引。

```
paul@RHELv4:~/test$ ln file2 hardlink_to_file2
paul@RHELv4:~/test$ ln -li
total 24
817266 -rw-r-- 1 paul 0 Feb 5 15:53 file1
817270 -rw-r-- 2 paul 92 Feb 5 15:42 file2
817266 -rw-r-- 1 paul 0 Feb 5 15:38 file3
817270 -rw-r-- 2 paul 92 Feb 5 15:42 hardlink_to_file2
```

两个文件具有相同的 `inode`，因此它们将具有相同的权限和相同的所有者。两个文件将具有相同的内容。实际上，由于两个文件现在是相等的，这意味着你可以安全地删除原始文件，硬链接文件将保留。`inode` 包含一个计数器，用于统计自身的硬链接数量。当计数器降为零时，`inode` 就会清空。

### 9.3.2. 查找硬链接

你可以使用 `find` 命令查找具有特定 `inode` 的文件。下面的截图显示了如何搜索所有指向 `inode` 817270 的文件名。记住，`inode` 号在其分区内是唯一的。

```
paul@RHELv4:~/test$ find -inum 817270 2> /dev/null
/home/paul/test/file2
/home/paul/test/hardlink_to_file2
```

## 9.4. 符号链接

符号链接（有时称为软链接）不链接到 `inode`，而是创建一个名称到名称映射。符号链接通过 `ln -s` 创建。如下所示，符号链接有它自己的 `inode`。

```
paul@RHELv64:~/test$ ln -s file2 symlink_to_file2
paul@RHELv64:~/test$ ls -li
total 32
817273 -rw-r-- 1 paul paul 13 Feb 17:06 file1
817270 -rw-r-- 2 paul paul 106 Feb 5 17:04 file2
817270 -rw-r-- 1 paul paul 0 Feb 15:38 file3
817270 -rw-r-- 2 paul paul 106 Feb 5 17:04 hardlink_to_file2
817267 lrwxrwxrwx 1 paul paul 5 Feb 5 16:55 symlink_to_file2 -> file2
paul@laika:~$
```

符号链接上的权限没有意义，因为应用的是目标的权限。硬链接限制限于其分区（因为它们指向 `inode`），而符号链接可以链接到任何地方（其他文件系统、网络）。

## 9.5. 删除链接

链接可以被删除。

## 10.5. nat (网络地址翻译)

`nat` 设备是一种同时会更改数据包中源地址和/或 IP 地址的路由器。它通常用于将私有地址范围 [rfc 1918] 内的多台计算机与（公网）互联网连接。`nat` 可以从互联网隐藏私有地址。

重要的一点是，人们和供应商在提到某种特定类型的 `nat` 时，并不总是使用正确的术语。请确保你讨论的是同一种东西。我们可以区分几种类型的 `nat`。

## 10.6. pat (端口地址翻译)

`nat` 通常包含 `pat`。`pat` 设备是一种同时会更改数据包中源和/或目标 `tcp/udp` 端口的路由器。`pat` 是 Cisco 的术语，在 Linux 的 `snat`、`nat`、掩装（masquerading）和端口转发（port forwarding）中使用。RFC 3022 其称为 `NAPT`，并将 `nat/pat` 组合定义为“传统 nat”。卖给你的 nat 设备可能同时执行 `nat` 和 `pat`。

## 10.7. snat (源地址翻译)

`snat` 设备在数据包通过我们的 `nat` 配置时更改源 IP 地址。使用 `iptables` 的 `snat` 配置包含固定的目标源地址。

## 10.8. masquerading (掩装)

`Masquerading`（掩装）是 `snat` 的一种形式，它使用公网 IP 地址隐藏私有网络的源 IP 地址。在动态互联网接口（宽带调制解调器/路由器）上常见。`iptables` 的掩装配置使用动态目标源地址。

## 10.9. dnat (目的地址翻译)

`dnat` 设备在数据包通过我们的 `nat` 时更改目的 IP 地址。

## 10.10. port forwarding (端口转发)

当设置静态 `dnat` 以允许外部连接进入我们的私有网络时，我们将其称为端口转发。

## 10.11. /proc/sys/net/ipv4/ip_forward

主机是否转发数据包在 `/proc/sys/net/ipv4/ip_forward` 中定义。以下截图显示了如何在 Linux 上启用数据包转发。

```
root@router-# echo 1 > /proc/sys/net/ipv4/ip_forward
```

下一个命令显示了如何禁用数据包转发。

```
root@router-# echo 0 > /proc/sys/net/ipv4/ip_forward
```

使用 `cat` 检查是否启用了数据包转发。

```
root@router-# cat /proc/sys/net/ipv4/ip_forward
```

## 10.12. /etc/sysctl.conf

默认情况下，大多数 Linux 计算机未配置自动数据包转发。要在系统启动时始终启用数据包转发，请将 `/etc/sysctl.conf` 中的 `net.ipv4.ip_forward` 变量更改为 1。

```
root@router-# grep ip_forward /etc/sysctl.conf
net.ipv4.ip_forward = 0
```
