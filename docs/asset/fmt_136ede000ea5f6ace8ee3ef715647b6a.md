
如果时间戳服务的 CA 证书未安装在系统中，可以手动获取。在发出请求时（因为使用了 `-cert` 参数），TSA 证书应该作为时间戳的一部分返回。例如，从 FreeTSA 获取 CA 证书：

```bash
$ cacert http://freetsa.org/files/cacert.pem
```

假设 OpenSSL 可用 CA 和 TSA 证书，你可以如下所示验证时间戳：

```bash
$ openssl ts -verify -in hash.log.tsr -queryfile hash.log.tsr -CAfile cacert.pem
Verification: OK
```

自指定时间以来。如果预计永久使用特定的时间戳权威，你可以将 CA 证书添加到操作系统的受信任 CA 存储中。

`AFFlib` 还提供了使用 X.509 证书对获取的镜像进行签名和验证签名的功能。本节未讨论信任用于签名镜像和验证时间戳密钥所需的信任网（web-of-trust）或公钥基础设施（PKI）。示例假设这种信任已经建立。

## 在镜像格式之间转换

出于各种原因，在取证镜像格式之间进行转换是有益的。如果实验室有了新的软件或基础设施，而当前格式不受支持或效率较低，转换为另一种格式可能是一个选择。如果你正在将镜像传输给第三方，他们可能有偏好的镜像格式。如果你从第三方那里接收镜像，你可能想将其转换为你偏好的格式。本节提供了在命令行上进行格式间转换的示例。展示了从几种源格式的转换，包括 EnCase、FTK、`AFF` 和 `raw`。此外，示例还演示了将各种格式转换为 SquashFS 容器。

当你在镜像格式之间进行转换时，最好使用管道和重定向。避免使用临时文件的工具。在转换过程中，可能会的两个副本可能会同时存在（其中一个可能是压缩的）。为转换过程做准备，请进行一些容量规划。

转换后，检查原始镜像和目的地的哈希值是否匹配。

### 从 Raw 镜像转换

将 `raw` 镜像转换为其他格式通常非常简单，因为可以使用标准的磁盘映像功能。使用 `raw` 镜像的文件而不是 `raw` 设备名称。

以下示例显示了将 `raw` 镜像文件转换为 EnCase 和 FTK 格式。第一个示例使用 `ewfacquire image.raw` 转换为 EnCase Expert witness 格式：

```
$ ewfacquire image.raw -t image -f encase7
ewfacquire 20160424
```

存储媒体信息：

- 类型：RAW 镜像
- 媒体大小：7.9 GB (7918845952 bytes)
- 每扇区字节数：512

所需的获取参数，请提供必要的输入

案件编号：42

描述：丢失的红色订书器案件

证据编号：1

检查员姓名：S. Holmes

备注：在现场发现了这个红色 U 盘

...

获取完成于：2016年5月14日 15:03:40

写入：7.3 GiB (7918864140 bytes)，耗时 54 秒，速度为 139 MiB/s (146645298 bytes/second)

数据计算了 5 个哈希：5dfe68597f8ad9f2060a453101f2c57

ewfacquire: SUCCESS

指定的源文件是 `raw` 镜像；`-t` 是 EnCase 字符的基础名称，指定了 EnCase 版本 7，当执行命令时，会询问一系列问题。由于 `raw` 文件没有案件元数据，你需要手动输入。

从 `raw` 镜像转换为 FTK SMART 类似：你指定 `raw` 镜像为源并手动添加案件元数据。使用 `fikimage`，你在命令行上指定元数据，如此示例所示：

```
$ ftkimager image.raw --s01 --case-number 1 --evidence-number 1 --description
"The case of the missing red stapler" --examiner "S. Holmes" --notes "This USB stick was found at the scene"
```

AccessData FTK Imager v3.1.1 CLI (Aug 24 2022)

Copyright 2006-2012 AccessData Corp., 384 South 400 West, London, IT 84042

保留所有权利。

创建镜像...

镜像创建完成。

`--s01` 标志指定将创建一个 SMART 压缩镜像。

文件名简单指定为 `image`，并将自动添加适当的文件扩展名。

将镜像转换为 SquashFS 取证容器如果使用 `sfsvimage` 命令也是一个简单的命令，如下：

```
$ sfsvimage -i image.raw image.sfs
Started: 2016-05-14T15:14:13
sfsvimage version: Sfsvimage Version 0.8
sfsvimage command: /usr/bin/sfvimage -i image.raw
Current working directory: /exam/exam/image
Forensic evidence source: if=/image.raw
Destination squashfs container: image.sfs
Image filename inside: image.raw
Aquisition command: sudo dd if=/exam/image.raw log=errorlog.txt hash=log.txt
hash-md5 2>/dev/null | -s 7918845952
```

7.38GB 0:00:22 [ 39MiB/s ] [==================================>] 100%

Completed: 2016-05-14T15:14:37

在这里，`raw` 镜像文件与目标 SquashFS 容器文件名一起指定。`sfsimage` 脚本构建了所需的 SquashFS 伪设备并为普通文本文件了日志和哈希信息。你可以手动向证据容器添加额外的元数据（使用 `sfsimage -a`）。

你无法直接使用典型工具访问压缩镜像，因为无法寻道其中的任何块。最好将此类文件转换为可搜索格式。在本示例中：

```
$ sfsvimage -i image.raw image.sfs
Started: 2016-05-14T15:14:13
sfsvimage version: Sfsvimage Version 0.8
sfsvimage command: /usr/bin/sfvimage -i image.raw
Current working directory: /exam/exam/image
Forensic evidence source: if=/image.raw
Destination squashfs container: image.sfs
Image filename inside: image.raw
Aquisition command: sudo dd if=/exam/image.raw log=errorlog.txt hash=log.txt
hash-md5 2>/dev/null | -s 7918845952
```

在这里，`raw` 镜像文件与目标 SquashFS 容器文件名一起指定。`sfsimage` 脚本构建了所需的 SquashFS 伪设备并为普通文本文件了日志和哈希信息。你可以手动向证据容器添加额外的元数据（使用 `sfsimage -a`）。

你无法直接使用典型工具访问压缩镜像，因为无法寻道其中的任何块。最好将此类文件转换为可搜索格式。

`image.E07` `image.E16` `image.E25` `image.E34` `image.E43` `image.E52`

`image.E08` `image.E17` `image.E26` `image.E35` `image.E44` `image.E53`

`image.E09` `image.E18` `image.E27` `image.E36` `image.E45` `image.E54`

开始之前，你需要一个 `mksquashfs` 伪定义来定义在 SquashFS 容器内部创建文件的命令。伪定义文件包含目标文件名、文件类型、权限、所有者以及要执行的命令。该命令的输出将成为定义的定义文件即 SquashFS 文件系统的内容。

在以下示例中，创建了一个名为 `pseudo_files.txt` 的文件，包含两个定义。第一个定义使用 `ewinfo` 提取 EnCase 元数据并将其放入 `image.txt` 中（如果不这样做，这些元数据将会丢失）。第二个定义将 `*.EO` 文件中的原始镜像导出到 `image.raw`。

```
# cat pseudo_files.txt
image.txt f 44 root ewinfo image.E01
image.raw f 44 root ewfexport -u -t - image.E01
```

`ewfexport` 标志 `-u` 允许转换无人值执行（否则它会向用户提示问题）。`-t` 标志指定目标，在本示例中目标是 `stdout` 或横杠 `-`。

使用该文件，你可以创建一个包含生成文件的压缩文件系统：

```
# mksquashfs pseudo_files.txt image.sfs -pf pseudo_files.txt
Parallel msquashfs: Using 12 processors
Creating 4.0 filesystem on image.sfs, block size 131072.
ewfexport 20160424
```

导出开始于：2016年5月12日 19:09:42

这可能需要一些时间。

...

导出完成于：2016年5月12日 19:28:56

写入 113 GiB (121332826112 bytes) 耗时 19 分 14 秒，速度为 100 MiB/s (105141097 bytes/second)

数据的 MDS 哈希：

0832e2310da559a2b359d48dbc451591

ewfexport: SUCCESS

...

文件系统大小 62068754.40 Kbytes (60614.02 MBytes)

52.38% 的未压缩文件系统大小 (118492706 Kbytes)

生成的生成的 SquashFS 文件系统 `image.sfs` 包含三个文件：原始镜像 `image.raw`、包含元数据的 `image.txt` 以及包含执行命令的 `pseudo_files.txt` 文件。

`mksquashfs` 手页提供了关于创建 SquashFS 文件系统的更多标志和选项。

你可以使用 `unsquashfs` 命令查看 SquashFS 文件的内容：

```
# mksquashfs -lls image.sfs
...
-R--I--R-- root/root      121332826112 2016-05-12 19:09 squashfs-root/image.raw
-R--I--R-- root/root      770 2016-05-12 19:09 squashfs-root/image.txt
-rw-w---- root/root      98 2016-05-12 16:58 squashfs-root
pseudo_files.txt
```

最后一步是通过比较 MD5 哈希值来验证证据。`ewinfo` 命令提供了在 EnCase 获取期间计算的 MD5 哈希。可以使用 `md5sum` 对 SquashFS 容器内新转换的原始镜像计算第二个 MD5 哈希。要这样做，你需要首先挂载 SquashFS 文件系统。以下示例显示了这些步骤：

```
# ewinfo.e01
ewfinfo 20160424
```

哈希信息

MD5:

083e2131d0a59ae3b594d8bc4151

```
# mkdir image.sfs.d; mount image.sfs image.sfs.d
# md5sum image.sfs.d/image.raw
083e2131d0a59ae3b594d8bc4151 image.sfs.d/image.raw
```

结果显示两个 MD5 哈希匹配，成功保留了从 EnCase 到 SquashFS 容器内的原始镜像转换。第三个匹配的 MD5 哈希可以在转换过程中 `ewexport` 输出中看到。`ewexport` 工具也可以导出到其他 EnCase 格式。当挂载的 SquashFS 文件系统 `image.sfs.d` 不再需要时，可以使用 `unmount image.sfs.d`。`fsimage` 脚本为你管理这些步骤。

### 从 EnCase 转换文件

`ftkimager` 工具可以从 EnCase 转换为 FTK。在本示例中，一组 EnCase e01 文件被转换为相同名称但扩展名为 s01 的 FTK 压缩文件：

```
# ftkimager.e01 image --s01
AccessData FTK Imager v3.1.1 (Aug 24 2012)
Copyright 2006-2012 AccessData Corp., 384 South 400 West, London, UT 84042
All rights reserved.
```

创建镜像...

镜像创建完成。

哈希已检查并添加到新的 FTK 文件中。案件元数据没有添加到新转换的文件中，而是从原始格式提取并保存为扩展名为 `.txt` 的独立文件（`image.s01.txt`）。

### 从 FTK 转换

命令行工具 `ftkimager` 在 EnCase 和 FTK 格式之间转换，并允许你使用 `stdin` 和 `stdout` 进行转换。在本示例中，一组压缩 FTK s01 文件被添加到 EnCase 格式：

```
# ftkimager s01 image --e01
AccessData FTK Imager v3.1.1 (Aug 24 2012)
Copyright 2006-2012 AccessData Corp., 384 South 400 West, London, UT 84042
All rights reserved.
```

创建镜像...

镜像创建完成。

案件元数据没有传输到新格式，而是自动保存到独立文件（`image.e01.txt`）。`ftkimager` 可以将 s01 文件转换为 `stdout`，你可以将其重定向到原始镜像文件或将其管道到其他程序。在本示例中，一组 FTK 文件通过 `ftkimager` 输出管道到 `sfsimage` 转换为 SquashFS 取证容器：

```
# ftkimager s01 - | sfsimage -i image.sfs
Started: 2016-05-14T19:59:13
sfsimage version: Sfsimage 0.8
sfsimage command: /usr/bin/sfsimage -
Current working directory: /exam
Forensic evidence source:
Destination squashfs container: image.sfs
Image filename inside container: image.raw
Acquisition command: sudo dc33dd log=error.txt hash=hashlog.txt hash=md5
2>/dev/null | pv -s 0
AccessData FTK Imager v3.1.1 (Aug 24 2012)
Copyright 2006-2012 AccessData Corp., 384 South 400 West, London, UT 84042
All rights reserved.
```

```
14.5GB 0:01:37 [ 151MiB/s ]
Completed: 2016-05-14T20:00:51
```

# sfsisimage -a s01.txt image.sfs

附加到 image.sfs  4.0 文件系统，块大小 131072

当你从 FTK 格式转换为原始磁盘镜像时，案件元数据不会被传输。你需要手动保存案件元数据，它通常位于单独的文件中。你可以像上一个示例中使用 `sfsisimage -a` 命令所示将其添加到 SquashFS 容器中。

在执行任何类型的格式转换后，你都应该在目标格式上单独验证哈希值，以确保证据的完整性得到了保留。

### 从 AFF 格式转换

`affconvert` 工具可以将 AFF 镜像转换为原始镜像（从原始镜像转换为 AFF 格式）。`affconvert` 工具不使用 `stdin` 或 `stdout`；相反，它读取或创建独立的 `.aff` 文件。以下简单示例显示了将一个 AFF 文件转换为原始镜像：

```
$ affconvert -r image.aff
convert image.aff --> image.raw
Converting page 96 of 96
bytes converted: 162570240
Conversion finished.
```

将原始镜像转换为 AFF 格式，只需使用 `affconvert image.raw`，相应的 `.aff` 文件将被创建。要使用管道和重定向处理 AFF 文件，可以使用 `affcat` 工具。上一个示例也可以通过 `affcat` 重定向到文件（不带任何状态或完成信息），如下所示：

```
$ affcat image.aff > image.raw
```

将 AFF 镜像转换为 EnCase 或 FTK，`affcat` 工具可以通过 `stdout` 或 `stdin` 管道到相应的工具创建所需的镜像。例如，你可以从 AFF 转换为压缩 FTK 镜像：
