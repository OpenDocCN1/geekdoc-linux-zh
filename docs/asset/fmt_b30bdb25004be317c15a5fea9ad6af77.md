
`kali@kali:~$ sudo apt update && sudo apt upgrade`

## 列表 274 - 更新软件包列表并升级软件包

虽然 Nessus 不可用于 Kali 软件仓库，但我们可以从 Tenable 网站手动下载适用于 Kali 的 64 位 `.deb` 文件：https://www.tenable.com/downloads/nessus。

我们可以通过点击下载页面上的“Checksum”链接（图 44）查看 SHA256 校验值，并使用 `sha256sum` 验证下载文件的校验和：

![](img/ec25e59d75726b7041242a56d3376832_211_0.png)

图 44：Nessus 下载和校验和

```bash
kali@kali:~/nessus$ sha256sum Nessus-X.X.X.deb

34199e8ff70bc1502b82495272cee2d313dc15ead1c0c1da6b851a32892d39d

Nessus-X.X.X.deb
```

列表 275 - 验证校验和

运行 `sha256sum` 后显示的值应与网站上显示的值匹配。请注意，此校验和取决于版本，可能与上图所示的不一致。

既然我们的校验和匹配，我们可以使用 `apt` 安装该软件包：

```bash
kali@kali:~/nessus$ sudo apt install ./Nessus-X.X.X.deb

...
Preparing to unpack .../kali/nessus/Nessus-X.X.X.deb ...
Unpacking nessus (X.X.X) ...
Setting up nessus (X.X.X) ...
Unpacking Nessus Scanner Core Components...
- You can start Nessus Scanner by typing /etc/init.d/nessusd start
- Then go to https://kali:8834/ to configure your scanner
Processing triggers for systemd (241-3) ...
```

列表 276 - Nessus 安装

安装完软件包后，我们可以启动 `nessusd` 服务：

```bash
kali@kali:~/nessus$ sudo /etc/init.d/nessusd start
Starting Nessus : .
```
