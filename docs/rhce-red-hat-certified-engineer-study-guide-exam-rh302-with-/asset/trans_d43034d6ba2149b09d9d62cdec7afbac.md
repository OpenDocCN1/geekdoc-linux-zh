

特殊开关允许你覆盖这些检查，以便应对异常情况。本章的其余部分将结合你可能需要如何执行的常用操作，解释 rpm 在这些操作背景下的运行机制。

## 添加软件包

要安装一个包，请执行采用如下形式的命令：

```
rpm -i package_file_name
```

其中 `package_file_name` 指定包含你想要安装的包的文件名。如果你愿意，可以列出多个包或使用 shell 字符（如 `*`）来指定一组文件。例如，这里有一个典型的命令：

```
rpm -i gnorpm-0.9-10.i386.rpm
gnome-linuxconf-0.23-1.i386.rpm
```

该命令安装包含在 `gnorpm-0.9-10.i386.rpm` 包中的 gnorpm 包以及包含在 `gnome-linuxconf-0.23-1.i386.rpm` 包中的 gnome-linuxconf 包。当然，命令首先执行前述描述的检查；如果任何检查失败，命令将失败且不会安装任何指定的包。

许多系统管理员喜欢包含 `-v` 和 `-h` 标志，因为：

```
rpm -iv gnorpm-0.9-10.i386.rpm
gnome-linuxconf-0.23-1.i386.rpm
```

`-v` 标志导致命令在执行时打印状态信息；当你指定多个文件时，它特别有用，因为 rpm 在开始安装每个文件时都会打印一条消息。`-h` 标志导致 rpm 在安装每个包时显示 50 个哈希标记（#），帮助你直观地查看每个包的安装进度。这是一个包含这些标志的 rpm 典型调用：

```
# rpm -iv gnorpm-0.9-10.i386.rpm
gnome-linuxconf-0.23-1.i386.rpm
gnorpm
############################################
```

`-vh` 的优势之一是能够非常清楚地看出哪些包实际上已经安装了。RPM 一个令人困恼的缺点是，如果包已经安装，它将以错误信息退出。如果没有 `-vh`，有时很难判断包列表中哪些包在 RPM 终止之前已经安装了。

另一个实用的 RPM 功能是支持存储在 FTP 服务器上的文件。与其下载包文件再安装该包，不如你通过执行如下形式的命令直接从 FTP 服务器安装：

```
ftp://server/path
```

其中 `server` 是匿名 FTP 服务器的主机或 IP 地址，`path` 指定了包文件的路径。例如，以下命令安装了位于 Red Hat 匿名 FTP 服务器上的一个包：

```
rpm -ivh ftp://contrib.redhat.com/i386/RedHat/RPMS/
gnorpm-0.9-10.i386.rpm
```

如果你需要通过特定账户访问 FTP 服务器，请执行采用如下形式的命令：

```bash
ftp://user:pass@server/path
```

其中 `user` 和 `pass` 指定用户 ID 和密码，其余标记具有之前给出的名称。如果服务器在非标准端口上监听，你可以使用此命令形式：

```
ftp://user:pass@server:port/path
```

其中 `port` 是服务器监听的端口号。Red Hat Linux 6.2 及更高版本的 RPM 支持文件名通配符，允许你包含通配符。例如，安装 gnorpm 的 RPM 命令可以写为：

```
rpm -ivh ftp://contrib.redhat.com/i386/RedHat/RPMS/
gnorpm*
```

另一个实用的 RPM 功能是，你不需要以任何特定顺序指定包，即使指定的包中有一个或多个包依赖另一个包的功能。rpm 会检测任何依赖关系并按适当顺序安装包。

如果一个包所需的特性既由同一命令中指定的包提供，也不由已安装的包提供，则 rpm 命令会打印错误信息。例如：

```bash
# rpm -i gnorpm-0.9-10.i386.rpm
error: failed dependencies:
  usermode >=1.3 is needed by gnorpm-0.9-10
  librpm.so.0 is needed by gnorpm-0.9-10
```

要解决依赖关系，你必须安装相应的包以提供所需的特性，或者将现有包升级到更高版本。例如，错误消息表明需要较版本的 `usermode` 并且需要库 `librpm.so.0`。在本章中，你将学习如何发现一个包提供了哪些特性，以便你可以确定哪个包将提供 `librpm.so.0` 库。

如果你尝试安装与现有包或文件冲突的包，你将看到类似下面的错误信息：

```bash
# rpm -i gnorpm-0.9-10.i386.rpm
file /usr/bin/gnor install of gnorpm-0.9-10 conflicts with file from package-0.8-5
file /usr/share/gnome/apps/System/gnor.desktop install of gnorpm-0.9-10 conflicts with file from package-0.8-5
file /usr/share/gnome/help/gnor.html install of gnorpm-0.9-10 conflicts with file from package-0.8-5
```

