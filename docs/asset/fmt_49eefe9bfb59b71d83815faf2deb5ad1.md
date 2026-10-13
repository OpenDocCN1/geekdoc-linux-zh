
注意上一个命令中的位置 `1001 MB` 是第一个分区的结束点。这种方式 `parted` 确保新分区紧随其后，没有任何间隙。因为分区从 `1001 MB` 开始，命令将结束点设置为 `1501 MB` 以获得 `500 MB` 的大小。

### 4.2. 通过列出 `/dev/vdb` 上的分区来验证你的工作。

```
[root@servera ~]# parted /dev/vdb print
Model: Virtio Block Device (virtblk)
Disk /dev/vdb: 5360MB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags:
```

| Number | Start | End | Size |
|---|---|---|---|

| 1 | 1049KB | 1GB |

新分区的大小并不正好是 `500 MB`。这是因为 `parted` 必须将分区与磁盘对齐。

### 4.3. 运行 `udevadm settle`。该命令等待系统注册新分区并在任务完成后返回。

```
[root@servera ~]# udevadm settle
[root@servera ~]#
```

### 5. 初始化新创建的分区为交换空间。

```
[root@servera ~]# mkswap /dev/vdb
Setting up swapspace version 1, size = 476 MiB (49918080 bytes)
no label, UUID=cb7f71ca-ee82-430e-ad4b-7dda1263228
```

## 管理基础存储

- 使用 `parted` 命令显示和创建分区。
- 在分区上创建新的文件系统并持久地挂载它们。
- 创建交换空间（swap spaces）并在启动时激活它们。

## 开始之前

使用密码 `student` 以 `student` 身份登录工作站。

在工作站上，运行 `lab storage-review start` 命令。此启动脚本会定义服务器是否可以通过网络访问。它还准备了第二个脚本，用于运行练习所需的服务器。

```
$student@workstation ~$ lab storage-review-start
```

1. 服务器上有新的磁盘可用。在第一块磁盘上，创建一个名为 `backup` 的 `2 GB` 分区。由于可能很难设置精确的大小，因此在 `1.8 GB` 到 `2.2 GB` 之间的大小都是接受的。在该分区上设置正确的文件系统类型以托管 XFS 文件系统。

服务器上 `student` 用户账户的密码为 `student`。该用户可以通过 `sudo` 拥有完整的 root 权限。

2. 使用 XFS 文件系统格式化该 `2 GB` 分区，并将其持久地挂载到 `/backup`。

3. 在新磁盘上，创建两个名为 `swap1` 和 `swap2` 的 `512 MB` 分区。在 `460 MB` 到 `564 MB` 之间的大小都是接受的。在这些分区上设置正确的文件系统类型以托管交换空间。

4. 将两个 `512 MiB` 分区初始化为交换空间并在启动时配置它们。设置 `swap2` 分区的优先级高于另一个分区。

5. 为了验证你的工作，请重启服务器。确认系统已自动挂载位于 `/backup` 的分区。此外，确认系统已激活了交换空间。

## 评估

在工作站上，运行 `lab storage-review grade` 脚本以确认本次练习成功。

```
[student@workstation ~]$ lab storage-review grade
```

## 完成

在工作站上，运行 `lab storage-review finish` 脚本以完成实验。

```
[student@workstation ~]$ lab storage-review finish
```

本实验结束。

## 基础检查清单

## 性能检查清单

在本实验中，你将在新磁盘上创建多个分区，使用某些文件系统进行格式化并挂载它们，并将其他分区激活为交换空间。

### 成果

你应该能够：

* 使用 `parted` 命令显示和创建分区。
* 在分区上创建新的文件系统并持久地挂载它们。
* 创建交换空间并在启动时激活它们。

## 开始之前

使用密码 `student` 以 `student` 身份登录工作站。

在工作站上，运行 `lab storage-review start` 命令。该命令运行一个脚本，确定服务器是否可以通过网络访问。它还为 `serverb` 上的练习准备了第二块磁盘。

```bash
[student@workstation ~]$ lab storage-review start
```

1. `serverb` 上有新的磁盘可用。在第一块磁盘上，创建一个名为 `backup` 的 `2 GB` GPT 分区。由于可能很难设置精确的大小，因此在 `1.8 GB` 到 `2.2 GB` 之间的大小都是接受的。在该分区上设置正确的文件系统类型以托管 XFS 文件系统。

`serverb` 上 `student` 账户的密码为 `student`。该用户可以通过 `sudo` 拥有完整的 root 权限。

#### 1.1. 使用 `ssh` 命令以 `student` 用户身份登录服务器。系统已配置为使用 SSH 进行身份验证，因此不需要密码。

2. 使用 XFS 文件系统格式化该 `2 GB` 分区，并将其持久地挂载到 `/backup`。

3. 在新磁盘上，创建两个名为 `swap1` 和 `swap2` 的 `512 MB` 分区。在 `460 MB` 到 `564 MB` 之间的大小都是接受的。在这些分区上设置正确的文件系统类型以托管交换空间。

4. 将两个 `512 MiB` 分区初始化为交换空间并在启动时配置它们。设置 `swap2` 分区的优先级高于另一个分区。

5. 为了验证你的工作，请重启服务器。确认系统已自动挂载位于 `/backup` 的分区。此外，确认系统已激活了交换空间。

## 第 6 章 | 管理基础存储

### 6. 启用新创建的交换空间。

使用 `swapon --show` 命令显示创建和初始化交换空间并不会自动启用其使用。

```
[root@servera ~]# swapon --show
[root@servera ~]#
```

- 启用新创建的交换空间。

```
[root@servera ~]# swapon /dev/vdb2
[root@servera ~]#
```

- 验证新创建的交换空间现在已可用。

| NAME | TYPE | SIZE | USED | PRIO |
|---|---|---|---|---|

| dev/vdb2 | partition | 476 | 0B | -2 |

- 禁用交换空间。

```
[root@servera ~]# swapoff /dev/vdb2
[root@servera ~]#
```

- 确认交换空间已禁用。

```
[root@servera ~]# swapon --show
[root@servera ~]#
```

## 7. 配置新的交换空间在系统启动时启用。

#### 7.1. 使用带有 `--fs` 的 `lsblk` 命令发现 `/dev/vdb` 设备的 UUID。

```
[root@servera ~]# lsblk --fs /dev/vdb2 
| NAME | FSTYPE | UUID | MOUNTPoint |
|---|---|---|---|
| vdb2 | swap | cb7f71ca-ee82-430e-ad4b-7dda12632328 | |
```

验证输出中的 UUID 在你的系统上可能不同。

#### 7.2. 在 `/etc/fstab` 中添加条目。在以下命令中，将 UUID 替换为上一步发现的 UUID。

```
[root@servera ~]# vim /etc/fstab
...output omitted...
UUID=cb7f71ca-ee82-430e-ad4b-7dda12632328 swap defaults 0 0
```

#### 7.3. 更新系统以注册新的 `/etc/fstab` 配置。

```
[root@servera ~]# systemctl daemon-reload
[root@servera ~]#
```

#### 7.4. 使用刚刚添加到 `/etc/fstab` 的条目启用交换空间。

```
[root@servera ~]# swapon -a
[root@servera ~]#
```

#### 7.5. 验证交换空间已启用。

```
[root@servera ~]# swapon --show
| NAME | TYPE | SIZE | USED | PRIO |
|---|---|---|---|---|
| /dev/vdb2 | partition | 476M | 0B | -2 |
```
