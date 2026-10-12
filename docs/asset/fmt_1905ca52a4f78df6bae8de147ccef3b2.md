
# LINUX 新手管理员指南，版本 0.201

## LINUX 快捷键与命令

### 6.9 X-windows 基础

`find /dev user "peter" imer`  
`find /home/peter -nouser -exec ls -l {} \ -ok chown peter.peter {} \`

上述命令打印所有属于用户 `peter` 的设备文件名。文件名输出到默认的 `stdout`，所以如果这是我需要的，就不需要指定。`root` 处理文件的所有权。

```
locate filename
```

查找包含字符串 `filename` 的文件名。比之前的命令更简单快速，但取决于一个数据库。

将 `MS Word` 文档转换为 `html` 格式。

```
executable_name
```

显示如果我在命令行输入其名称将运行的可执行文件路径。例如，此命令：

`mozilla`  
`which` 在系统上产生：`/usr/bin/mozilla`

```
whereis command
```

打印命令 `command` 的二进制文件、源码和手册页文件的位置。

```
grep -r 'celeste' . |more
```

（两个命令，使用在你的系统上有效的那个）。搜索当前目录及其所有子目录下的所有文件（`-r` 选项代表“递归”）。示例字符串 `celeste`。打印文件名以及文件中包含搜索字符串的行号。

`kfind &`  
（在 `X` 终端中）。一个用于 `find` 和 `grep` 的 `GUI` 前端。非常好用。命令末尾的 `&` 让 `kfind` 在后台运行，从而让终端保持可用。

`xinit &`  
启动一个精简的 `X-windows` 服务器（不带窗口管理器）。`&` 让命令在后台运行。

`startx & :1`  
启动 `X-windows` 服务器和默认窗口管理器。工作原理类似于在带有 `Win.1` 的 `DOS` 中输入 `win`。

`startxx <-Alt+F7>, 等等。`  
在显示器 `1` 上开启另一个 `X-windows` 会话（默认打开在显示器 `0`）。你可以同时运行多个 `GUI` 终端。使用 `<ctrl><Alt+F7>` 在它们之间切换。

`term`  
（在 `X` 终端中）运行一个简单的 `X` 终端。输入内容将关闭它。对于 `Windows`，还有其他更“虚拟”的终端，例如流行的 `console`、`kvt`（两者都有）以及 `gnome-terminal`。如果你需要更华丽的，可以使用 `tyterm`。对于简单快速，我选择 `<xvt`。

`- startde`  
`gnome-session`  
`xfe`  
`afterstep`  
`AnotherLevel`  
`fwm2`  
`fwm`

（在 `X` 终端中）7 种不同的命令，使用启动你窗口管理器的那个。在裸机器的 `X` 终端中启动喜欢的窗口管理器。

`kstart --desktop 4 --iconify kwrite`  
（在 `X` 终端中）在第 4 个桌面启动工作程序（`KDE` 和 `Gnome` 都可以有多个桌面供用户切换，这样你可以保持所有窗口井井有序），并在启动时最小化该程序。当你以这种方式启动 `GUI` 程序，使其不会过度干扰你当前 `GUI` 中的工作时，这非常有用。

### 6.10 网络应用

`mozilla &`  
（在 `X` 终端中）运行 `Mozilla Web` 浏览器。当前浏览器是 `Mozilla 1.0.1`（2002年10月），非常好用。替代方案有 `alsokonqueror` 和 `galleon`（在终端中输入 `konqueror&galleon`）。

`mozilla -display host:0 &`  
（在 `X` 终端中）在当前机器上运行 `mozilla`，并将输出名为 `host` 的显示器 `0`。你的机器必须拥有在 `host` 上显示的权限（通常通过在 `host` 机器的终端执行 `host_current_machine_name` 命令）。其他 `X-windows` 程序也可以以此方式远程运行。

`lynx.file`  
查看 `html` 文件或通过 `lynx` 浏览文本。虽然 `lynx` 的外观或便利性不如基于 `GUI` 的浏览器，但不需要任何配置，只要你的网络正常即可。

`konqueror &`  
（在终端中）文件管理器和网络浏览器二合一。非常好用，在很多方面与 `mozilla` 很有竞争力。随 `KDE` 自带。

`pine`  
一个良好的、老式的文本模式邮件阅读器。另一个老式且标准的工具是 `Elm`。`Mozilla mail` 会从你的互联网账户读取邮件。`pine` 允许你读取“本地”邮件，例如你的或 `cron` 进程发送给家庭网络中计算机的邮件。该命令也可以用于读取/撰写邮件，但非常不方便——它旨在用于自动化脚本。

`mut`  
一个非常简单但极其实用且快速的邮件阅读器。

`mail`  
一个基础的电子邮件操作系统。查看前一个以获得更好的邮件阅读器。如果你想从 `shell` 脚本发送电子邮件，`mail` 是很好的选择。

`email &`  
（在终端中）`GUI` 邮件程序。我使用 `mail`，它比 `netscape mail` 好得多。我可以拥有多个账户并从 `smtp`（本地服务器）和 `pop3` 服务器（互联网提供商）获取邮件到收件箱。简单且支持数字签名。

`licq &`  
（在终端中）`icq` 即时通讯客户端。另一个好用的是`icq`。旧版本的发行版没有安装 `icq`，你需要下载并安装它。

`ix &`  
（在终端中）启动你喜欢的新闻组（`usenet`）阅读器。它比 `netscape` 内置阅读器好得多。

`talk usename`  
与当前登录在你机器上的另一个用户对话（使用 `talkusersame@mailename` 与另一台计算机的用户对话）。接受对话邀请的命令是 `talk username2`。如果有人尝试和你对话并干扰了你的工作，使用命令 `msg q` 拒绝接收消息。你可能需要使用 `who` 或 `w` 来确定当前登录的用户。

`telnet`  
使用 `TELNET` 协议连接到另一台机器。远程机器或 `IP` 地址。你必须在远程登录处拥有账户。`telnet` 连接到另一台机器并让你对其操作，就像坐在它的键盘前一样（几乎）。`telnet` 在网中看到的所有内容都是明文的，你输入的也是。使用 `ssh`（需要某些设置）进行加密传输。

`login server`  
（=远程登录）连接到另一台机器。使用当前会话的用户名/密码；如果失败，则会提示。

`rsh`  
（=远程登录）连接到另一台机器。使用当前会话的用户名/密码；如果失败，则会提示。

`ssh server`  
（=远程登录）连接到另一台机器。使用当前会话的用户名/密码；如果失败，则会提示。

`telnet`  
（=远程登录）连接到另一台机器。使用当前会话的用户名/密码；如果失败，则会提示。

`telnet`  
（=远程登录）连接到另一台机器。使用当前会话的用户名/密码；如果失败，则会提示。

# LINUX 新手工具指南，版本 0.201

## LINUX 快捷键与命令

(=`tar` 归档工具) 解压从互联网下载的压缩 `tar` 包 (*`tar.gz` 或 *`.tgz`)。

```
tar xvf filename.tar
```

解压压缩的 `tar` 包 (*.`tar`)

```
tar czvf /var/backups/backup.tar.gz /home
```

```
cd ; tar xzvpf /var/backups/backup.tar.gz "$file.rtf"
```

(作为 `root` 用户) 第二条命令显示了如何从备份中恢复文件。这不会包含我的 `tar` 包中的“点文件”（以点开头头的文件或目录）。

```
tar cvzf filename.tgz * [a-z]*
```

```
gunzip filename.gz
```

解压缩一个压缩文件 (*.`gz` 或 `.z`)。如果你想将文件压缩为 `zip` 格式，请使用 `zip`（也可用 `zip` 或 `compress`）。

```
zcat filename.gz
```

(=`zcat`) 显示压缩文件的内容。其他实用的无需预先解压缩即可操作文件的工具也可用：`zmore, zgrep...`

```
bunzip2 filename.bz2
```

(=`bunzip`) 解压缩使用 `bzip2` 压缩工具压缩的文件 (*.`bz2`)。用于大文件。

```
unzip filename.zip filename2
```

解压缩使用与 `DOS` 的 `ZIPK` 兼容的压缩工具压缩的文件 (*.`zip`)。

```
zip filename.zip filename2
```

```
unjar file.arj
```

提取 *`.arch` 归档文件的内容。

```
th a file.lh
```

提取 `larch` 归档文件的内容。

```
uencode -output filename
```

解码使用 `ucode` 编码的文件。`uu-` 编码的文件通常用于电子电子邮件中的非文本文件（=`uencode` 将任何文件转换为 `ASCII` 文件）。

```
cat filename | mimencode -o filename.mime
```

```
cat filename | mimemcode -u filename
```
