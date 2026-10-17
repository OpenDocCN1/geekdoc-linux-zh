
## useradd：创建用户账户

```bash
sudo useradd -m -d /home/customuser customuser
```

`-m`选项确保创建用户家目录，而`-d`指定家目录路径。

### 3. 指定用户的登录 shell：

```bash
sudo useradd -s /bin/bash bashuser
```

此命令创建名为"bashuser"的用户，并将登录 shell 设置为`/bin/bash`。

### 4. 设置用户密码：

```bash
sudo useradd -m -p $(openssl passwd -1 mypassword) secureuser
```

`-p`选项允许你设置用户的加密密码。在此示例中，`openssl passwd -1`生成字符串"mypassword"的加密密码。

### 5. 创建具有特定用户 ID (UID) 和组 ID (GID) 的用户：

```bash
sudo useradd -u 1001 -g 1001 customuser
```

`-u`选项设置用户 ID，而`-g`选项设置用户的主组 ID。

### 6. 创建系统用户：

```bash
sudo useradd -r sysuser
```

`-r`选项用于创建系统用户，通常用于运行系统服务。

### 7. 设置用户账户的过期日期：

```bash
sudo useradd -e 2023-12-31 tempuser
```

`-e`选项设置用户账户的过期日期。在此示例中，"tempuser"的账户将在2023年12月31日过期。

### 8. 显示 useradd 命令帮助：

```bash
useradd --help
```

此命令提供`useradd`命令选项和用法的摘要。

## 37. userdel：删除用户账户。

Linux 中的`userdel`命令用于从系统中删除用户账户及相关文件。它是一个强大的命令，需要管理权限才能执行。当用户账户被删除时，通常相关的家目录和邮件池会被移除，但其他位置的文件不会被触及。

**示例：**

### 1. 基本用法：

```bash
sudo userdel mohan
```

这将删除名为"mohan"的用户账户。

### 2. 删除用户及家目录：

```bash
sudo userdel -r jane
```

这将删除用户账户"jane"及其家目录和内容。

### 3. 强制删除且无需提示：

```bash
sudo userdel -f alice
```

### 4. 指定不同的家目录：

```bash
sudo userdel -m -r bob
```

这将删除用户账户"bob"并将家目录移动到备份位置。

### 5. 将用户从组中移除：

```bash
sudo userdel -G developers,sudo charlie
```

此命令将删除用户账户"charlie"并使其从"developers"和"sudo"组中移除。

### 6. 显示帮助信息：

```bash
userdel --help
```

这将显示选项列表及其解释。

## 38. passwd：更改用户密码。

Linux 中的`passwd`命令用于更改用户密码。它允许用户更新自己的密码，或者如果由超级用户执行，则更改系统中任何用户的密码。

**示例：**

### 1. 更改你自己的密码：

```bash
passwd
```

系统会提示你输入当前密码，然后输入新密码。

### 2. 更改其他用户的密码（作为 root）：

```bash
sudo passwd username
```

用实际的用户名替换"username"。此命令会提示你为指定用户输入新密码。

### 3. 锁定用户账户：

```bash
sudo passwd -l username
```

这将锁定指定用户账户的密码，阻止其登录。

### 4. 解锁用户账户：

```bash
sudo passwd -u username
```

这将解锁指定用户账户的密码，允许其再次登录。

### 5. 删除用户密码：

```bash
sudo passwd -d username
```

这将删除指定用户账户的密码，实际上使通过密码登录变得不可能。

### 6. 使用户密码过期：

```bash
sudo passwd -e username
```

这将强制用户在下次登录时更改密码。

## 39. mpstat：报告处理器相关统计信息。

Linux 中的`mpstat`命令用于显示多处理器系统中每个处理器利用率的详细信息。它提供单个处理器以及所有处理器平均值的统计信息。

**示例：**

### 1. 每 2 秒显示所有处理器的 CPU 利用率统计信息，共 3 次报告：

```bash
mpstat -u 2 3
```

### 2. 显示单个处理器的统计信息：

```bash
mpstat -P ALL
```

### 3. 显示中断统计信息：

```bash
mpstat -I SUM
```

### 4. 显示所有可用信息：

```bash
mpstat -A
```

## 40. sar：收集、报告或保存系统活动信息。

Linux 中的`sar`命令用于收集、报告和保存系统活动信息。它提供有关系统性能的广泛统计信息，包括 CPU 利用率、内存使用、磁盘活动、网络活动等。`sar`收集的数据对性能分析和故障排除非常有用。

**示例：**

### 1. 以 5 秒间隔显示 CPU 利用率统计信息，共 3 次：

```bash
sar -u 5 3
```

### 2. 以 10 秒间隔显示内存利用率统计信息，共 5 次：

```bash
sar -r 10 5
```

### 3. 以 1 分钟间隔无限期显示 I/O 和传输速率统计信息：

### 4. 以 2 秒为间隔显示网络统计信息，共 4 次：

```bash
sar -n DEV 2 4
```

### 5. 以 30 秒为间隔显示所有可用的统计信息，共 10 次：

```bash
sar -A 30 10
```

## 41. echo：显示一条消息或向文件写入消息。

Linux 中的`echo`命令用于在标准输出（通常是终端）上显示一行文本或一串字符。它是一个简单且常用的命令，用于向屏幕打印信息、变量或消息。

**示例：**

### 1. 基本用法：

```bash
echo "Hello, World!"
```

### 2. 使用变量：

```bash
name="mohan"
echo "My name is $name"
```

### 3. 不换行：

```bash
echo -n "This is on the same line"
echo " but this is on the next line."
```

### 4. 转义字符：

```bash
echo -e "This is a line with a\tab."
```

## 42. history：显示命令历史记录。

Linux 命令历史是一个功能，允许用户查看和调取之前在终端中执行过的命令。它通过避免用户重新输入常用命令来帮助用户节省时间。命令历史存储在一个文件中，通常位于用户的家庭目录中，并由 Shell 管理。

**示例：**

### 1. 查看命令历史：

```bash
history
```

这将显示一个编号列表，最近执行的命令位于列表底部。

### 2. 执行以前的命令：

```bash
!5
```

这将执行历史记录中第 5 行的命令。

### 3. 清除命令历史：

```bash
history -c
```

这不会删除历史文件；它只是清除当前会话的历史记录。

## 43. iostat：报告 CPU 和 I/O 统计信息。

Linux 中的`iostat`命令用于报告设备、分区和 NFS（网络文件系统）的 CPU 和输入/输出（I/O）统计信息。它提供了系统性能的综合概述，帮助用户识别潜在的瓶颈并监控资源使用情况。

**示例：**

### 1. 显示 CPU 使用率统计信息：

```bash
iostat -c
```

### 2. 以 2 秒为间隔显示设备使用率统计信息，共 5 次报告：

```bash
iostat -d 2 5
```

### 3. 以每秒兆字节为单位显示设备和分区的扩展统计信息：

```bash
iostat -x -m
```

### 4. 带时间戳显示 NFS 统计信息：

```bash
iostat -N -t
```

## 44. fuser：识别正在使用文件或套接字的进程。
