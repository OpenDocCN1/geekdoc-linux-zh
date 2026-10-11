
user$ `git config --global user.name "Howard Hawks"`

user$ `git config --global user.email "hawks@my-company.com"`

user$ `git clone https://github.com/git-book/hello-world.git`

user$ `cd hello-world`

```
第二个示例显示了如何在现有项目的 main 分支中快速修复错误。你可以使用 `git checkout` 切换到 main 分支。`git pull` 下载远程仓库中保存的所有更改。现在，你需要纠正错误，使用 `git commit` 保存你的更改，并通过 `git push` 将更改传回 origin 仓库：
```

user$ `cd directory/with/existing/git/repo`

user$ `git checkout main`

user$ `git pull`

user$ `my-favorite-editor files...`

user$ `git commit -a -m 'Bugfix login authentication'`

user$ `git push`

```
# glances [options]

根据应用程序的不同，同名包中的 `glances` 命令是 `top` 的现代替代方案，或者是以客户端/服务器模式运行的简单监控程序。后者需要相应的配置，但也允许通过网络浏览器访问监控数据。

当直接调用时，该命令相比 `top` 还提供了网络和 I/O 活动的概述以及文件系统的状态。颜色显示针对深色终端进行了优化。如果你设置了浅色背景，请使用 `--theme-white` 选项运行 `glances`（参见图 3）。

各种快捷键根据不同标准对进程进行排序：`C` 按 CPU 使用率，`I` 按 I/O 活动，`M` 按内存使用量，`P` 按名称，`T` 按运行时间。按下回车键，你可以根据搜索过滤过滤列表。其他快捷键可以隐藏信息或激活不同的显示模式。例如，`U` 在当前网络吞吐量和累计数据量之间切换。按下 `H` 调用帮助页面可以显示更多快捷键。

![](img/94f0b4d76a25250c220515a1d5bba83f_286_0.png)

**图 3** 使用“glances”进行监控

```
gnome-session-quit [options]
```

`gnome-session-quit` 程序显示一个对话，可以在其中注销、关机或重启计算机。

- `--force`：即使有未保存的文件也执行注销。此选项只能配合 `--logout` 使用。
- `--logout`：询问用户是否要注销。
- `--no-prompt`：在不进行提示的情况下执行注销。此选项只能配合 `--logout` 使用。
- `--power-off`：询问用户是否想关机。
- `--reboot`：询问用户是否想重启计算机。

```
gpassword [options] group
```

`gpassword` 实际上用于设置组密码。然而，组内多个成员必须知道的密码被认为是不安全的，因此不再使用。

尽管如此，`gpasswd` 仍然承担着重要的功能。在下面的变体中，它可以从组中删除一个用户：

```
root# gpasswd -d user group
```

这使得 `gpasswd -d` 成为 `usermod -a -G user` 的对应命令，后者是将用户添加到组中。

## gpg 或 gpg2 [options/commands]

`gpg` 用于加密、解密或对文件进行签名，并管理密钥。`gpg` 受无数选项的控制，仅在有限范围内适用于手动使用。该命令被邮件客户端用于加密和对消息签名，并被包管理工具用于验证包及其包源的完整性。

通过 `-c` 和 `-d` 选项，`gpg` 可用于文件的进行对称加密和解密。这虽然简单，但在安全性方面并不理想。所有其他选项都假设你想使用非对称加密：加密将使用你通信对方密钥的公钥部分，而解密将使用你自己的密钥的私钥部分。这假设你同时也使用 `gpg` 进行密钥管理。

`gpg` 旨在用于服务器和嵌入式环境，依赖于少数外部库。而 `gpg2` 是为桌面使用设计的。该版本还支持 S/MIME。除此之外，两个命令支持相同的选项。

- `--batch`
激活批处理模式。在此模式下不允许交互式命令，且没有交互。批处理模式用于脚本编程。

- `-c file` or `--symmetric file`
提示你输入密码，然后加密指定的文件，最后将结果保存为 `file.gpg`。

- `-cipher-algo zip/zlib/bzip2/none`
定义加密算法。默认情况下，`gpg` 使用 CAST5 算法。通过 `gpg --version` 命令可以确定可选择的算法。

- `-compress-algo zip/zlib/bzip2/none`
指定是否以及如何对数据压缩。使用 ZIP 过程作为标准。出于兼容性考虑，不建议使用 zip 或 none 以外的设置。如果源数据已经过压缩，则建议使用 `none`。否则，重新压缩将在不减少所需空间的情况下产生多余操作。

- `-d file` or `--decrypt file`
提示你输入密码，然后解密指定的文件，最后将结果写入标准输出。

- `--decrypt file > plain text`
解密指定的文件并将输出重定向到纯文本文件。该文件必须使用你自己的密钥的公钥部分加密。要解密它，你必须输入密钥的密码。

- `--encrypt file`
加密指定的文件并将其保存为 `file.gpg`。你交互交互地输入密钥的邮箱地址。密钥可能需要先使用 `--import` 保存到密钥数据库中。如果你在加密选项之前指定了 `--armor`，则加密后的文件将以 ASCII 格式保存。这需要更多空间，但简化了通过邮件转发。

- `--export name@host`
在指定文件中保存 `name@host` 密钥公钥部分的二进制表示。你必须将此文件传给向你发送加密文件或邮件的人。如果你在 `--export` 选项之前指定了 `--armor`，公钥将以兼容邮件的文本格式保存。

- `--gen-key`
创建一个新密钥并将其保存到 `.gnupg/pubring.gpg` 中。你需要输入各种数据：密钥所需的类型和长度，以及你的姓名、邮箱地址、密码等。

- `--import public-key-file`
将他人密钥的公钥部分导入你自己的密钥集合。这是为了向该人员发送加密文件或邮件所必需的。

- `-k` Or `--list-keys`
列出存储在 `.gnupg/pubring.gpg` 中的所有密钥。

- `--no-tty`
抑制警告信息的输出。

- `--passphrase-file file`
从指定文件中读取加密密码。

- `--passphrase-repeat n`
指定密码输入的频率。

- `-q` Or `--quiet`
静默模式，不输出调试信息。

- `--output file`
将输出写入指定的文件。

- `--verify file`
验证指定文件的签名有效性。

- `--version`
显示 `gpg` 的版本。

## 示例

- [费曼学习法](https://wiki.example.org/feynmans_learning_method)的灵感源于诺贝尔物理奖获得者`理查德·费曼`。

1. 运用费曼技巧，你只需花上`20 min`就能深入理解知识点，而且记忆深刻，*难以遗忘*。

```
if (condVar > someVal) {console.log("xxx")}
```

必须进行传输，以便正确处理此问题
（内部，`/dev/gpiochip4`）。

GPIO 编号作为额外参数传递，
其中 GPIO 的内部标识是相关的，
而不是 GPIO 触点条上的引脚编号：

```
user$ chip=4
```

（用于树莓派 5）

```
user$ gpioset $chip 7=1
```

（GPIO 7 = 将引脚 26 设置为高电平）

```
user$ gpioset $chip 7=0
```

（GPIO 7 = 将引脚 26 设置为低电平）

你可以同时控制多个输出（这里是 GPIO 7, 8 和 25）：

```
user$ gpioset $chip 7=0 8=1 25=0
```
