
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

在默认配置中，`aide --init`命令会检查`/etc/aide.conf`文件中定义的一组目录和文件。要在 AIDE 数据库中包含额外的目录或文件，并更改它们的监控参数，请相应地编辑`/etc/aide.conf`。

### 3. 开始使用 aide，从初始数据库文件名中删除 `.new` 字符串：

```bash
# mv /var/lib/aide/aide.db.new /var/lib/aide/aide.db.gz
```

### 4. 要更改 AIDE 数据库的位置，请编辑`/etc/aide.conf`文件并修改`DBDIR`变量。为了额外的安全，请将数据库、配置和`/usr/sbin/aide`二进制文件存储在安全位置（例如只读介质）。

## 7.3. 更新 AIDE

在验证更改后，`aide --init`命令会检查`/etc/aide.conf`文件中定义的一组目录和文件。要在 AIDE 数据库中包含额外的目录或文件，并更改它们的监控参数，请相应地编辑`/etc/aide.conf`。

### 附加资源

- LUKS 项目主页
- LUKS 磁盘上格式规范

## 8.2. RHEL 8 中的 LUKS 版本

在 RHEL 8 中，LUKS 加密的默认格式是 LUKS2。旧的 LUKS1 格式仍然被完全支持，并作为与早期 RHEL 版本兼容的格式提供。

LUKS2 格式的设计是为了以后对各个部分进行更新，而无需更改二进制结构。LUKS 内部使用 JSON 文本格式存储元数据，同时它可以检测元数据损坏，并允许从元数据副本进行自动修复。

> 注意
> 在需要兼容仅支持 LUKS1 的旧系统中，请使用 LUKS2。请注意，RHEL 7 从 7.6 版本开始支持 LUKS2 格式。

> ### 警告
> LUKS2 和 LUKS1 使用不同的命令加密磁盘。对 LUKS 版本使用错误的命令可能会导致数据丢失。

| LUKS 版本 | 加密命令 |
|---|---|
| LUKS2 | `cryptsetup reencrypt` |
| LUKS1 | `cryptsetup-reencrypt` |

## 在线重加密

LUKS2 格式支持在设备在使用时对已加密设备进行重加密。例如，你无需卸载设备上的文件系统即可执行以下任务：

- 更改卷密钥
- 更改加密算法

在加密未加密设备时，你必须卸载文件系统。在加密简短初始化后，你可以重新挂载文件系统。

LUKS1 格式不支持在线重加密。

## 转换

LUKS2 格式的灵感来源于 LUKS1。在某些情况下，你可以将 LUKS1 转换为 LUKS2。在以下特定场景下无法进行转换：

- LUKS1 设备被标记为由基于策略的解密（PBD - Clevis）解决方案使用。当检测到某些 `luksmeta` 元数据时，`cryptsetup` 工具将转换该设备。
- 设备处于活动状态。在进行任何转换之前，设备必须处于非活动状态。

## 8.3. LUKS2 重加密期间数据保护的选项

LUKS2 提供了多个选项，在重加密过程中优先考虑性能或数据保护：

### 校验和 `checksum`

这是默认模式。它平衡了数据保护和性能。该模式在重加密区域存储扇区的单独校验和，因此恢复过程可以检测 LUKS2 已经重加密的扇区。该模式要求块设备扇区是原子。

### 日志 `journal`

这是最安全的模式，但速度最慢。该模式在二进制区域写入重加密区域，由 LUKS2 写入数据。

### 无 `none`

此模式优先考虑性能且不提供数据保护。它仅防止安全终止导致损坏，例如 `SIGTERM` 信号或用户按下 `Ctrl+C`。任何意外的系统崩溃或应用程序崩溃可能导致数据损坏。

你可以使用 `cryptsetup` 的 `--resilience` 选项来选择模式。

如果 LUKS2 重加密过程意外强制终止，LUKS2 可以通过以下方式之一执行恢复：

- 自动：在下次打开 LUKS2 设备的操作期间进行。此操作由 `cryptsetup open` 命令或通过 `system-cryptsetup` 挂载设备触发。
- 手动：通过在 LUKS2 设备上使用 `cryptsetup repair` 命令。

## 8.4. 使用 LUKS2 加密块设备上的现有数据

此过程使用 LUKS2 格式对尚未加密的设备上的现有数据进行加密。新的 LUKS 头存储在设备的头部。

### 前提条件

- 块设备包含一个文件系统。
- 你已经备份了数据。

## 第 8 章. 使用 LUKS 加密块设备

> 警告
> 在加密过程中，你可能会丢失数据：由于硬件、内核或人为故障。在开始加密数据之前，请确保你已经有了可靠的备份。

操作步骤

- 1. 卸载你加密的设备上的所有文件系统。例如：

```bash
# unmount /dev/sdb1
```

- 2. 为存储 LUKS 头留出可用空间。选择适用于你场景的以下选项之一：

  - 在加密逻辑卷的情况下，你可以扩展逻辑卷而不调整文件大小。例如：

```bash
# lvextend -L+32M vg0/lv0
```

  - 使用分区管理工具（如 `parted`）扩展分区。
  - 缩小设备上的文件系统。你可以使用 `resize2fs` 实用处理 `ext2`、`ext3` 或 `ext4` 文件系统。注意，你不能缩小 XFS 文件系统。

- 3. 初始化加密。例如：

```bash
# cryptsetup reencrypt \
  --encrypt \
  --init-only \
  --reduce-device-size 32M \
  /dev/sdb1 sdb1_encrypted
```

该命令会要求你输入密码并启动加密过程。

- 4. 挂载设备：

```bash
# mount /dev/mapper/sdb1_encrypted /mnt/sdb1_encrypted
```

- 5. 启动在线加密：

```bash
# cryptsetup reencrypt --reuse-only /dev/sdb1
```

附加资源

- 详情请参阅 `cryptsetup(8)`、`lvextend(8)`、`resize2fs(8)` 和 `parted(8)` 手页。

## 8.5. 使用带有分离标头的 LUKS 加密块设备上的现有数据

# 红帽企业 Linux 8 安全加固

此过程对块设备上的现有数据进行加密，且不为存储 LUKS 头创建可用空间。头存储在分离的位置，这也作为了额外的安全层。该过程使用 LUKS2 加密格式。

### 前提条件

- 块设备包含一个文件系统。
- 你已经备份了数据。

> 警告
> 在加密过程中，你可能会丢失数据：由于硬件、内核或人为故障。在开始加密数据之前，请确保你已经有了可靠的备份。

操作步骤

- 1. 卸载设备上的所有文件系统。例如：

```
# umount /dev/sdb1
```

- 2. 初始化加密：

```bash
# cryptsetup reencrypt \
--encrypt \
--init-only \
--header /path/to/header \
/dev/sdb1 sdb1_encrypted
```

将 `/path/to/header` 替换为分离 LUKS 头文件的路径。分离 LUKS 头必须是可访问，以便以后解锁加密设备。

该命令会要求你输入密码并启动加密过程。

- 3. 挂载设备：

```bash
# mount /dev/mapper/sdb1_encrypted /mnt/sdb1_encrypted
```

- 4. 启动在线加密：

```bash
# cryptsetup reencrypt --resume-only --header /path/to/header /dev/sdb1
```

### 附加资源

- 更多详情请参阅 `cryptsetup(8)` 手页。

## 8.6. 使用 LUKS2 加密空白块设备

此过程提供了关于使用 LUKS2 格式加密空白块设备的信息。

### 前提条件

- 一个空白块设备。

操作步骤

- 1. 将分区设置为加密的 LUKS 分区：

```
# cryptsetup luksFormat /dev/sdb1
```

- 2. 打开 LUKS 分区：

```
# cryptsetup open /dev/sdb1 sdb1_encrypted
```

这会解锁分区并将其映射到设备映射器。要执行此操作，你需要创建一个文件系统。例如：

```
# mkfs -t ext4 /dev/mapper/sdb1_encrypted
```

- 3. 挂载设备：

```bash
# mount /dev/mapper/sdb1_encrypted /mnt/sdb1_encrypted
```

### 附加资源

- 更多详情请参阅 `cryptsetup(8)` 手页。

## 第 9 章. 使用基于策略的解密配置加密卷的自动解锁

基于策略的解密（PBD）是一套技术，用于解锁硬盘和虚拟机上的加密卷。PBD 使用了多种解锁方法，例如用户密码、可信平台模块（TPM）设备、连接到系统的 PKCS11 设备（例如智能卡）或网络服务器。

PBD 还将不同的解锁方法组合成策略，使得能够以不同的方式解锁同一个卷。红帽企业 Linux 中 PBD 的当前实现包含 Clevis 框架和插件。目前有：

- `tang` - 使用网络服务器解锁
- `tpm2` - 使用 TPM 策略解锁

网络边界加密（NBDE）是 PBD 的子类，允许将加密卷绑定到特殊的网络服务器。NBDE 的当前实现包含了 Tang 服务器的 Clevis 插件以及 Tang 服务器本身。

## 9.1. 网络边界加密

在红帽企业 Linux 中，NBDE 通过以下组件和技术实现。

图 9.1 使用 LUKS 加密卷时的 NBDE 方案。`luksmeta` 包不用于 LUKS2 卷。

| CLEVIS 框架 | TANG 服务器 |
| :--- | :--- |
| Tang Clevis 插件 | |
| Jose Crypto Library | Jose Crypto Library |

Tang 是一个将数据绑定到网络呈现的服务器。当系统绑定到安全网络时，它使包含数据的系统可用。Tang 是无状态的，不需要 TLS 或身份验证。与托管型解决方案（服务器存储所有加密密钥并了解每个使用的密钥）不同，Tang 与任何客户端密钥交互，因此永远不会从客户端获取身份识别信息。

Clevis 是一个自动解密的插件化框架。在 NBDE 中，Clevis 提供 LUKS 卷的自动解锁。`clevis` 包提供了该功能的客户端实现。

## 9. 使用基于策略的解密配置加密卷自动解锁

Clevis pin（插件）是 Clevis 框架的插件。其中一种插件是实现与 NBDE 服务器——Tang 交互的插件。

Clevis 和 Tang 是提供网络绑定（network-bound encryption）的客户端和服务器组件。在 Red Hat Enterprise Linux 中，它们与 LUKS 配合使用，对根卷和非根卷进行加密解密，以实现网络磁盘加密。

客户端和服务器端组件均使用 Jose 库执行配置加密和解密操作。

当您配置 NBDE 时，用于 Tang 的 Clevis pin 会获取 Tang 服务器公布的非对称密钥列表。或者，由于密钥是非称的，可以从带外分发 Tang 的公钥列表，以便客户端在无法访问 Tang 服务器的情况下进行操作。这种模式被称为离线配置（offline provisioning）。

用于 Tang 的 Clevis pin 使用其中一个公钥生成一个唯一的、在密码学上强大的加密密钥。一旦使用该密钥对数据进行加密，密钥就会被丢弃。Clevis 客户端应将配置操作产生的状态存储在方便的位置。加密数据的过程就是配置步骤。

LUKS 2 (`LUKS2`) 是 Red Hat Enterprise Linux 8 中的默认格式，因此 NBDE 的配置状态存储在 LUKS2 头部中。`lukmeta` 软件包对 NBDE 配置状态的利用仅用于使用 LUKS1 加密的卷。用于 Tang 的 Clevis pin 同时支持 LUKS1 和 LUKS2，无需特殊指定。

当客户端准备访问其数据时，它会加载配置步骤中产生的元数据并响应恢复加密密钥。这一过程就是恢复步骤。

在 NBDE 中，Clevis 绑定一个 LUKS 卷插件，使其能够自动解锁。在成功完成绑定过程后，可以使用提供的 Drac unlock 解锁磁盘。

## 9.2. 安装加密客户端 - CLEVIS

使用此步骤在您的系统上部署并开始使用 Clevis 可插体系框架。

步骤

- 1. 在带有加密卷的系统上安装 Clevis 及其插件：

```
# yum install clevis
```

- 2. 要解密数据，使用 `clevis decrypt` 命令并提供 JSON Web Encryption (`JWE`) 格式的密文，例如：

```
$ clevis decrypt < secret.jwe
```

其他资源

- 快速参考，请查看内置的 CLI 帮助：

```
$ clevis
Usage: clevis COMMAND [OPTIONS]

clevis decrypt      使用加密时定义的策略进行解密
```

- `clevis encrypt sss` 使用 Shamir 秘密分发策略加密
- `clevis encrypt tang` 使用 Tang 绑定服务器策略加密
- `clevis encrypt tpm2` 使用 TPM2. 芯片绑定策略加密
- `clevis binds` 使用指定的策略绑定 LUKS 设备
- `clevis lists` 列出绑定到 LUKSv1 或 LUKSv2 设备的插件
- `clevis pass` 返回用于绑定特定插槽的 LUKS 口密码
- `clevis regen` 重新生成 LUKS 元数据
- `clevis report` 报告服务器端的任何密钥轮换
- `clevis unbind` 解除绑定到 LUKS 卷的插件
- `clevis unlock` 解锁 LUKS 卷

- 欲需更多信息，请参阅 `clevis(1)` 手页。

## 9.3. 在 SELinUX 强制模式下部署 TANG 服务器

使用此步骤部署运行在自定义端口并作为 SELinux 强制模式下限制服务的 Tang 服务器。

### 前提条件

- 已安装 `policycoreutils-python-utils` 包及其依赖项。

步骤

- 1. 要安装 tang 包及其依赖项，以 root 身份输入以下命令：

```bash
# yum install tang
```

- 2. 选择一个未占用的端口（例如 `7500/tcp`），并允许 tangd 服务绑定到该端口：

```bash
# semanage port -a t tangd_port -p tcp 7500
```

注意，一个端口只能被一个服务使用，因此尝试使用已占用的端口将返回 `ValueError: Port already defined` 错误信息。

- 3. 在防火墙中打开端口：

```bash
# firewall-cmd --add-port=7500/tcp
# firewall-cmd --runtime-to-permanent
```

- 4. 启用 tangd 服务：

```bash
# systemctl enable tangd.socket
```

- 5. 创建覆盖文件：

```bash
# systemctl edit tangd.socket
```

- 6. 在编辑界面中（打开了位于 `/etc/systemd/system/tangd.socket.d/` 目录下的空 override.conf 文件），通过添加以下行将 Tang 服务器的默认端口从 80 更改为之前指定的数字：

```
[Socket]
ListenStream=
ListenStream=7500
```

保存文件并退出编辑器。

- 7. 重新加载更改的配置：

```bash
# systemctl daemon-reload
```

- 8. 检查您的配置是否生效：

```
# systemctl show tangd.socket -p Listen
Listen=[:]:7500 (Stream)
```

- 9. 启动 tangd 服务：

```bash
# systemctl start tangd.socket
```

由于 tangd 使用 system socket 激活机制，服务器会在第一个连接进入时启动。在首次启动时会自动生成一组新的加密密钥。要执行手动生成密钥等加密操作，请使用 `jose` 工具。

其他资源

- `tang(8)` 手页
- `semanage(8)` 手页
- `firewall-cmd(1)` 手页
- `systemd.unit(5)` 和 `systemd.socket(5)` 手页
- `jose(1)` 手页

## 9.4. 轮换 Tang 服务器密钥并更新客户端上的绑定

使用以下步骤轮换您的 Tang 密钥并更新客户端上的现有绑定。轮换密钥的精确间隔取决于您的应用程序、密钥大小以及机构策略。

前提条件

- Tang 服务器正在运行。
- 客户端上已安装 `clevis` 和 `clevis-luks` 包。
- 注意 `clevis list`、`clevis luks report` 和 `clevis luks regen` 已在 RHEL 8.2 中引入。

步骤

- 1. 要轮换密钥，在 Tang 服务器的 `/var/db/tang` 密钥数据库目录下使用 `/usr/libexec/tangd-keygen` 命令生成新密钥：

```
# ls /var/db/tang
# /usr/libexec/tangd-keygen /var/db/tang
# ls /var/db/tang
```

- 2. 检查 Tang 服务器是否接受新密钥，例如：
