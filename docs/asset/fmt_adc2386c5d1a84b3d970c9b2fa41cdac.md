
`usermod` 命令以多种方式修改给定用户的账户，例如更改家目录：

`sudo usermod -d /home/another smith`

## 可用选项

*   `-a` 当将用户添加到组（`-G`）时，保留用户现有的组成员关系。
*   `-c string` 设置用户的注释字段（历史上称为 GECOS 字段）。这通常是用户的全名，但可以是任何字符串。
*   `-d dir` 将用户的家目录设置为`dir`。
*   `-s shell` 将用户的登录`shell`设置为`shell`。
*   `-u uid` 将用户的 ID 设置为`uid`。除非你确定自己在做什么，否则请省略此选项并接受默认值。
*   `-c string` 设置用户的注释字段（历史上称为 GECOS 字段）。这通常是用户的全名，但可以是任何字符串。
*   `-g group` 将用户的初始（默认）组设置为`group`，这可以是数字组 ID 或是组名，且必须已经存在。
*   `-G group1,group2,...` 使用户成为额外的、已存在的`group1`、`group2`等的成员。

`sudo find / -group friends -print > /tmp/friend.files`

因为`groupdel`不改变文件的组所有权。它只是简单地从`/etc/group`中删除了组名。任何属于被删除组的文件都将保留现在过时的组 ID。

# groupmod

`stdin` `stdout` `-file` `opt` `--help` `--version`

`groupmod [options] group`

`groupmod` 命令修改给定的组，更改其名称或组 ID：

`sudo groupmod -n newname friends`

`groupmod` 不影响任何属于该组的文件：它仅仅是更改了系统记录中的 ID 或名称。

## 有用选项

*   `-n name` 将组名更改为`name`（安全）。
*   `-g gid` 将组 ID 更改为`gid`（有风险）。任何具有原始组 ID 的文件现在将具有无效的组所有权，并需要清理。

# 安装软件包

*   `dnf` 适用于 RPM 文件的标准包管理器（`CentOS`、`Fedora`、`Red Hat`、`Rocky` 等）。
*   `yum` 适用于 RPM 文件的旧版包管理器。
*   `rpm` 在本地操作 RPM 包。
*   `apt` 适用于 DEB 文件的标准包管理器（`Debian`、`Deepin`、`elementary OS`、`Ubuntu`、`Kodachi`、`Linux MX`、`Mint`、`Nitrix`、`POP!_OS`、`Rescatux`、`Ubuntu`、`Zorin OS` 等）。
*   `aptitude` 适用于 DEB 文件的备用包管理器。
*   `dpkg` 在本地操作 DEB 包。
*   `emer` Gentoo Linux 的包管理器。
*   `pacman` Arch Linux 的包管理器（外加 `Garuda`、`EndeavourOS`、`Manjaro` 等）。
*   `zypper` openSUSE 的包管理器。
*   `flatpak` 基于容器的包管理器。
*   `snap` 基于容器的包管理器。

你的 Linux Linux 发行版附带了一个包管理器程序，可以通过命令行、GUI 工具或两者兼备来安装软件包。令人困惑的是，每个包管理器都有独特的命令，并可能使用不同的包文件格式。因此，作为 Linux 用户，你的首要任务之一就是学习哪种包管理器是你发行版的标准。如果你不确定正在运行哪种 Linux 发行版，以下命令中的一个应该给你提供提示：

```bash
cat /etc/issue
```

Ubuntu 22.04.2 LTS

`Running Ubuntu Linux`

```
more /etc/*-release
```

DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=22.04
DISTRIB_CODENAME=jammy
