
### 7.1. 查看 `stratis-filesystem1` 文件系统的当前使用情况。

```
[servera] # stratis list
| 池 | 名称 | UUID | 创建 | 设备 |
| :--- | :--- | :--- | :--- | :--- |
| stratispool | stratis-filesystem1 | 546 MIB | Apr 08 2022 07:12 | /dev/stratis/stratispool/stratis-filesystem1 48e... |
```

### 7.2. 在 `stratis-filesystem1` 文件系统中创建一个 2 GB 的文件。运行命令可能需要一分钟完成。

```
[servera # dd if=/dev/urandom of=/stratis/file2 bs=1M count=2048
```

### 7.3. 验证 `stratis-filesystem1` 文件系统的用空间。输出显示 `stratis-filesystem1` 文件系统的用空间已增加。这确认了精简配置文件系统按需扩展。

```
[servera] # stratis filesystem list
| 池 | 名称 | UUID | 创建 | 设备 |
| :--- | :--- | :--- | :--- | :--- |
| stratispool | stratis-filesystem1 | 2.60 GIB | Apr 08 2022 07:12 | /dev/stratis/stratispool/stratis-filesystem1 48e... |
```

### 8. 为 `stratis-filesystem1` 文件系统创建一个名为 `stratis-filesystem1-snap` 的快照。快照允许你访问从 `stratis-filesystem1` 文件系统中删除的任何文件。

#### 8.1. 为 `stratis-filesystem1` 文件系统创建快照。运行命令可能需要一分钟完成。

```
[servera] - stratis snapshot stratispool stratis-filesystem1 stratis-filesystem1-snap
```

#### 8.2. 验证快照的可用性。

```
[servera] - stratis filesystem list
| 池 | 名称 | UUID | 创建 | 设备 |
| :--- | :--- | :--- | :--- | :--- |
| stratispool | stratis-filesystem-snap | 2.73 GIB | Apr 08 2022 07:22 | /dev/stratis/stratispool/stratis-filesystem1-snap 5774... |
| stratispool | stratis-filesystem1 | 2.73 GIB | Apr 08 2022 07:12 | /dev/stratis/stratispool/stratis-filesystem1 48e... |
```

#### 8.3. 删除 `/stratis/file1` 文件。

```
[servera -] rm /stratis/file1
rm: regular file '/stratis/file1'? y
```

#### 8.4. 创建 `/stratisvol-snap` 目录。

```
[root@servera ~] mkdir /stratisvol-snap
```

#### 8.5. 将 `stratis-filesystem1-snap` 快照挂载到 `/stratisvol-snap` 目录。

```
[root@servera ~] mount /dev/stratispool/stratis-filesystem1-snap \
/stratisvol-snap
```

#### 8.6. 验证你可以从快照中访问从 `stratis-filesystem1` 文件中删除的文件。

```
[root@servera ~] cat /stratisvol-snap/file1
Hello World!
```

### 9. 卸载 `/stratisvol-snap` 和 `/stratisvol` 卷。

```
[root@servera ~] unmount /stratisvol-snap
[root@servera ~] unmount /stratisvol
```

### 10. 从系统中移除 `stratis-filesystem1` 精简配置文件系统和 `stratis-filesystem1-snap` 快照。

#### 10.1. 销 `stratis-filesystem1-snap` 快照。

```
[root@servera ~] destroy stratis filesystem destroy stratispool stratis-filesystem1-snap
```

#### 10.2. 销 `stratis-filesystem1` 文件系统。

```
[root@servera ~] destroy stratis filesystem destroy stratispool stratis-filesystem1
```

#### 10.3. 以学生用户的身份返回工作站系统。

```
[root@servera ~] exit
[student@workstation~] exit
logout
Connection to server closed.
[student@workstation ~]$
```

# 管理存储栈

在本实验中，你将调整现有的逻辑卷大小，根据需要添加 LVM 资源，然后添加一个带有持久化挂载 XFS 文件系统的新逻辑卷。

## 预期结果

- 将 `server_01_lv` 逻辑卷调整为 768 MIB。
- 创建大小为 128 MIB 的新 `server_02_lv` 逻辑卷，并使用 XFS 文件系统。
- 将该卷持久挂载到 `/storage/data2` 目录。

## 开始之前

由于学生使用的是工作站机器，请使用 `lab` 命令为你的练习准备系统。

此命令将准备你的环境并确保所有所需的资源都已可用。

```
[student@workstation ~]$ lab start lvm-review
```

# 操作指令

在服务器机器上，挂载在 `/storage/data` 目录的 `server_01_lv` 逻辑卷空间不足，需要扩展到 768 MIB。你必须确保 `server_01_lv` 持久挂载在 `/storage/data1` 目录上。

`server_01_lv` LV 存在于 `server_01_vg` 卷组中。遗憾的是，它没有足够的空间来扩展现有的逻辑卷。`/dev/vdb` 上存在一个 512 MIB分区。在 `/dev/vdb` 磁盘上使用连续的 512 MIB 大小创建一个分区。

创建一个大小为 128 MIB 的 `server_02_lv` LV。在新卷上创建 XFS 文件系统。将新创建逻辑卷挂载到 `/storage/data2` 目录。

1. 在 `/dev/vdb` 磁盘上创建一个 512 MIB 的分区。将此分区初始化为物理卷 `PV`，并扩展 `server_01_vg` 卷组以使用该分区。
2. 将 `server_01_lv` 逻辑卷扩展到 768 MIB。
3. 在现有卷组中，创建一个大小为 128 MIB 的新 `server_02_lv` 逻辑卷。创建一个 XFS 文件系统并将其持久挂载到 `/storage/data2` 目录。
4. 验证新创建的 LV 已按所需大小挂载。

### 1.1. 以学生用户身份登录服务器机器并切换到 root 用户。

```
[student@workstation omitted...]
[student@server ~]$ sudo -i
[sudo] password for student: student
[root@server #]
```

### 1.2. 创建 512 MIB 分区并设置 lvm 分区类型。

## 第 6 章 | 管理存储栈

```
[root@server1 ~]# parted /dev/vdb mkpart primary 514MiB 1026MiB
[root@server1 ~]# parted /dev/vdb set 2 lvm
```

### 1.3. 向内核注册新分区。

```
[root@server1 ~]# udevadm settle
```

### 1.4. 将分区初始化为 PV。

```
[root@server1 ~]# pvcreate /dev/vdb2
Physical volume "/dev/vdb2" successfully created.
```

### 1.5. 使用新的 `/dev/vdb2` 扩展 `server_01_vg`
