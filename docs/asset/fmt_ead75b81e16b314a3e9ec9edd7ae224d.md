
- 重启 `xinetd` 守护进程。

```
/etc/init.d/xinetd restart
```

你配置了最简单的 AMANDA 系统。使用 `/dev/null` 设备简化了过程，因为它是一个没有物理意义的逻辑设备。写入该设备的所有内容都会被丢弃。

## 第13章：自动化备份

### 测试备份

现在测试备份系统。以下指令将测试你刚刚创建的简单 AMANDA 系统。注意客户端运行在服务器上。

- 1. 以 root 用户身份登录客户端 `chivas`。
- 2. 切换到 `amanda` 用户。

安装 AMANDA 软件包会创建 `amanda` 用户。你应该以 `amanda` 用户身份运行所有备份。以非特权用户运行备份可以减少你的安全风险。

- 3. 运行 `amdump` 程序开始示例备份。

```
/usr/sbin/amdump DailySet1
```

`DailySet1` 参数引导 `amdump` 使用你在 `/etc/amanda/DailySet1` 目录中修改的配置文件。AMANDA 客户端运行在服务器上。客户端运行 `tar` 工具对 `/etc` 目录进行存档。`tar` 的输出通过回环接口 `127.0.0.1` 发送到服务器。服务器将备份数据刷新到 `/dev/null` 设备。实际上没有保存数据，但此示例演示了 AMANDA 的基本配置和用法。

一旦 `amdump` 完成，你可以运行 `amcheck` 工具来显示备份状态。

```
/usr/sbin/amcheck -s DailySet1
```

你应该会看到类似下面的输出：

Amanda Server Host Check

WARNING: tapedev is /dev/null, dumps will be thrown away

Holding disk /var/tmp:186412 KB space available, that's plenty

NOTE: skipping tape checks

Server took 0.004 seconds

这表明 `/dev/null` 在不保存任何数据的情况下测试了备份系统。这也显示了可用空间。在使用真实介质进行备份时，此信息可以帮助判断是否有足够的存储空间。（AMANDA 还会备份结果发送给 `amanda` 用户。）

### 构建简单的备份系统

从上一节可以看出，AMANDA 的设置并不困难。本节将简单的“null”配置扩展为真实的备份系统。我们将客户端备份到真实介质。我们还展示了如何从备份中恢复数据。

在本节中，我们将 `/dev/null` 设备替换为磁盘驱动器。可以使用配置此系统。磁盘驱动器提供了快速且可靠的介质。以下章节描述了如何设置服务器和两个客户端。

#### 配置服务器

以下步骤描述了如何配置 AMANDA 服务器。该服务器通过磁盘驱动器作为备份介质对之前的“null”服务器进行了扩展。

- 1. 在服务器 `chivas` 上以 root 身份登录。
- 2. 从之前示例的备份中恢复原始 AMANDA 配置文件。

```
cd /etc/amanda/DailySet1
cp/* 
```
- 3. 编辑默认的 `/etc/amanda/DailySet1/amanda.conf`，创建一个刷新到硬盘的 AMANDA 服务器。设置设备以便我们可以使用硬盘：

```
tapedev "no-device"
wipedev "no-device"
changerdev "no-device"
```
- 4. 创建一个新的使用硬盘作为备份介质的光带类型；硬盘很便宜，你应该考虑使用驱动器作为备份介质。将 `length` 参数设置为你的磁盘大小（尽管你可以设置小于总可用空间的值）。`filemark` 参数用于定义光带标记之间的字节数。使用磁盘驱动器时，`filemark` 参数设置为零，因为没有需要。

```
tapetype Disk {
comment "Save to disk"
length 100 mbytes
filemark 0
speed 100 kbytes
}
```
- 5. 配置 Holding disk 指向备份磁盘。在接下来的示例中，整个磁盘被专用于备份磁盘。备份磁盘使用 ext 文件系统格式化并挂载到 `/backup`。

```
holdingdisk disk {
  comment "main holding disk"
  directory "/backup"
  use 500 Mb
}
```

备份磁盘也可以简单的目录或文件系统。在这种情况下，你使用以下目录参数：

```
directory "/dev/null"
directory "/backup"
```
- 6. 将 `reserve` 设置为 0。

```
reserve 0
```
- 7. 配置 `/etc/amanda/DailySet1/disklist` 文件以定义要备份的客户端目录。`disklist` 文件还控制在进行客户端备份时使用的 `dumptype`。

```
# server
localhost /home
```

这定义了一个 Linux 客户端。我们选择在客户端上备份任意目录 —`/etc`。本节描述了如何设置 AMANDA 服务器。下一节将显示如何设置客户端。

#### 配置客户端

之前的示例在同一台计算机上配置了客户端和服务器。该模型提供了构建工作系统最简单、最快的方法。本节扩展了示例，在独立的机器上创建一个 AMANDA 客户端。以下指令显示了如何在与服务器的客户端上安装和配置 AMANDA：

- 1. 以 root 身份登录客户端。
- 2. 如果你还没有安装，请从附带的 CD-ROM 安装 AMANDA 软件包。

```
rpm -ivh /mnt/cdrom/amanda*
```

注意 AMANDA 软件包会将 `amanda` 用户和组添加到系统中。后续配置都取决于它们。

- 3. 通过修改 `/etc/xinetd.d` 目录下的相应文件来启用 AMANDA。将 `amanda`、`amidxtape` 和 `amandaix` 文件中的 `disable` 参数更改为以下值：`disable = no`
- 4. 重启 `xinetd` 守护进程。

```
/etc/init.d/xinetd restart
```
- 5. 对配置文件进行备份。

```
cd /etc/amanda/DailySet1
mkdir Bak
cp * Bak
```
- 6. 修改 AMANDA 客户端上的 `.amandosts` 以标识运行备份的服务器和用户名：

```
chivas.paunchy.net amanda
```

你现在准备好从 AMANDA 服务器启动备份了。下一节描述了如何运行测试备份。

### 测试备份

现在测试备份系统。以下指令将测试你刚刚创建的简单 AMANDA 系统。注意客户端运行在服务器上。

- 1. 在服务器 `chivas` 上以 root 用户身份登录。
- 2. 切换到 `amanda` 用户。

```
su - amanda
```

安装 AMANDA 软件包会创建 `amanda` 用户。你应该以 `amanda` 用户身份运行所有备份。以非特权用户运行备份可以减少你的安全风险。

## 第13章：网络备份自动化

Amanda Tape 服务器主机检查

警告：`tapedv` 不是磁带，转储将被丢弃

存储磁盘 `/var/tmp/` 可用磁盘空间 184612 KB，这非常充足

注意：正在跳过磁带检查

服务器检查耗时 0.004 秒

这表明使用磁盘驱动器作为备份介质可以创建一个用于备份你网络的系统。该系统的优点是速度快且可靠。然而，你应该考虑在某个时候获取可移动介质。一种可能性是使用可写 CD-ROM。你可以使用 `cdrecord` 或 `gtoaster` 等工具将备份磁盘的部分或全部内容复制到 CDR 光。另一种选择是获取流式磁带机或带库。

日志还显示了存储磁盘的可用空间。这些信息将帮助你判断在使用真实介质进行真实备份时，你是否有足够的存储空间。

![](img/75465a3c65cedf6b73d2aa7a566f6512_382_0.png)

AMANDA 的下一个版本是 2.4.3，并将提供更好的基于磁盘的备份选项。版本 2.4.3 目前处于测试阶段。AMANDA 源代码托管在 SourceForge (`www.sourceforge.net`) 上，可以通过访问 `www.amanda.org/download` 找到。

### 恢复备份数据

如果你在备份期间启用了 `dumptype index` 参数，你可以使用 `amrecover` 应用选择性地恢复文件和数据。否则，你可以使用 `amrestore` 工具恢复整个 AMANDA 备份，无论备份是否包含索引。

以下指令说明了如何从此示例备份中交互式地恢复数据。这些指令假设你正在恢复上一个示例中通过 `DailySet` 控制的备份。

- 1. 首先：以 root 身份登录客户端 `toluca`。
- 2. 在 `/var/lib/amanda/.amadahosts` 中添加 root 用户。

```
toluca.paunchy.net amanda
toluca.paunchy.net root
```
- 3. 启动 `amrecover` 浏览器（指定配置文件和 AMANDA 服务器）。
