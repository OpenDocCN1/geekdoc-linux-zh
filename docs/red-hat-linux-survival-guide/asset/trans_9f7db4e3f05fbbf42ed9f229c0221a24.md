
```
# For the primary server
ftpd@206.171.50.50 : ALL : twist exec \
/usr/sbin/in.ftpd -l -a /etc/ftp/ftpaccess
```
```
# For the virtual FTP server
ftpd@206.171.50.51 : ALL : twist exec \
/usr/sbin/in.ftpd -l -a /etc/ftp/client1.ftpaccess
```
```
# For the second virtual FTP server
ftpd@206.171.50.52 : ALL : twist exec \
/usr/sbin/in.ftpd -l -a /etc/ftp/client2.ftpaccess
```

- 5. 现在创建 /etc/ftp 目录并将 /etc/ftpaccess 文件移入该目录。
- 6. 复制 /etc/ftp/ftpaccess 文件两份，使你拥有 /etc/ftp/client1.ftpaccess 和 /etc/ftp/client2.ftpaccess 文件。
- 7. 从用于邮件 FTP 服务器的 /etc/ftp/ftpaccess 文件中删除任何 virtual 关键字。
- 8. 修改 client1.ftpaccess 文件，使其包含如下行：
  virtual 206.171.50.51 root /home/client1/ftp
- 9. 同样地，修改 client2.ftpaccess 文件，使其包含如下行：
  virtual 206.171.50.52 root /home/client2/ftp
  不要忘记用你自己的 IP 地址和目录路径替换。
- 10. 现在将 anonftp 文件复制到 /home/client1/ftp 和 /home/client2/ftp 目录中。
- 11. 使用以下命令重启 xinetd 服务器：
  killall -USR1 xinetd
  就这样！现在你有两个虚拟 FTP 站点，可以通过各自的主机名或 IP 地址访问。

## 监控传输日志

日志记录对于 FTP 服务非常重要，因为你想知道谁在对你的文件进行什么操作。wu-ftpd 服务器在 xferlog 文件中记录传输，该文件通常位于 /var/log 目录中。你可以使用前面讨论过的 log 命令和 log transfers 关键字来自定义日志记录。

如果你有兴趣定期监控 xferlog，可以尝试 Dump xfer。你可以从以下 FTP 地址下载此软件包：

```
ftp://ftp.microimages.com/tools/dump_xfer.1.2.tar.gz
```

## 成为高效的 FTP 用户

本节我将向你展示如何有效地使用 FTP 服务从 FTP 服务器下载或上传文件。

## 使用命令行 FTP 客户端

几乎所有现代操作系统默认都提供命令行 FTP 客户端。是的，甚至较新的 Windows（98 或更新版本）也内置了命令行 FTP 客户端。有趣的是，各种流行操作系统上的几乎所有 FTP 客户端的行为都非常相似。因此，如果你知道如何使用 Linux FTP 客户端，你应该能够在 Windows 下甚至 Mac OS X（基于 FreeBSD）下使用它。

## 连接到 FTP 服务器

要从任何具有命令行 FTP 客户端的机器 FTP 到名为 ftp.domain.com 的站点，请从 Linux shell 或 X Window 系统下的 xterm 窗口运行 ftp ftp.domain.com 命令，或其等效命令。例如，在 Windows 下从 DOS shell 窗口运行此命令。

在 shell 窗口运行此命令后，FTP 客户端尝试连接到 FTP 站点。一旦连接成功，你将看到用户名和密码提示。输入适当的用户名和密码。如果你想以匿名用户身份访问远程 FTP 站点，可以输入 anonymous 或 ftp 作为用户名，然后输入你的电子邮件地址作为密码。

## 浏览 FTP 站点

登录后，你可以使用 cd 命令浏览目录，并使用 dir 或 ls 命令查看目录列表。任何时候你想知道当前正在浏览哪个目录，都可以输入 pwd 命令查看目录路径。

## 设置传输模式

默认情况下，大多数 FTP 客户端将传输模式设置为二进制，这应该适用于所有情况。如果在会话期间没有看到有关传输模式的消息，你可以通过输入 bin 或 binary 命令将其设置为二进制。如果出于某种原因需要切换到文本模式传输，可以输入 text 更改为文本模式。

## 下载文件和目录

要从站点下载文件，可以输入 get filename 命令。文件将被下载到本地系统的当前目录。要从目录获取多个文件，可以使用 mget filename1 filename2 filename3 [filenameN] 命令。

你也可以使用通配符，例如 mget *.file_extension 来下载具有特定扩展名的文件。例如，mget *.gif *.jpeg 允许你从远程 FTP 站点的当前目录下载本地系统当前目录中的所有 GIF 和 JPEG 文件。

使用 mget 命令时，你会注意到 FTP 客户端会在每个文件下载前提示你。如果你希望它在不逐个询问的情况下下载这些文件，只需使用 prompt 命令切换提示模式，然后运行 mget 命令即可。此外，如果你希望看到文件下载的视觉指示，可以输入 hash 命令在下载过程中切换 # 字符的显示。

![](img/9eb7e89292d2f85707b4d49102c865b7_456_0.png)

> 对于非常大的下载，显示 # 是无用的，因为你会得到很多满屏的 #。

如果你从 Linux FTP 服务器下载到 Linux FTP 客户端系统，你可以利用一个特殊功能，该功能通常也存在于其他基于 Unix 的 FTP 服务器中，允许你通过指定 get directory_name 命令下载整个目录。你甚至可以压缩传输，从而加快下载速度。例如，要以压缩模式下载名为 pub 的目录，可以输入 get pub.gz 命令。请注意，此类命令仅在 FTP 服务器允许此操作时才有效。

## 重新启动失败的下载

如果你的下载会话因系统或网络问题而失败，你可以在再次登录 FTP 服务器后发出 reget filename 命令重新启动下载。这是恢复大文件失败下载传输的绝佳技术。例如，如果你已下载了 30MB 文件中的 10MB 并因网络问题或系统错误而中断，可以再次连接到 FTP 服务器并为同一文件名发出 reget 命令。这将节省你的时间和减少带宽浪费。

## 上传文件

上传文件的先决条件是拥有向 FTP 服务器上传的适当权限。未经许可切勿向他人的 FTP 服务器上传文件；这可能被视为严重的刑事活动。

假设你有权限向已连接的 FTP 服务器上传文件，运行 put filename 命令即可从本地系统的当前目录上传指定文件。如果文件位于不同目录，可以使用 lcd 命令更改本地系统的当前目录。例如，如果你从 /tmp 目录启动 FTP 客户端，并且在 FTP 客户端提示符下想要从 /root/myfiles 目录上传文件，可以运行 lcd /root/myfiles 将本地系统的当前目录设置为 /root/myfiles。然后你可以运行 put 命令上传文件。

如果你想上传多个文件，可以运行 mput filename1 filename2 ... [filenameN] 命令，或使用通配符如 mput *.file_extension 上传特定扩展名的文件。

如果你有权限在 FTP 站点中创建/删除目录，可以分别使用 mkdir directory 和 rmdir directory 命令执行此操作。此外，如果你想在服务器上重命名文件，使用 rename filename 命令。

## 转到当前 shell

当你连接到 FTP 站点时，仍可以通过在 FTP 命令提示符下输入 ! 暂时转到当前 shell 窗口。你可以通过在 shell 提示符下输入 exit 命令返回到 FTP 会话。

## 中止文件传输

开始上传或下载传输后，你可以通过按住 Ctrl+C 键序列几秒钟来中止它。上传传输会立即中止；下载传输可能需要几秒钟或更长时间。

## 关闭 FTP 连接

完成上传或下载任务后，只需输入 quit 命令即可终止 FTP 连接。

## 使用 .netrc 自动执行 FTP 会话

如果你从一个或多个 FTP 站点执行常规下载或上传任务，可以通过在主目录中创建 .netrc 文件来节省输入。Linux FTP 客户端会自动读取此文件，以查找其当前连接的主机名的匹配记录。例如，列表 14-3 显示了主机名为 ftp.domain.com 的示例 .netrc 文件。

### 列表 14-3 一个示例 .netrc 文件

```
machine ftp.domain.com
login your_username
password your_password
macdef init
bin
prompt
cd /some/path
get filename
quit
```

每当你连接到 ftp.domain.com 时，此示例 .netrc 文件将从你的主目录（即 ~/.netrc）读取，并且 FTP 客户端
