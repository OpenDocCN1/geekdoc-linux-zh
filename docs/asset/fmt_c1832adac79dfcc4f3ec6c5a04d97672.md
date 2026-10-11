
```
root# rkhunter-check
[ Rootkit Hunter version 1.4.6 ]
正在检查系统命令
...
正在检查文件属性
正在检查前提条件 [ OK ]
/usr/sbin/adduser [ OK ]
/usr/sbin/chroot [ OK ]
...
正在检查已知的 rootkit 文件和目录
55808 Trojan - Variant A [ Not found ]
ADM Worm [ Not found ]
AjaRootkit [ Not found ]
正在检查系统配置文件
正在检查 SSH 配置 [ Found ]
检查是否允许 SSH root 访问 [ Warning ]
检查是否允许 SSH 协议 v1 [ Not allowed ]
系统检查摘要：
文件属性检查：已检查文件: 151, 可疑文件: 1
rootkit 检查：已检查 rootkit: 475, 可能的 rootkit: 0
...
所有结果已写入日志文件：/var/log/rkhunter.log
```

## `rm` 命令

```
rm [options] files
```

`rm` 删除指定的文件。除非使用 `-r` 选项，否则不会删除目录。`rmdir` 命令用于删除单个目录。如果需要删除带有特殊字符的文件，必须将文件名用单引号括起来。这里列出了 `rm` 最重要的选项：

- `-f`

不进行进一步询问直接删除（包括目录）。

注意！

- `-i` 或 `--interactive` 或 `-v` 或 `--verbose`

在删除每个单独文件之前显示确认提示。

- `-r` 或 `-R` 或 `--recursive`

递归删除所有子目录中的文件（小心！）。如果删除了子目录的所有内容，该子目录本身也会被消除。

### 示例

以下命令删除当前目录下的所有备份文件（以 `~` 字符结尾的文件）：

```
user rm \*char126
```

`rm` 删除备份文件或目录。如果备份是一个目录，则其中包含的所有子目录和文件也将被删除！

```
user$ rm -r backup
```

`rm` 删除所有以哈希字符 (`#`) 开头的文件。使用单引号是为了防止 shell 将 `#` 解释为注释。

```
user$ rm '#\*'
```

## `rpicam-still` [options]

Raspberry Pi OS 上的 `rpicam-still` 命令可以使用连接到树莓派的相机拍照。

- `-camera 0|1`

选择摄像头。只有在同时连接两个摄像头时才需要指定此选项。

- `-e jpg|bmp|gif|png`

指定所需的图像格式（默认是 jpg）。

- `--ev n`

设置曝光补偿。使用 `--ev 0.5` 结果将变亮半档，使用 `--ev -0.5` 则变暗。

- `--height n`

指定图像高度（默认是相机的最大分辨率）。

- `-n`

录制时不显示预览窗口。

- `-o file`

指定图像文件名。

- `-q n`

指示 JPEG 图像质量（0 为最小，100 为最大）。

- `--rotation n`

指定图像的旋转角度。仅允许 0 和 180。

- `-t n`

指定创建照片之前的时间间隔（毫秒）（默认为 5000 毫秒，即 5 秒）。要尽快拍照，必须输入 `-t 1`。

- `--timestep n`

指定拍摄额外照片的毫秒数。在这种情况下，`-t` 控制整个命令的运行时间（例如 `-t 60000` 意味着一分钟）。

- `--width n`

指定图像宽度（默认是相机的最大分辨率）。

### 示例

以下命令创建一个分辨率为 800 × 600 的照片：

```
user$ rpicam-still --width 800 --height 600 -o photo.jpg
```

第二个示例创建一个 10 秒的延时摄影：

```
user$ rpicam-still -t 10000 --timestep 1000 -o timelapse.jpg
```

### 变体

`rpicam-still` 命令还支持其他选项。例如，你可以使用 `--rotation` 选项来旋转图像：

```
user$ rpicam-still --rotation 180 -o rotated.jpg
```

## `rpcinfo` [options]

`rpcinfo` 运行远程过程调用 (RPC) 并返回 RPC 服务器返回的结果。`rpcinfo` 主要用于检查 NFS 服务器配置等。

- `-p [hostname]`

确定本地计算机或外部计算机上所有活跃的 NFS 和 RPC 服务列表。

## `rpm` options [filename/package name]

`rpm` 用于安装、更新或删除 RPM 包，或显示有关这些包的信息。`rpm` 适用于所有基于 RPM 软件包的发行版，例如 Fedora、Red Hat 和 SUSE。

- `-e` 或 `--erase`

删除已有的软件包。如果你还使用了 `--nodepeps` 选项，即使有其他软件包依赖于该包，该包也会被删除。

- `-i` 或 `--install`

安装指定的软件包文件。可以使用额外的 `--root` 目录选项更改安装位置。如果指定的包是源包，则程序代码和配置文件将安装在 `/usr/src` 中。在这种情况下，可以通过更改 `/etc/rpmrc` 来设置安装位置。

配合额外的 `--test` 选项，`rpm` 不会进行任何更改，而仅输出实际安装期间会发生的情况。

`rpm` 尝试自动检查签名包的完整性。但是，必须有可用的签名公钥才能执行此操作（参见 `--import` 选项）。如果你让 `rpm` 忽略检查，必须使用 `--nosignature` 选项。

配合额外的 `--nodeps` 选项，即使 `rpm` 认为各种依赖关系未满足，你也可以安装软件包。（如果两个包相互依赖，则无需使用 `--nodeps`。你只需同时安装两个包即可！）

额外的 `--ignorearch` 选项允许在 `rpm` 识别出 CPU 架构不正确的情况下进行安装。这在 64 位发行版上安装 32 位软件包时有时是必要的。

`--force` 选项在任何情况下强制安装，即使 `rpm` 认为该包已经安装。

额外的 `--noscripts` 选项确保 `rpm` 不会自动运行安装程序。然而，你刚刚安装的程序可能无法正常工作。

- `--import`

安装指定的 GPG 密钥。`rpm` 可以使用此密钥来检查签名包的完整性。所需的密钥文件可以在所有提供签名 RPM 包的网站上找到。

- `-q` 或 `--query`

提供有关已安装软件包或包文件内容的信息。在简单形式下，`rpm -q package name` 会输出精确的包名，包括指定包的版本号。

你可以使用 `rpm -qf file` 来确定特定文件属于系统中的哪个包。这对于配置文件特别有用。例如，`rpm -qf /sbin/hwclock` 返回包名：`util-linux-n`。

`rpm -qp package.rpm` 提供尚未安装的包的信息。在这种情况下，必须使用 `*.rpm` 文件的文件名作为参数。

`rpm -q --whatprovides` 或 `rpm -q --requires` 属性搜索会查找所有提供或需要指定依赖属性的已安装包。这两个选项不适用于搜索尚未安装的包！

`rpm -q --provides package` 或 `rpm -q --requires` 创建指定包提供或需要的所有属性的列表。这些选项也可以用于尚未安装的包文件（额外的 `-p` 选项）。

对于所有返回包作为结果的查询变体，你可以使用额外选项来控制找到的包信息量：

- `-i` : 软件包的简短描述、压缩大小
- `-l` : 列出包中所有的文件
- `-lv` : 如上所述，但包含文件大小、访问权限等更多信息
- `-c` : 列出包的所有配置文件
- `-d` : 列出该包所有带有在线文档的文件
- `--scripts` : 列出所有安装程序

如果你只需要所有已安装软件包的未排序列表，应该运行不带任何额外参数的 `rpm -qa`。`rpm -qa --last` 按安装日期对所有包排序（最近安装的包在前）。

- `-U --upgrade`

更新已有的软件包。系统将从上一个包修改的配置文件创建备份文件；旧包的所有其他文件将被新版本替换或删除。配合额外的 `--oldpackage` 选项，你可以用旧包替换较新的包。你也可以使用 `--nodeps` 确保 `rpm` 在升级时忽略包依赖关系。

- `-V` 或 `--verify`

检查包中的任何文件自安装以来是否发生了变化。命令返回所有更改文件的列表。文档文件不进行检查。

### 示例

以下命令安装指定的软件包：

```
root# rpm -i abc-2.0.7-1.x86_64.rpm
```

第二个 `rpm` 示例提供了所有已安装包的列表，其中包按安装日期排序（最近安装的包位于列表顶部）：

```
root# rpm -qa --last
```

`rpm -q --provides` 告诉你之前安装的哪个包提供了 `mysql.so` 属性：

```
root# rpm -q --provides mysql.so php-mysql
```
