
```
total 4149
dwxrxr-x- 2 34 archive 51 Jul 26 1992  forward
-rw-xr--x 1 34 archive uucp 06 Jul 26 1992  hushlin
-rw-xr--x 1 34 archive 59 Jul 31 1992  kermrc
drw-xr-x 1 34 archive 06 Jul 26 1992  notar
drw--s-x 5 34 archive 512 Jul 23 19:00 archive
drwxr-xr-x 1 34 archive 01 Jul 26 1992  archive ->
drwxr-xr-x 4 0 archive 512 Apr 02 16:29  bin
drwxr-xr-x 1 34 archive 23 Sep 14 1993  by-name.gz ->
drwxr-xr-x 1 34 archive 23 Sep 14 1993  index/by-name.gz
-rw-xr--x 1 34 archive 9011 Feb 26 1992 1991.compress
drw-xr--x 2 34 archive 09 Jul 23 18:50  /dev/null
drw-xr--x 2 34 archive 512 Jun 26 1992  dev
drwxr-xr-x 21 34 archive 1024 Sep 29 15:18
drwxr-xr-x 5 34 archive 512 Apr 14 16:42  faces ->
drw-xr--x 1 34 archive 31 Dec 08 1993  /archive/published/unix
drwxr-xr-x 2 34 archive 512 Jul 26 1992  ftp
drwxr-xr-x 10 34 archive 529 Sep 29 10:34  government
drwxr-xr-x 1 34 archive 1668 Sep 26 18:26
-rw-xr--x 1 34 archive 79820 Jul 11 20:54.gz
drwxr-xr-x 1 34 archive 17 Jul 26 1992  help -> info/archive
drw-xr--x 20 34 archive 1024 Dec 02 1993  index
drwxr-xr-x 19 34 archive 512 Sep 29 10:30
drwxr-xr-x 4 34 archive 512 Sep 29 15:36:10
drwxr-xr-x 25 34 archive 512 Sep 29 10:59  languages
```

![](img/bffdba228b65a1846f7f38a3801d7f2_582_0.png)

# 列表 27.2 继续

```
drwx-xr-x 4 34 archive 512 Sep 29 10:28 library
ddrw--s--x 2 34 archive 0 8192 Jul 26 1992 lostfound
drwxr-xr-x 1 34 archive 20 Aug 2 1992 ls-1R.Z -> index/ls1R.Z
drwxr-xr-x 1 34 archive 21 Sep 14 1993 ls-1R.gz -> index/ls1R.gz
drwxr-xr-x 1 34 archive 21 Aug 2 1992 ls-1tR.Z -> index/ls1tR.Z
drwxr-xr-x 1 34 archive 22 Sep 14 1992 sc-archive -> vendor/scro/index/ls
drwx-xr-x 24 34 archive 1024 Sep 29 15:16 networking
drwxr-xr-x 1 34 archive 512 Aug 10 09:26 packages
d--xrwx-x 17 34 archive 512 Sep 26 12:29 private
drwx-xr-x 25 34 archive 1536 Sep 29 15:30 pub
drwxr-xr-x 17 34 archive 1024 Sep 29 15:38 published
drwxr-xr-x 1 34 archive 10 Jul 26 1992 sc-archive -> vendor/sco
drwx-xr-x 20 34 archive 512 Sep 29 04:18 systems
drwxr-xr-x 14 34 archive 1536 Sep 29 15:36 tmp
drwxr-xr-x 1 34 archive 17 Jul 26 1992 unix-today -> vendor/unix-today
drwx-xr-x 36 34 archive 1024 Sep 29 15:29 uset
drwx-xr-x 6 0 archive 512 Oct 22 1992 usr
drwxr-xr-x 1 34 archive 16 Aug 2 1992 uumap -> networking/uumap
-rw-rw-r-- 1 34 3279899 Sep 28 21:05 uumap.tar.z
drwx-xrwx 3 210 archive 2560 Sep 24 15:36 uunet-info
drwx-xr-x 6 34 archive 1536 Sep 29 10:29 uevent
222 字节将在 07.6 秒 (4 Kbytes/s)
ftp>
ftp  cd systems/unix/linux
250-该子树内的文件自动从
250-tss-11.mit.edu/pub/linux 镜像
250-
250 CWD 命令成功。
ftp>
ftp  binary
200 类型设置为 I。
ftp  get sum.Z
200 PORT 命令完成。
150 正在为 sum.Z 打开 BINARY 模式数据连接 (80959 bytes)。
226 传输完成。
local: sum.remote: sum.z
80959 字节将在 5.6 秒 (14 Kbytes/s)
ftp  quit
221 再见。
$
```

在这里与 `.uu.net` 发起了 FTP 会话，这是互联网上一个主要的 FTP 存档站点。登录提示处提供的用户名是 anonymous，因为这是一个匿名 FTP。对于密码，使用了完整的电子邮件地址：`ftp.uu.net` 随后显示一个欢迎横幅，它提供了关于存档的一些信息。在这个示例中，你可以看到用户更改了目录、将模式设置为二进制、获取了压缩文件并退出。

![](img/bffdba228b65a1846f7f38a3801d7f2_584_1.png)

# 故障排除

我传输了一个二进制文件，但它运行不正常。我无法解压缩、解包或进行任何操作。确保你已将模式设置为二进制。

我正在传输大文件并想检查进度。使用 `hash` 命令。`ftp` 在每个数据缓冲区后打印 `#` 字符。数据缓冲区可能因版本而异，但通常为 1024、4096 或 8192 字节。

我尝试使用匿名 FTP，站点提示我用户未知且登录失败。你错过了匿名，或者该站点不支持匿名 FTP。过去匿名连接的惯例是使用 guest 作为密码。

# 使用 r- 命令

## login

`login` 命令与 `telnet` 命令非常相似，因为它允许你在远程系统上启动一个交互式命令会话。`rlogin` 的语法如下：

```
rlogin [-BEKdx] [-e char] [-k realm] [-l user-name] hostname
```

尽管最常用的用法是：

```
rlogin
```
