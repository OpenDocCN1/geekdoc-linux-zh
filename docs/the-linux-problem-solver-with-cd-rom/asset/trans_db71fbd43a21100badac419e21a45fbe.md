

Automounter 监视一个目录，并在该目录上挂载文件系统之前冻结对该目录的访问尝试。一旦文件系统被挂载，访问即可照常继续。

由于 Automounter 仅在需要时才挂载文件系统，因此在网络上共享数据的机器可以同时关闭，也可以随意启动。只要启动过程中不需要查看任何 NFS 挂载的文件系统，该机器的启动速度就与独立机器一样快。

> NOTE
> 即使是 Automounter 也无法防止文件服务器崩溃造成的延迟。如果服务器 X 宕机，而你尝试查看 X 上的 /foo/bar，Automounter 将冻结你的访问，并在尝试挂载时很可能会超时并给出 I/O 错误。然而，这不会影响当前正在运行的进程；只要它们不尝试访问不可用的文件系统，它们应该能正常继续。

目前有两种常用的自动挂载守护进程：原生的 Linux automount，以及可在多个平台上运行的 amd。我们将重点关注 automount，因为它相当小巧且简单易用。

## automount

automount 以一个（最好是空的）目录作为其基目录，并将远程目录附加到该目录上。（最常见的例子是 /home。用户的家目录通常是 /home/user，因为用户通常希望其家目录在整个网络中位于同一位置。）

## The Automounter Map File

要配置 Automounter，请使用一个映射（文件）来确定 automount 将处理哪些目录以及在请求时从何处获取它们。将映射放置在网络上的某个位置，并使用 NIS、NIS+ 或任意程序执行使其可用，或简单地作为纯文本文件。无论你选择哪种方法，访问映射的格式或多或少是相同的。下面是一个 /home 的示例映射：

```
sue    mikado.example.com:/u25/sue
bob    atlantic.example.com:/u1/bob
```

假设你将映射放在名为 /etc/auto.home 的文件中。要在其上启动 Automounter，请使用以下命令：

```
# automount /home file /etc/auto.home
```

现在输入 cd /home/bob 即可进入 bob 的家目录。

## NOTE

要使 automount 正常工作，你必须将 autofs 文件系统直接或作为模块配置到内核中。相比之下，amd 并不特别需要 autofs 文件系统，但最好使用 autofs 以避免出现像 /a/mikado.example.com/u25/sue 这样奇怪的路径名——如果它们存在，你的用户会发现它们并向你询问，而你不想费心解释。总之，不要将目录挂载在其给定名称下，而应挂载在系统的另一部分，并从“正确”的位置放置符号链接到目录实际所在的位置。

automount 映射格式（如上例所示）与 Sun Microsystems 的 Automounter 兼容，可与 Sun 网络良好集成。除了文件格式外，Linux 还可以共享 Sun 的 /etc/auto.master，其中包含所有自动挂载点（如上文引用的 /home）以及映射位置。

## autofs

Linux 提供了一个名为 autofs 的脚本，应从 rc*.d 目录之一运行。autofs start 读取 /etc/auto.master 并为每个条目启动一个 automount 进程。以下是 auto.master 的示例：

```
/home      auto.home          -rw,intr,noquota
/scratch   /etc/auto.scratch
```

第一个条目指示 automount 在 NIS 映射 auto.home 中查找 /home 数据，而第二个条目以正斜杠（/）开头，因此 automount 会查询文件 /etc/auto.scratch。换句话说，在此示例中运行 autofs start 等同于运行以下命令：

```
# automount /home nis auto.home
# automount /scratch file /etc/auto.scratch
```

挂载选项放置在映射中的可选中间字段中。让我们修改上面的 /home 映射：

```
sue      -r                mikado.example.com:/u25/sue
bob      -nolock            atlantic.example.com:/u1/bob
cdrom    -ro,fstype=iso9660  /dev/hdb
```

此代码表示将 /home/sue 设置为只读访问，并且不要锁定来自 atlantic.example.com 的挂载（ presumably 因为该服务器上的锁定效果不佳）。最后一个条目根本不是 NFS 文件系统；它在此提供是为了展示如何使用 Automounter 来处理可移动介质。

