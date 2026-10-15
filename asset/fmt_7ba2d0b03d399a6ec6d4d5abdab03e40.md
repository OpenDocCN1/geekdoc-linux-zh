
| `cdda:` | 像处理普通文件一样处理 CD 轨道 |
| `file:` | 访问本地文件系统 |
| `nntp:` | 使用新闻组访问数据 |
| `gzip:` | 窥探 `gzip` 存档 |
| `dav:` | 访问 WebDAV 服务器 |
| `pipe:` | 访问发送到管道的数据 |
| `ssh:` | 连接到 `SSH` 服务器 |
| `tar:` | 窥探 `tar` 存档 |
| `fonts:` | 访问字体信息 |
| `burn:` | 从内部刻录 CD |
| `themes:` | 访问系统上的桌面主题 |

#### 堆叠 VFS 模块

GNOME VFS URL 可以相互堆叠。例如，如果你有一个位于远程系统的压缩 `tar` 文件，你可以在 `http` URL 之上堆叠一个 `tar`。假设压缩 `/tmp/pics.tar` 包含一个名为 `freddie.jpg` 的图像，并且你想用 GNOME 查看它。GNOME VFS 文档告诉你可以使用以下格式查找 VFS URL：`url@suburl`。例如，如果你有一个包含 `bar.txt` 文件的存档 `/tmp/foo.tar`，`tar` 文档告诉你可以使用 `http://tmp/foo.tar@bar.txt`。注意那个额外的冒号：`@tar/bar.txt` 组件充当 HTML 文档中的命名锚点，而不是 VFS 模块。

如果你想查看的图片存储在压缩 `tar` 包中怎么办？简单，只需在堆栈上使用另一个 VFS 组件（`gzip`），例如：

`http://myserver.example.com/pics.tgz:gzip@tar://freddie.jpg`

你可以手动解压 `tar` 包并告诉归档打开 JPG 照片（提醒自己在完成后清理所有临时文件）。通过让 VFS 担心这些细节，你可以为自己节省时间。与其将图像提取到临时位置，你可以使用如下的 VFS URL：

```bash
$ eog file://tmp/pics.tar@freddie.jpg
```

这里是命令的各个部分是如何组合的。第一部分是你运行的命令名称（Eye Of Gnome）。接下来，你使用一种 URL 类型（`file://tmp/pics.tar`），它使用协议打开 `/tmp/pics.tar`。接下来是神奇的部分：`@tar/freddie.jpg`。这告诉 GNOME 将 `@tar` 之后的所有内容视为 `tar` 存档，并访问 `freddie.jpg` 成员。

## 16 技巧：让 GNOME 虚拟文件系统为你代力

| `dr-xr-xr-x 3 root root 0 Oct 3 2003` | `-rw-r--r-- 1 root 8364 Oct 3 10:28` | `/etc/confs/cdplayer.schemas` |
| `INFO` | | |
| `-rw-r--r-- 1 root root 0 Oct 3 2003` | `-rw-r--r-- 1 root 21092 Oct 3 10:27` | `/etc/confs/charpick.schemas` |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/VERSION-RELEASE` | |
| `INFO/GROUP` | | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/BUILDHOST` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/SOURCEMP` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/DISTRIBUTION` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/VENDOR` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/DESCRIPTION` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/SUMMARY` | |
| `dr-xr-xr-x 3 root root 0 Oct 3 2003` | `INFO/SCRIPTS` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/SCRIPTS/POSTIN` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/SCRIPTS/ALL` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/PACKAGER` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/URL` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/SERIAL` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/COPYRIGHT` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/LICENSE` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/MODTIME` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/RWPMVERSION` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/OS` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/SIZE` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/REQUINMENT` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/OBSOLETE` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/PROVIDES` | |
| `-r--xr--x-- 1 root root 0 Oct 3 2003` | `INFO/CHANGELOG` | |
| `dr-xr-xr-x 1 root root 63419 Oct 3 10:28` | `/etc/confs/schemas/battstat.schemas` | |

前 28 个文件是虚拟的，其余的是如果你安装了此包，则安装在你系统上的真实文件。

你可以使用 `gnomevfs-cat` 来提取文件，例如：

```
[freddie@bastille] gnomevfs-file:file-apps
2.4.1-1386.rpm@HEADER
Name: gnome-apps
Relocations: (not relocatable)
Version: 2.4.1
Vendor: Red Hat, Inc.
Release: 1
Build Date: Fri Oct 3 10:29:07 2003
Install (not installed)
Build Host: daffy.redhat.com
Group: User Interface/Desktops
Source RPM: gnome-apps
2.4.1-src
Size: 1121002
License: GPL
Signature: DSA/SHA1, Tue Oct 28 19:10:23, 2006 b42b699d4a2f6d2 - Red Hat, Inc.
<Package>bugzilla.redhat.com</package>
URL: http://www.gnome.org/
Summary: Small applications for the gnome panel.
Description:
GNOME (Network Object Model Environment) 是一组用户friendly应用程序和桌面工具。
这前 28 个文件是虚拟的，其余的是如果你安装了此包，则安装在你系统上的真实文件。

你可以使用 `gnomevfs-cat` 来提取文件，例如：

```

[freddie@bastille] gnomevfs-file:file-apps

2.4.1-1386.rpm@HEADER

Name: gnome-apps

Relocations: (not relocatable)

Version: 2.4.1

Vendor: Red Hat, Inc.

Release: 1

Build Date: Fri Oct 3 10:29:07 2003

Install (not installed)

Build Host: daffy.redhat.com
