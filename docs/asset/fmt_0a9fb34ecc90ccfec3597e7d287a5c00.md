
你会被问到一个问题，显然你应该选择一个既安全又好记的密码（或至少是安全的）。最好的做法是保留默认值，你可以随意更改的密码除外。现在按照该计划操作：

### mount union plain

将显示文件的某些版本，只留下加密版本。运行上面的命令，将出现计划的命令。这就是 `encryptfs` 的工作原理。文件系统是虚拟的，它是真实的，只有数据被写入到 `crypt` 中的加密文件中。一旦你挂载了分区，它就会受到保护，在重新挂载之前无法再次读取，而这需要你的密码。

### 便捷的加密

当然，有一种更简单的设置加密的方法：如果你想隔离安装，可以使用 `encryptfs` 这种保护你的家目录。例如，`encryptfs` 本身包含在 Linux 内核中，但你需要安装 `encryptfs-utils` 软件包才能与之工作。创建两个目录并创建一个加密计划：

### mount encryptfs crypt

---

### 翻译正文（剩余部分）：

- 这是你的文件在加密后的样子，其内容同样无法理解。

它并不局限于加密分区，还可以用于加密单个目录。如果你想隔离安装，可以使用此方法来保护你的家目录。例如，`encryptfs` 本身包含在 Linux 内核中，但你需要安装 `encryptfs-utils` 软件包才能与之工作。创建两个目录并创建一个加密计划：

### mount encryptfs crypt

你会被问到一个问题，显然你应该选择一个既安全又好记的密码（或至少是安全的）。最好的做法是保留默认值，你可以随意更改的密码除外。现在按照该计划操作：

| 名称 | 大小 |
|---|---|
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.el-qiptmc476XfFVNlWW...` |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` | 16 |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` |  |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` |  |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` | 5 |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` |  |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` |  |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` | 214 |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` |  |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` |  |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` |  |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` | 18 |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` | 13 |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` |  |  |
| `ENCRYPTFS_FNES`, `ENCRYPTED_FS_jf30fi5.elqiptmc476XfFVNlW...` |  |  |

### mount union plain

将显示文件的某些版本，只留下加密版本。运行上面的命令，将出现计划的命令。这就是 `encryptfs` 的工作原理。文件系统是虚拟的，它是真实的，只有数据被写入到 `crypt` 中的加密文件中。一旦你挂载了分区，它就会受到保护，在重新挂载之前无法再次读取，而这需要你的密码。

### 便捷的加密

当然，有一种更简单的设置加密的方法：如果你想隔离安装，可以使用 `encryptfs` 这种保护你的家目录。例如，`encryptfs` 本身包含在 Linux 内核中，但你需要安装 `encryptfs-utils` 软件包才能与之工作。创建两个目录并创建一个加密计划：

### mount encryptfs crypt

### mount union plain

### 便捷的加密

### setup-private

如果你想隔离安装，可以使用 `encryptfs` 这种保护你的家目录。例如，`encryptfs` 本身包含在 Linux 内核中，但你需要安装 `encryptfs-utils` 软件包才能与之工作。创建两个目录并创建一个加密计划：

### mount encryptfs crypt

# 使用 zCrypt 另一种方式加密驱动器

让你的数据免受导航到新位置的影响

虽然你可以使用用户账户和权限访问计算机上的数据，但这不足以防止入侵者访问你的私有文件。保持数据安全的唯一可靠方法是对其进行加密。当然，使用 `zCrypt` 进行加密是一个简单且易于操作的过程。你可以在分区内或 USB 闪盘上创建加密驱动器。此外，它还可以使用 `GPG` 对单个文件进行加密。

接下来，在密钥文件中输入加密文件的密码。请确保密码是字母和数字的混合，以增加猜解难度。还要记住，如果你忘记了密码，将无法恢复文件——这就是加密的意义所在！确认密码后，点击按钮（`Button`）创建文件。此过程取决于硬件情况，可能需要几秒钟。完成后，你将在指定的目标位置获得一个 `.zc` 扩展名的加密版本。文件处理完成后，原始文件将保持不变。

要安装 `zCrypt`，请访问 `http://github.com/zCrypt` 并下载最新的二进制包。该程序提供适用于 Debian 和 Ubuntu 的 `.deb` 安装包。下载程序包并使用你的工具进行解压。在解压后的文件夹中，切换到与你架构对应的文件夹（32 位机器使用 `x86`，64 位机器使用 `amd64`）。两个文件夹都包含四个可以使用 `dpkg` 安装的二进制包。在其他系统上，请使用你的工具进行安装。下载应用程序说明书，并按照 `BUILD-INSTRUCTIONS` 文件中的详细步骤开始使用。

你现在必须选择文件后才能创建和进行更改。为此，启动 `zCrypt` 并导航到 `>`。选择你想要加密的文件，并在目标字段中选择该文件的位置。输入你想要加密的密码并点击按钮。完成后，加密文件将创建在指定位置。只需按照上述步骤操作即可。

`zCrypt` 还支持加密加密，即对一个已经加密的消息再次进行加密，可以使用相同或不同的算法。

加密孤岛（Encrypted silos）在你仅需要保护少数文件时效果良好。它有点繁琐，仅适用于你不需要频繁读取或修改的文件。如果你需要保护大量文件，更好的方法是使用加密驱动器。

之后你应该做的第一件事之一是对所有你认为敏感的文件创建加密版本。为此，启动 `zCrypt` 并导航到 `>`。选择你想要加密的文件，并在源（`Source`）字段相邻的位置选择你想要加密的文件路径。`zCrypt` 将使用这些信息创建一个同名且以 `.zc` 结尾的文件——或者通过点击相邻的图标将其保存到其他处。

`zCrypt` 使用块设备加密，这意味着它可以加密特定设备内的所有内容。该设备可以是磁盘、分区，甚至是挂载为块设备的文件。通过设备加密，用户在将数据写入锁定设备之前，先在块设备上创建文件系统。加密后的存储空间看起来像大块随机数据，甚至不会显示其目录结构。

# 创建新卷

| 卷类型 | 名称 |
|---|---|
| `ext4` | `encrypt_data_v1.img` |
| `ext4` | `encrypt_data_v2.img` |
