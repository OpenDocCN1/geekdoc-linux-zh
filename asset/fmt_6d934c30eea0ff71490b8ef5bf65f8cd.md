
```
ftp
Commands may be abbreviated. Commands are:
sendport site
addr size
account debug put status
append mget pid
end quit struct
ascii cls mode system
binary glob unix
hash hget never
help help status
case sect help
cd idle rename
cdup nlist tense
class image take
case open user
delete proxy send
```

一旦看到这些，你就会获得可以从本地机器下载文件的命令。以下对话显示了如何使用命令下载 `SMP-FAQ`：

```
ftp get SMP-FAQ
local: SMP-FAQ received
20 Type I transfer mode successful
150 Opening BINARY data connection to SMP-FAQ (42072 bytes).
226 Transfer complete in 7.02 seconds (5.9 Kbytes/sec)
42072 bytes received
```

第一个命令告诉远程系统向你的本地机器发送名为 `SMP-FAQ` 的文件。FTP 服务器检查文件是否存在以及获取它的权限。下一行确认传输的开始。第四行在传输启动时显示。第五行指定了类型（文本或二进制）、正在传输的文件名以及文件大小。传输完成后，将显示 `Transfer Complete` 消息，行显示传输状态。最后，出现 FTP 提示符等待你的下一个指令。

以下对话显示了如何获取特定命令的帮助：

```
ftp help cdup
change remote directory to parent directory
```

此对话显示了如何使用内置帮助系统。通过查询 FTP 命令（如前面的示例所示），你可以获取特定命令的帮助。之前的对话演示了获取 `cdup` 命令的帮助。虽然信息并不详细，但足以理解该命令。更多可用命令请参考 `ftp` 手册。

最后，我们通过以下对话结束工作示例：

```
ftp close
221-You have transferred 42072 bytes in 1 file.
221-Total transfer for this session is 5632 bytes in 5 transfers.
221-Goodbye.
```

### 在 Linux 内部

| 选项 | 说明 |
|---|---|
| `-M` | 启用多宿主模式。 |
| `-S` | `tcppd` 将将匿名传输记录到 `/var/log/ftpd`。 |
| `-U` | 每个并发会话都会记录到 `/var/run/utmp`，可以使用 `show` 等命令进行查询。 |
| `-T` | 超时时间 - 允许请求的最大时间。 |
| `-t` | 空闲超时时间。 |
| `-u` | 更改取消权限掩码（`unmask`）。默认值为 `027`。 |

请务必检查你所在发行版的 `ftpd` 手页；你所在发行版的选项可能有所不同。当指定守护进程处理 FTP 请求时，这将在 `/etc/inetd.conf` 文件中进行标识。

以下是适用于 SuSE 6.2 Linux 发行版的 `/etc/inetd.conf` 文件的片段。这里的区别在于 SuSE 倾向于让 `inetd` 启动 `tcpd` 守护进程而不是 `ftpd`。`tcpd` 守护进程是各种互联网服务的控制设施。

```
# 这些标准服务。
# ftp stream tcp nowait /usr/sbin/tcpd.su.ftpd -a
# ftp stream tcp nowait /usr/sbin/tcpd.in.ftpd #
```

`tcpd` 程序可以监控 `telnet`、`finger`、`ftp`、`exec` 和 `talk` 等请求。当请求进来时，`inetd` 守护进程会运行 `tcpd` 程序而不是实际的服务器进程。然后，`tcpd` 会记录请求、进行清理工作，并运行相应的服务进程。

如你所见，这包含了启动 `tcpd` 守护进程的示例选项（已注释掉）。你的文件看起来可能像这样，或者像你之前的示例一样——即 `ftp` 行没有被注释。

## FTP 目录结构

设置 FTP 目录是一个简单的过程。最简单的树结构由一个专为 FTP 指定的文件系统组成。一个直观的例子是使用 `/usr/ftp` 或类似的名称。根路径是什么并不重要；重要的是根路径之下的结构和内容。

FTP 服务需要若干目录。最基本的结构包含 `bin`、`dev` 等和 `lib`。每个目录的用途与其在 Linux 中的用途相对应。

二进制目录（`bin directory`）包含支持你的 FTP 服务所需的任何命令。最低要求是包含 `ls` 命令。根据我们之前的示例，完整路径将是 `/usr/ftp/bin`。你可能在 `/usr/ftp` 中需要的其他文件还有 `compress`、`gzip` 和 `tar`。

`dev` 目录持有 `/dev/zero` 的副本。`ld` 文件如通常一样，`ls` 命令将使用 `/dev/zero`。这在较新的 Linux 发行版中是这样的。要测试这一点，不要将 `/dev/zero` 复制到 `/usr/ftp/dev`；连接并运行 `ls` 查看发生了什么。请务必阅读 `lib` 目录以获取更多信息。如果你需要复制 `/dev/zero`，请务必使用 `link` 命令。你可能还需要 `/usr/ftp/dev` 目录下的 `tcp` 和 `udp` 文件。

接下来，你需要将 `passwd` 文件复制到 `/usr/ftp/etc`。接着复制 `group` 文件。这两个文件都可以在 `/etc` 目录中找到。用你喜欢的编辑器打开每个文件，删除除 `anonymous`、`ftp` 和 `bin` 以外的所有条目。然后，将所有密码替换为星号（`*`）。在密码条目中使用星号将允许访问该账户。

`lib` 目录是你需要创建的下一个目录。你将 `/lib/libc.so` 文件放置在 `/usr/ftp/lib` 目录。请务必复制实际版本文件（替换 `XXX`），例如 `libc.so.4.7.6` 或 `libc.so.6`。你的版本号可能与此处列出的不同。在复制文件之前，登录系统并检查你的 `libc.so` 文件是否匹配。

最后，需要创建 `pub` 目录。这个目录非常重要，因为这是用户连接到你的 FTP 站点的原因。你可以根据操作需要，在 `/usr/ftp/pub` 下创建任意数量的目录。至少，你可能为上传（`incoming`）、文档（`docs`）以及任何你可能需要的其他目录创建目录。

在 `/usr/ftp/pub` 下的每个目录中，你应该有一个 `README` 文件，用于描述当前目录的用途。你可能还需要一个 `CONTENTS` 文件，列出目录内容和每个文件的描述。

## 目录权限

设置目录结构的权限非常简单。你不会希望匿名用户使用你的 Linux 系统——这样做将是灾难性的。你如何防止用户跳出 FTP 沙箱？使用 `chroot` 命令。`chroot` 的语法如下：

```
chroot newRootDir [command]
```

该命令实际上更改了指定命令的根目录。如果没有指定命令，则将切换到用户的 `shell`。`chroot` 命令用于将根目录更改为 `/` 以外的其他目录。使用我们的示例，如果你为匿名用户将根设置为 `/usr/ftp`，则所有目录命令将相对于 `/usr/ftp` 目录。如果用户执行命令 `cd /pub`，当前目录将是 `/usr/ftp/pub`。

在上一节中，我建议你创建一个上传目录。这个目录是你的用户可以向 FTP 站点上传文件的地方。如果你允许上传功能，你必须为该目录提供执行和写入权限。通常做法要求你对该目录的所有文件进行审查。在你确定了文件的值后，可以将其移动到 `pub` 目录结构中的其他位置中。

## 配置 FTP

设置 FTP 服务器涉及配置多个文件。最重要的文件是 `/etc/ftpd.conf`。该文件控制 `ftpd` 守护进程的行为，包括哪些用户允许连接以及他们可以访问哪些目录。另一个文件是 `/etc/inetd.conf`。该文件定义了由 `inetd` 守护进程管理的服务。要启用 FTP，你可以在 `/etc/inetd.conf` 添加如下行：

```
# ftp stream tcp nowait /usr/sbin/tcpd.su.ftpd -a
```

配置好这些文件后，你需要重启 `ftpd` 或 `inetd` 守护进程使更改生效。你可以通过运行以下命令来实现：

`service ftpd restart` 或 `service inetd restart`

重启守护进程后，你应该测试你的 FTP 服务器是否正常工作。你可以通过从另一台机器连接到你的 FTP 服务器来测试。如果遇到任何问题，请检查配置文件是否有错误。

## 总结

在本章中，我们涵盖了 FTP 协议及其在计算机间传输文件的用途。我们讨论了如何设置 FTP 目录并配置必要的权限。我们还查看了如何配置 `ftpd` 和 `inetd` 守护进程。最后，我们展示了如何验证 FTP 服务器是否正常工作。
