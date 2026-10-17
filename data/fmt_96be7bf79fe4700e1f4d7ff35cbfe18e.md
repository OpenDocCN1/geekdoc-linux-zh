
这些命令应将 DOSEMU 文件安装在 `/var/lib/dosemu` 目录下。你必须以 `root` 身份登录，并有至少 10m 的可用虚拟内存用于构建。

> 注意：你必须安装包 `d`，即程序开发包。你需要该包中的各种编译器和工具来构建 DOS 模拟器。

## 配置 DOSEMU

在构建模拟器之后，你必须配置系统。首先，创建一个可引导的 DOS 磁盘，并将以下 DOS 文件复制到磁盘：`command.com`、`fdisk.exe` 和 `sys.com`。

接下来，将 `dosemu` 子目录下的以下 DOSEMU 文件拷贝到软盘：`emfs.sys`、`ems.sys`、`cdrom.sys` 和 `exitemu.com`。你可以使用之前“在 Linux 下处理文件”中提到的 `m-` 命令将 Linux 分区的文件拷贝到软盘器。

![](img/c03a7fab2607b66f899c0357fa9e7e_154_0.png)

![](img/c03a7fab2607b66f899c0357fa9e7e_155_0.png)

如果你在寻找 Linux 文件上有困难，可以使用 `find` 命令来定位。例如，此命令：

```
find -name emufs.sys -print
```
