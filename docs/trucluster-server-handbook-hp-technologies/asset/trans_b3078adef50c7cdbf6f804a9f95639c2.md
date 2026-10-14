
预计从 HP、第三方供应商或开源社区进行安装。

对初始 Tru64 UNIX 系统磁盘进行分区，可以在开始 Tru64 UNIX 安装之前进行，也可以在 Tru64 UNIX 安装过程中进行。我们将展示两种方法，由您自行判断哪种方式更简单、更高效。

### 4.2.1.2.1 使用 disklabel(8) 命令进行分区

使用 disklabel(8) 命令对 Tru64 UNIX 系统磁盘进行分区，是在您真正开始安装 Tru64 UNIX 之前执行的。我们知道，您会问自己：“在尚未安装 Tru64 UNIX 的情况下，怎么能使用像 disklabel 这样的 UNIX 命令呢？”让我们来看看如何做到这一点：

- 在 Tru64 UNIX 安装的第一个提示符处，您可以退出安装程序，以便在用于 Tru64 UNIX 的磁盘上编辑并写入新的磁盘标签。

  ```
  Welcome to the Tru64 UNIX Installation Procedure
  This procedure installs Tru64 UNIX onto your system. You will be asked a series of system configuration questions. Until you answer all questions, your system is not changed in any way.

  0 The "Exit Installation" option stops the installation and puts your system in single-user mode with superuser privileges. This option is intended for experienced UNIX system administrators who want to perform file system or disk maintenance tasks before the installation. This option may also be used for disaster recovery on a previously installed system.

  Remember, you can always get extra information by typing help.
  1) U.S. English Installation
  2) Installation with Worldwide Language Support
  3) Exit Installation
  Enter your choice: 3
  ```

- 在 shell 提示符下，设置您将用于编辑磁盘标签的合适终端类型和编辑器。在我们的示例中，我们发现 vt100 终端类型配合 vi(1) 编辑器效果很好。

  ```
  # TERM=vt100; export TERM
  # EDITOR=/bin/vi; export EDITOR
  ```

- 下一步是确定要使用的磁盘。您应该已经大致知道要使用哪个磁盘。问题在于找到正确的那个。在本例中，我们将使用 dsk0，因为它是服务器本地的硬盘。

  ```
  # /sbin/bwxmgr -view device
  ...
  67: /dev/disk/cdrom0c        COMPAQ   CD-224E        bus-1-targ-0-lun-0
  68: /dev/disk/dak0c          COMPAQ   BD018635C4     bus-5-targ-0-lun-0
  ...
  ```

- 既然我们知道了要使用的磁盘，剩下的问题就是编辑并写出磁盘标签，对吗？嗯，差不多。我们知道系统磁盘各分区的大小（以 MB 为单位），但我们仍然需要知道在磁盘标签中应将每个分区大小改为多少。由于每个分区的大小是以 512 字节块为单位的，请使用以下算法来获取每个分区的适当大小：

  分区大小（MB）× 2048 = 分区大小（512 字节块）

  以下是几个示例：

  如果我们需要一个 512 MB 的分区，比如根分区（/），我们按如下方式计算分区大小：

  `512 * 2048 = 1048576`

  如果我们需要一个用于交换分区²的 4.5 GB 分区，则计算出的分区大小为：

  `(4.5 * 1024) * 2048 = 9437184`

  我们使用相同的算法来计算我们将在即将成为系统磁盘的磁盘上使用的其他三个磁盘分区。有关我们计划用于本地 Tru64 UNIX 系统磁盘的分区示例，请参见表 4-2。

- 既然我们已经确定了要使用的磁盘以及每个分区的大小，接下来就是在编辑标签之前，先在磁盘上写一个默认标签。

  ```
  # disklabel -r -w dsk0
  ```

- 最后，我们编辑该磁盘的磁盘标签，并将其写出到磁盘本身。

  ```
  # disklabel -e -r dsk0
  ```

- 要重新启动 Tru64 UNIX 安装，只需执行 restart 命令即可。

  ```
  # cd /
  # restart
  ```

### 4.2.1.2.2 使用磁盘配置应用程序进行分区

如果您通过图形用户界面（GUI）执行 Tru64 UNIX 的完整安装，则可以在不退出安装的情况下完成对系统磁盘分区的自定义修改。怎么做？从安装的 GUI 中，查看所选磁盘分区信息，方式如下

> 2 关于交换分区，请参见第 4.2.2 节。
