
72 2022年10月第263期 `LINUX-MAGAZINE.COM` | `LINUXPROMAGAZINE.COM`

## LINUX KOREADER 电子阅读器

图 3：配置状态栏。

虽然墨水屏不需要屏保，但将简单的 `Sleeping`（睡眠）替换为更有信息的内容（例如当前书籍以及你的阅读进度）并没有问题。打开顶部栏，选择 `Settings | Screen | Screensaver`（设置 | 屏幕 | 屏保），并启用 `Use list's book cover`（使用列表书籍封面）。在 `Settings | Screensaver` 中开启 `Add message to screensaver`（向屏保添加消息）选项，并设置显示当前页码和总页数的百分比（图 4）。

图 4：配置自定义屏保。

`Web Clipper` 部分。启用 `Web Clipper Service`（网页剪贴板服务）并复制自动生成的标记代码（图 5）。`Joplin` 插件。安装软件包。要在 `Ubuntu` 和 `Linux Mint` 上获取，请运行：

```bash
sudo apt install install
```

将电子阅读器连接到电脑，并打开 `reader/settings.luat` 文件进行编辑。找到 `"exporter"` 部分并添加以下项目，将 `127.0.0.1` 替换为电脑的实际 IP 地址（使用令牌授权）。

## 进阶

处理好基础设置后，是探索 `KOReader` 提供的功能了。使用 `KOReader` 的配置文件（`profiles`），你可以快速方便地在多种配置切换。例如，你可以为夜晚创建一个配置（带有柔和亮度和冷色温），开启夜模式。你还可以创建一个同时开启前光和夜模式的白天配置。要创建配置，使用顶部栏并选择 `Tools | Profiles`（工具 | 配置文件），配置你的设置并点击完成。长按创建的配置以启用它。

就像任何有其特色的阅读应用一样，`KOReader` 支持将高亮导出为 `HTML`、`JSON` 和文本文件。如果你使用 `Joplin` [8] 作为你的笔记应用，`KOReader` 可以直接将高亮推送到其中。初始设置过程需要一些工作，但一旦完成，将笔记传输到 `Joplin` 就变得简单了。首先，你需要配置 `Joplin`。启动应用程序，选择 `Tools / Options`（工具 / ）。

图 5：在 `Joplin` 中启用 `Web Clipper`。

`LINUX-MAGAZINE.COM` | `LINUXPROMAGAZINE.COM` 2022年10月26日 73

## LINUX KOREADER 电子阅读器

```json
"joplin_IP" = "127.0.0.1",
"joplin_token" = "authorization_token",
"joplin_port" = 4188,
"joplin_export" = true
```

更改。从现在起，当你从授权的设备连接到电子阅读器时，无需输入密码。

## 备份 KOReader 的数据

保存更改并安全断开电子阅读器。在运行 `Joplin` 的电脑上，打开终端并运行以下命令：

对于每本书，`KOReader` 都会创建一个包含书籍设置、笔记、位置和内容的元数据文件。虽然你可以同步当前位置并导出，但保留所有重要数据的一个备份也是很有意义的。为了方便管理书籍和元数据，在电子阅读器上创建一个目录来存储所有书籍（例如 `Library`）。有两种方法可以实现这一点：

```bash
socat tcp-listen:4188,reuseaddr,fork tcp:localhost:4188
```

大多数 Linux 发行版的文件管理器都处理 `SSH` 和 `SFTP` 协议。你可以通过在地址栏中指定地址来访问电子阅读器的文件系统。例如：

```bash
sync -avz --delete -P "ssh -p 222" /mnt/root@127.0.0.1:2222
```

```bash
sync -avz --delete -P "ssh -p 222" /mnt/
ondir/library/user@127.0.0.1:/path/to/library
```

```bash
sync -avz --delete -P "ssh -p 222" /mnt/
ondir/backup/korader/user@127.0.0.1:/path/to/export
```

连接 `KOReader` 最简单的方法是无密码登录。这种方法也是最安全的，因为同一网络上的任何人都可以访问电子阅读器。为了限制仅允许授权设备访问，你需要在想要连接的设备上生成 `SSH` 密钥对。要在 `Linux` 上生成 `SSH` 密钥对，请在终端运行 `ssh-keygen` 命令。按照提示操作，但跳过密码：

与其使用内置客户端输入 `rsync` 命令，不如将所需的命令添加到 `reader/.ssh/bash_history` 文件中简化过程。或者，你可以使用一个脚本在 `/korader/scripts/dir/` 中创建一个名为 `backup` 的文本文件，并添加以下代码（根据需要调整示例）：

```bash
#!/bin/bash
sync -avz --delete -P "ssh -p 222" /mnt/
ondir/library/user@127.0.0.1:/path/to/library
sync -avz --delete -P "ssh -p 222" /mnt/
ondir/backup/korader/user@127.0.0.1:/path/to/export
```

```bash
cat ~/.ssh/* 将电子阅读器连接到电脑，并为 /korader/settings/ssh 目录创建 authorized keys 文件。对于文件编辑器，将密钥粘贴其中并保存
```

# KOREADER 电子阅读器 LINUX 语音

保存文件并赋予其执行权限：

```
chmod +x /koreader/scripts/up.sh
```

要在电子阅读器中启动脚本，请打开终端并运行 `koreader/scripts/backup.sh`。

如果你必须使用第二台电子阅读器，并想下载设置和数据，你只需要创建一个运行以下命令的脚本：

```
rsync -avh --delete -n -g --no-p -e "ssh -p 22" USER@127.0.0.1:/path/to/library/ /mnt/osboard/library/
rsync -avh --delete -n -g --no-p -e "ssh -p 22" USER@127.0.0.1:/path/to/clipboard/ /mnt/osboard/koreader/clipboard/
```

每当你运行上述脚本时，系统都会提示你输入两次密码，这很快就会非常麻烦。为了完成优化，请在 `KOReader` 中生成 `SSH` 密钥对，并将公钥添加到远程机器的授权密钥列表中。

要生成 `SSH` 密钥对，启动 `KOReader` 中的终端模拟器并按照提示操作，跳过指定密码。这将在 `/usr/local/iluje/usnet/etc/dot/` 目录下生成密钥对。为了确保密钥已在那里，

```
ssh-add -c "/usr/local/iluje/usnet/etc/ssh-id_rsa" -l
```

将 `ssh_id_rsa.pub` 复制到 `Linux` 机器，并使用以下命令将其添加到服务器上的 `authorized_keys` 文件：

```
cat id_rsa.pub | ssh USER@127.0.0.1 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

从现在起，你可以无需密码运行脚本（或任何需要通过 `SSH` 连接（到远程机器）的命令）。

# 结语

你不需要就此停止，`KOReader` 还有更多精彩内容。深入研究手势操作，你会发现你几乎可以用手势控制应用程序的每一个方面。如果你已经按照喜好配置了手势，可以探索 `KOReader` 的统计数据。简而言之，你会发现找不到比它更好、更强大的阅读应用了。如果你愿意花精力学习它的功能，你将获得一种以前从未想过的阅读体验。

# 信息

- [1] `KOReader`: `https://github.com/koreader/koreader`

- [2] `KOReader` wiki: `https://github.com/koreader/koreader/wiki`

- [3] `Joplin`: `https://joplinnapp.org`

- [4] `Kobustff`: `https://www.mobilireader.com/forums/showthread.php?t=254214`

# 作者

`Demir Popov` 多年来一直致力于关于 `Linux` 和开源软件的写作。他的文章发表在丹麦、英国、美国、德国、西班牙和俄罗斯的杂志上。你可以在他的个人网站 `tokyoma.com` 找到更多信息。

# LINUX 语音 0 A.D.

# 在 0 A.D. 中沉浸在活生的历史中

古代时代的重塑

在即时策略游戏 `0 A.D.` 中主宰古代文明的命运并复兴历史。
