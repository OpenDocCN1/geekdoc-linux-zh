
指定目标端口（例如，HTTP 的 80 端口）。

- **IPv6 Traceroute：**

```
traceroute -p 80 example.com
```

使用 IPv6 地址执行 traceroute。

- **将输出保存到文件：**

```
traceroute -6 ipv6.example.com
```

将输出重定向到文件以便后续分析。

- **连续追踪：**

```
traceroute example.com > trace_output.txt
```

连续追踪路由，每个跃点发送单个数据包，等待时间最短。

## 32. ifconfig 或 ip：配置网络接口。

### `ifconfig` 命令：

`ifconfig` 命令用于配置 Linux 系统上的网络接口。它允许您查看和配置网络接口的 IP 地址、子网掩码、广播地址和其他参数。然而，在许多现代 Linux 发行版中，`ifconfig` 已被弃用，转而使用更强大的 `ip` 命令。

#### 示例：

1. **查看网络接口：**

```
ifconfig
```

此命令显示系统中所有网络接口的信息。

2. **查看特定接口的信息：**

```
ifconfig eth0
```

将 `eth0` 替换为您的网络接口名称。此命令显示指定接口的详细信息。

3. **分配 IP 地址：**

```
sudo ifconfig eth0 192.168.1.2
```

此命令将 IP 地址 192.168.1.2 分配给 `eth0` 接口。

4. **设置子网掩码：**

```
sudo ifconfig eth0 netmask 255.255.255.0
```

为 `eth0` 接口设置子网掩码。

5. **启用或禁用接口：**

```
sudo ifconfig eth0 up
sudo ifconfig eth0 down
```

这些命令分别启用或禁用 `eth0` 接口。

### `ip` 命令：

`ip` 命令是一个更强大、更灵活的网络接口配置和管理工具。它提供了 `ifconfig` 之外的广泛功能。

#### 示例：

1. **查看网络接口：**

```
ip link show
```

此命令显示系统中所有网络接口的信息。

2. **查看 IP 地址：**

```
ip address show
```

显示分配给所有接口的 IP 地址的详细信息。

3. **分配 IP 地址：**

```
sudo ip address add 192.168.1.2/24 dev eth0
```

将 IP 地址 192.168.1.2 和子网掩码 255.255.255.0 分配给 `eth0` 接口。

4. **设置子网掩码：**

```
sudo ip address add 192.168.1.2/24 dev eth0
```

这也为 `eth0` 接口设置了子网掩码。

5. **启用或禁用接口：**

```
sudo ip link set eth0 up
sudo ip link set eth0 down
```

这些命令分别启用或禁用 `eth0` 接口。

6. **显示路由表：**

```
ip route show
```

显示内核路由表。

## 33. netstat：显示网络连接、路由表、接口统计、伪装连接和多播成员关系。

Linux 中的 `netstat` 命令是一个强大的网络实用工具，用于显示有关网络连接、路由表、接口统计、伪装连接等的信息。它提供了多种选项，帮助您分析和排除网络相关问题。

### 示例：

- **使用数字地址显示所有监听和非监听套接字：**

```
netstat -an
```

- **显示所有协议的统计信息：**

```
netstat -s
```

- **显示所有 TCP 连接及使用它们的过程：**

```
netstat -atp
```

- **显示路由表：**

```
netstat -r
```

- **仅显示监听中的 TCP 套接字：**

```
netstat -tl
```

- **显示所有接口的信息：**

```
netstat -ie
```

- **显示内核接口表：**

```
netstat -i
```

## 34. ncdu：NCurses 磁盘使用情况 - 一个磁盘使用分析器。

`ncdu` (NCurses Disk Usage) 是 Linux 中用于分析和磁盘空间使用情况的命令行实用程序。它以简单、交互的方式查看和浏览文件系统，并以层级格式显示目录和子目录的大小。

### 示例：

1. **分析当前目录的磁盘使用情况：**

```
ncdu
```

2. **分析特定目录的磁盘使用情况：**

```
ncdu /path/to/directory
```

3. **从分析中排除某些文件或目录：**

```
ncdu -x "*.log" /path/to/directory
```

4. **以只读模式运行以防止意外删除：**

```
ncdu -r /path/to/directory
```

5. **指定包含要分析的目录列表的文件：**

## 35. ltrace：库调用跟踪器。

`ltrace` 是 Linux 中的一个命令行实用工具，用于拦截并显示程序所执行的动态库调用。它可以让你查看进程调用的库函数和系统调用，从而提供程序运行期间行为的重要见解。

**示例：**

- 1. 基本用法：

```bash
ltrace ls
```

此命令跟踪由 `ls` 命令执行的动态库调用。

- 2. 过滤输出：

```bash
ltrace -e fopen ls
```

`-e` 选项允许你过滤输出，仅显示你感兴趣的函数。在此示例中，它仅跟踪由 `ls` 命令对 `fopen` 函数的调用。

- 3. 将输出重定向到文件：

```bash
ltrace -o output.txt ls
```

此命令将 `ltrace` 的输出重定向到名为 `output.txt` 的文件，而不是打印到终端。

- 4. 通过 PID 跟踪特定进程：

```bash
ltrace -p <pid>
```

用你想跟踪的正在运行的进程 ID 替换 `<pid>`。这对于将 `ltrace` 附加到已运行的进程非常有用。

- 5. 显示系统调用：

```bash
ltrace -S ls
```

`-S` 选项除了库调用外，还包含系统调用的显示。

- 6. 在 64 位系统上跟踪 32 位进程：

```bash
ltrace -a 32 -c ls
```

使用 `-a` 选项在 64 位系统上跟踪进程时指定架构（在此情况下为 32 位）。

- 7. 按库过滤：

```bash
ltrace -l libm.so ls
```

此命令仅跟踪由 `ls` 命令对 `libm` 库中函数的调用。

- 8. 显示时间和计数：

```bash
ltrace -c ls
```

`-c` 选项显示每个函数的调用次数和所花时间摘要。

- 9. 跟踪带有命令行参数的程序：

```bash
ltrace gzip file.txt
```

你可以连同其命令行参数一起跟踪程序。

- 10. 跟踪多个命令：

```bash
ltrace -o output.txt sh -c "ls; echo Hello"
```

通过使用 `c` 选项并将它们括在引号中，在 shell 中跟踪多个命令。

- 11. 显示函数参数：

```bash
ltrace -f -F ls
```

`f` 选项跟踪 fork（分叉），而 `F` 选项显示函数参数。

## 36. useradd：创建新的用户账户。

Linux 中的 `useradd` 命令用于在系统上创建新的用户账户。它是一个基本命令，允许你在创建新用户时指定各种参数。

**示例：**

- 1. 创建新用户：

```bash
sudo useradd mohan
```

此命令使用默认设置创建名为 "mohan" 的新用户账户。用户的家目录将是 `/home/mohan`。

- 2. 创建具有特定家目录的用户：
