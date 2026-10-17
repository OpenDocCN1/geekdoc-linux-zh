
以下是 `/etc/fstab` 中持久挂载 Stratis 系统的示例。

```
UUID=31b9...8c55 /dir xfs defaults,x-systemd.requires=stratisd.service 0 0
```

`x-systemd.requires=stratisd.service` 挂载选项延迟挂载文件系统，直到 systemd 启动 `stratisd.service`。

# 第 8 章 实现高级存储功能

## 引导练习

在本次练习中，你将使用 Stratis 管理功能创建池、卷和文件系统。

### 目标

你应该能够：

- 创建一个精简配置的文件系统。
- 验证 Stratis 是否能够动态增长。

### 开始之前

- 登录工作站。

### 步骤

- 1. 从工作站打开会话。
- 2. 切换到 root 用户。
- 3. 安装 `stratis` 和 `stratis-cli` 包。
- 4. 激活 `stratisd` 服务。
- 5. 确保 `stratispool1` 池存在。
  - 5.1 创建一个名为 `stratispool1` 的 Stratis 池。
  - 5.2. 验证 `stratispool1` 的可用性。
- 6. 使用块设备 `/dev/vdc` 扩展 `stratispool1` 的容量。
  - 6.1 将块设备 `/dev/vdc` 添加到 `stratispool1`。
  - 6.2 验证 `stratispool1` 的大小。
  - 6.3 验证当前作为 `stratispool1` 成员的块设备。

在池 `stratispool1` 中创建一个名为 `stratis-filesystem1` 的精简配置文件系统。在 `/stratisvol` 上的 `stratis-filesystem1` 上创建一个名为 `file` 的文件，内容为 `Hello World!`。

- 使用 `stratis filesystem create` 命令在 `stratispool1` 上创建精简配置文件系统 `stratis-filesystem1`。该命令可能需要一分钟时间完成。

```
[root@servera ~] # stratis filesystem create stratispool1 stratis-filesystem1
```

- 使用 `stratis list` 命令验证 `stratis-filesystem1` 的可用性。

```
[root@servera ~] # stratis filesystem list

| Pool Name | Used | Created | Device / UUID |
| :--- | :--- | :--- | :--- |
| stratispool1 | stratis-filesystem1 | 546 Mib | Mar 29 2019 07:48 | /stratis/stratispool1/stratis-filesystem1 8714...e7db |
```

注意 `stratis-filesystem1` 的当前使用情况。该文件系统的使用量将在后续步骤中按需增加。

- 使用 `mkdir` 命令创建名为 `/stratisvol` 的目录。

```
[root@servera ~] # mkdir /stratisvol
```

- 使用 `mount` 命令将 `stratis-filesystem1` 挂载到 `/stratisvol`。

```
[root@servera ~] # mount /stratisvol/stratispool1/stratis-filesystem1

stratisvol
```

- 使用 `mount` 命令验证 Stratis 文件系统 `stratis-filesystem1` 是否已挂载到 `/stratisvol` 上。

```
[root@servera ~] # mount

...output omitted...

/dev/mapper/stratis-1-5c0e...12b9-thin-fs-8714...e7db on /stratisvol type xfs

(rw,relatime,selabel,inode64,unit=2048,swidth=2048,noquota)
```

- 使用 `echo` 命令创建测试文件 `/stratisvol/file1`。

```
[root@servera ~] # echo "Hello World!" > /stratisvol/file1
```

### 8. 验证精简配置文件系统 `stratis-filesystem1` 是否随着文件系统上数据的增长而动态扩展。

#### 8.1. 使用 `stratis filesystem list` 命令查看 `stratis-filesystem1` 的使用情况。

```
[root@servera ~] # stratis filesystem list

| Pool Name | Used | Created | Device / UUID |
| :--- | :--- | :--- | :--- |
| stratispool1 | stratis-filesystem1 | 546 MiB | Mar 29 2019 07:48 /nstratis/stratispool/stratis-filesystem1 8714...e7db |
```

#### 8.2. 使用 `dd` 命令在 `stratis-filesystem1` 上创建一个 2 GiB 的文件。该命令可能需要一分钟时间完成。

```
[root@servera ~] # dd if=/dev/urandom of=/stratisvol/file2 bs=1M count=2048
```

#### 8.3. 使用 `stratis filesystem list` 命令验证 `stratis-filesystem1` 的使用情况。

```
[root@servera ~] # stratis filesystem list

| Pool Name | Used | Created | Device / UUID |
| :--- | :--- | :--- | :--- |
| stratispool1 | stratis-filesystem1 | 2.5 GiB | Mar 29 2019 07:48 /\nstratis/stratispool/stratis-filesystem1 8714...e7db |
```

前面的输出显示 `stratis-filesystem1` 的使用量已经增加。精简配置文件系统的增长动态扩展，以适应因创建 `/stratisvol/file2` 导致的实时数据增长。

- 9. 为 `stratis-filesystem1-snap` 创建快照。快照将让你能够访问从 `stratis-filesystem1` 中删除的任何文件。

#### 9.1. 使用 `stratis filesystem snapshot` 命令为 `stratis-filesystem1` 创建快照。该命令可能需要一分钟时间完成。

```
root@servera ~] # stratis filesystem snapshot stratispool1 \
stratis-filesystem1 stratis-filesystem1-snap
```

#### 9.2. 使用 `stratis filesystem list` 命令验证快照的可用性。

```
[root@servera ~] # stratis filesystem list

... omitted...

stratipool stratis-filesystem1-snap 2.53 GiB Mar 29 2019 10:28 /strastipool/stratis-filesystem1-snap 29d1...8a16
```

#### 9.3. 删除 `/stratisvol/file1`。

```
[root@servera ~] # rm /stratisvol/file1

rm: remove regular file '/stratisvol/file1'? y
```

#### 9.4. 使用 `mkdir` 命令创建 `/stratisvol-snap`。

```
[root@servera ~] # mkdir /stratisvol-snap
```

#### 9.5. 使用 `mount` 命令将 `stratis-filesystem1-snap` 快照挂载到 `/stratisvol-snap`。
