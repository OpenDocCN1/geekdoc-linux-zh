

首先我们切换到目标目录，然后

- `x`—从 tar 归档中提取文件。
- `p`—保留权限。
- `f`—文件名将为 `.`，即保存 tar 文件的临时缓冲区。

## 压缩、加密和发送 tar 流

上一节中使用 tar 命令的文件复制技术也可以用于通过局域网或互联网（使用 ssh 命令）快速安全地复制目录结构。利用这些技术的一种方法是使用以下命令行，首先压缩指定目录的内容，然后将压缩并加密的归档流解压到远程主机上的指定目录中：

```
```bash
$ tar czvf - data_folder | ssh remote_host '\( cd ~/mybackup_dir; tar xzvf - )'
```
```

tar 命令用于创建、列出并压缩名为 `data_folder` 的目录中的文件。输出通过 ssh（安全 shell）命令传输并发送到名为 `remote_host` 的远程计算机。在远程计算机上，流随后被提取并保存在名为 `/mybackup_dir` 的目录中。发送流时系统会提示输入密码。

## 使用 cp 复制文件

要复制文件，我们可以使用 cp 命令。用于简单复制时的命令的一般格式为

```
```bash
$ cp -a source_directory target_directory
```
```

-a 参数等同于给出 -dpR，即

- `d`—取消引用符号链接（从不跟随符号链接）并复制它们指向的文件而不是复制链接本身。
- `p`—尽可能保留所有文件属性。（文件所有权可能会干扰。）
- `R`—递归复制目录。

cp 命令也可以通过使用 -avR 命令行选项来快速复制目录并保留权限。使用这些选项可保留文件和目录权限、提供详细输出，并递归复制和重新创建子目录。备份期间也可以通过重定向标准输出来创建备份日志，如下所示：

```
```bash
sudo cp -avR directory_to_backup destination_vol_or_dir 1>/root/backup_log.txt
```
```

或

```
```bash
sudo cp -avR ubuntu /test2 1>/root/backup_log.txt
```
```

此示例在名为 `/test2` 的卷上对名为 `/ubuntu` 的目录进行精确复制，并将备份报告 `backup_log.txt` 保存到 `/root` 下。

## 使用 `mc` 复制文件

Midnight Commander（可在 Universe 仓库中获得，软件包名为“mc”；有关如何启用 Universe 和 Multiverse 仓库，请参阅第 7 章“管理软件”）是一款命令行文件管理器，用于复制、移动和归档文件和目录。Midnight Commander 的外观和感觉与 DOS 时代著名的 Norton Commander 相似。通过在 shell 提示符下执行 `mc`，会显示文件系统的双窗格视图。它包含用于操作文件的下拉菜单选项和功能键。它还使用自己的虚拟文件系统，能够挂载 FTP 目录并显示 tar 文件、gzip 压缩的 tar 文件（`.tar.gz` 或 `.tgz`）、bzip 文件、DEB 文件和 RPM 文件的内容，以及从中提取单个文件。仿佛这还不够，mc 还包含用于 ext2/3 分区的 File Undelete 虚拟文件系统。通过使用 `cd` “更改目录”到 FTP 服务器的 URL，您可以使用 FTP 协议传输文件。Ubuntu 默认选择的字体在 tty 控制台（与 xterm 相反）中使用时使 mc 的显示显得难看，但不影响其性能。

图 13.4 显示了默认双面板显示的截图。按下 F9 键会展开菜单，按下 F1 会显示帮助文件。默认 GNOME 终端中的一个“功能”会拦截用于退出 mc 的 F10 键，因此请改用 F9 访问菜单中的退出项，或直接用鼠标单击底部的菜单栏。配置文件记录详尽，如果您了解 shell 脚本和正则表达式，似乎很容易扩展 mc 以适应您的系统。它是未运行 X 的服务器上文件管理的绝佳选择。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_333_0.png)

**图 13.4** Midnight Commander 是一个功能高度多样的文件工具。如果它在您的屏幕上显示不正常，请使用 `-a` 参数启动它以强制 ASCII 模式。

