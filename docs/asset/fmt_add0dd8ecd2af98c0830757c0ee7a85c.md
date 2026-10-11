
## 第 21 章：故障排除

- 1. 要进入电脑 BIOS 界面中的 Setup 设置模式，请执行以下操作：
    a. 重启电脑。
    b. 在几秒钟内，你应该看到 BIOS 界面，并显示要按哪个功能键进入 Setup 模式。（在 Dell 工作站上，是 `F2` 功能键）。
    c. 出现 BIOS 界面。（如果系统开始启动 Linux，说明你按功能键的速度不够快。）

- 2. 在 BIOS 设置界面，执行以下操作以确定你的电脑是 32 位还是 64 位的、是否包含虚拟化支持，以及你的网络接口是否支持 PXE 启动。

根据你的电脑和 Linux 系统，你的体验可能与我不同。不同电脑的 BIOS 设置界面不同。通常，你可以使用方向键和 `Tab` 键在不同列之间移动，并按回车选择条目。

    - 在我的工作站上，在 `System`（系统）标题下，我突出 `Processor Info`（处理器信息），可以看到我的是 64 位技术计算机。查看你电脑上的 `Processor Info` 或类似项目，查看你使用的处理器类型。
    - 在我的 Dell 设备上，在 `Onboard Devices`（内置设备）标题下，我突出 `Integrated NIC`（集成网卡）并按回车。出现的 `Integrated NIC` 界面让我选择启用或禁用网卡（开启或关闭），或启用 `RPL`（如果我通过网络启动电脑）。

- 3. 要中断启动过程进入 GRUB 引导程序，执行以下操作：
    a. 重启电脑。
    b. 在 BIOS 界面出现后，当你看到启动 Linux 系统的倒计时时，按下任意键（如空格键）。
    c. 出现 GRUB 引导菜单，允许你选择启动哪个操作系统内核。

- 4. 要将电脑启动到运行级别 1 以便进行系统维护，请进入 GRUB 启动界面（如上一个练习所述），然后执行以下操作：
    a. 使用方向键突出显示你想启动的操作系统和内核。
    b. 输入 `e` 查看启动操作系统的条目。
    c. 将光标移动到包含内核的行上。（该行某处应包含 `vmlinux` 字样。）
    d. 将光标移动到行尾，添加一个空格，然后输入 `1 init=bin/bash`。
    e. 按照指令启动新条目。你可能需要按 `Ctrl+X` 或回车；当看到新文本时，输入 `by`。

如果执行成功，你的系统将跳过登录提示并启动到 root 用户 shell，你可以在那里无需提供密码即可执行管理任务。

- 5. 要启动红帽企业 Linux（通过 RHEL 6.x）以便在每个服务启动时进行确认，请执行以下操作：
    a. 遵循之前的两个练习，但在内核行末尾不是数字 `1`，而是单词 `confirm`。
    b. 当启动过程到达启动运行级别服务时，系统会提示确认 `Y` 或拒绝 `N` 每个服务，或继续 `C` 直接启动所有其他服务。

请注意，此选项在最新的 Fedora 和 Ubuntu 中不可用。

- 6. 查看...（注：原文 OCR 文本截断/继续）

## 附录 B：练习答案

- 7. 如果你怀疑系统今天遭受了恶意攻击，并且重要的二进制文件已被修改，你可以在命令行输入以下命令来查找这些被修改的文件：`find directory -mtime -1`，针对目录 `/bin`, `/sbin`, `/usr/bin`, `/usr/sbin`。

- 8. 要安装并运行 `chrootkit` 以检查练习中的恶意攻击是否安装了 rootkit，请检查你的发行版并执行以下操作：
    a. 在 Fedora 或 RHEL 发行版上安装，在命令行中输入 `install chrootkit`。
    b. 在 Ubuntu 或基于 deb 的发行版上安装，在命令行中输入 `sudo apt-get install chrootkit`。
    c. 运行检查，在命令行中输入 `chrootkit` 并查看结果。

- 9. 要查找系统中任何位置设置了 SetUID 或 SetGID 权限的文件，在命令行中输入 `find / -perm /6000`。

- 10. 安装 `aide` 软件包，运行 `aide` 命令初始化 `aide` 数据库，将数据库复制到正确位置，并运行 `aide` 命令检查系统上的任何重要文件是否被修改。

```bash
# yum install aide
# aide -i
# cp /var/lib/aide/aide.db.new /var/lib/aide/aide.db
# aide -C
```

为了让输出更有趣，你可以在运行 `aide -i` 之前安装 `lemon` 包（在之前的练习中描述过），并在运行 `aide -C` 之前对其进行修改，以查看修改后的二进制文件在 `aide` 中的外观。

## 第 23 章：理解高级 Linux 安全

要完成这些练习，你必须安装 `gpg2` 包。Ubuntu 默认不安装该包，但在最近的 Fedora 和 RHEL 版本中已安装。

- 1. 要使用 `gpg2` 工具和对称密钥加密文件，请输入以下命令（`gpg2` 工具会要求输入密码来保护对称密钥）：
`$ gpg -c filename`

- 2. 要使用 `gpg2` 工具生成密钥对，请输入：
`$ gpg2 -gen-key`

- 你 必须提供以下信息：
    a. 你想要哪种非对称密钥：
        * RSA 和 RSA（默认）
        * DSA 和 ElGamal
        * DSA（仅签名）
        * RSA（仅签名）
    c. 密钥的有效期为多少天、周、月、年。（你也可以请求密钥永久有效。）
    d. 你的真实姓名、电子邮件地址和注释，用于创建公钥的 User ID
    e. 私钥的密码

- 3. 要列出你生成的密钥，请输入：
`$ gpg --list-keys`

- 4. 要使用 `gpg2` 工具加密文件并添加你的数字签名，请执行以下操作：
    a. 你必须先生成密钥环（练习 2）。
    b. 生成密钥环后，输入：
`$ gpg --output EncryptedSignedfile FileToEncryptSign`

要使用适当摘要工具确保下载的文件没有损坏，你必须执行以下操作。（记住，摘要也称为校验和。）

- a. 查看下载网站以获取 MD5 或 SHA-1 文件或数字。
- - 如果是校验和数字，你需要进入下一步。
- - 如果是校验和文件，你需要下载该文件，然后使用 `cat` 命令将校验文件的内容显示在屏幕上。

- b. 如果是 MD5，在命令行中使用以下命令并与网站上的 MD5 校验文件或数字进行对比：
`$ mdsum FirstDownloadedFile`

- c. 如果是 SHA-1 哈希值，在命令行中输入以下命令并与网站上的 SHA-1 校验文件或数字进行对比：
`$ shasum FirstDownloadedFile`

- 6. 要确定你 Linux 系统上的 `su`（哪个 `su`）是否感知 PAM，请输入：
`$ ldd (which su) | grep pam`
`libpam.so.0 => /lib64/libpam.so.0 (0x00007fac89d4b9400)`
`libpam_misc.so.0 => /lib64/libpam_misc.so.0 (0x00007fac89b5c4400)`

如果你 Linux 系统上的 `su` 感知 PAM，那么当你执行 `ldd` 命令时，你会看到列出的 PAM 库名称。

- 7. 要确定 `su` 命令是否具有 PAM 配置，请输入：
`$ ls /etc/pam.d/su`

如果文件存在，在命令行中输入显示其内容。PAM 内容使用以下任何项：`auth`, `account`, `password`, `session`。
`$ cat /etc/pam.d/su`

- 8. 在 Fedora 或 RHEL 系统上列出各种 PAM 模块，输入：
`$ ls /lib/security/pam*.so`
在 Ubuntu Linux 系统上列出各种 PAM 模块，输入：
`$ sudo find / -name pam*.so`

## 附录 B：练习答案

```bash
# chcon user_tmp /etc/test.txt
# ls -Z /etc/test.txt
-rw-r---- root unconfined u:object_r:user_tmp:t:s0 /etc/test.txt
# restore /etc/test.txt
# ls -Z /etc/test.txt:s0
-rw-r---- root unconfined u:object_r:etc_t:s0 /etc/test.txt
# rm /etc/test.txt
```

8. 要确定 Boolean 是否允许通过 FTP 访问其主目录并永久开启该 Boolean，请使用以下命令：

```bash
# getsebool -a | grep ftp
tftp_home_dir -- off
```
