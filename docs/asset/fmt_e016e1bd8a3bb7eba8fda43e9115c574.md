
此示例显示你的计算机上有四个可启动分区，称为 `linux` 和 `dos`。前三个指的是 Linux 分区。第四个指的是 DOS 分区。如果你在几秒后没有输入任何内容，将加载第一个可启动分区。或者你也可以输入其他分区的名字来改为启动该分区。

以下是不同启动镜像用途的说明：

- `linux-ent` — 这是一个适用于企业计算的可启动镜像。该镜像默认开启。
- `linux-dos` — 这是一个可用于多处理器（SMP）计算机的可启动镜像。
- `linux-up` — 这是一个用于标准安装的可启动镜像。

如果你有多个启动镜像，按下 `Shift` 键，`LILO` 将询问你想要启动哪个镜像。可用的启动镜像和其他选项在 `/etc/lilo.conf` 文件中定义。

## 设置 `/etc/lilo.conf` 文件

`/etc/lilo.conf` 文件是 `LILO` 获取查找和启动可启动分区及镜像所需信息。通过向 `/etc/lilo.conf` 文件添加选项，你可以更改启动过程的行为。以下是 `/etc/lilo.conf` 文件部分内容的示例：

```bash
boot=/dev/hda

map=/boot/map

install=/boot/boot.b

prompt

timeout=50

message=/boot/message

linear

default=linux-ent

image=/boot/vmlinuz-2.2.16-21enterprise

label=linux-ent

root=/dev/hda6

read-only

other=/dev/hda

label=dos
```

`boot` 行表示可启动分区位于由 `/dev/hda` 代表的硬盘上（第一个 IDE 硬盘）。`map` 行表示映射文件的位置（默认为 `/boot/map`）。映射文件包含引导内核的名称和位置。`install` 行表示 `/boot/boot.b` 文件被用作新的引导扇。开启 `prompt` 后，当系统启动且没有按下任何键时，将出现启动提示符。

`timeout` 值（在此例中为 50 分之一，即 5 秒）定义了在启动默认镜像之前等待键盘的时间。`message` 行让 `LILO` 在启动时显示 `/boot/message` 文件的内容（其中包含图形化的 Red Hat 屏幕）。

# 第一部分 + Red Hat Linux 入门

## 第二章 + 安装 Red Hat Linux

- 1. 从 `/boot/src/i386/zImage-2.5.3` 复制镜像到 `/boot/zImage-2.5.3`。
- 2. 在 `lilo.conf` 中添加以下行：

```bash
image=/boot/zImage-2.5.3

label=new
```
- 3. 输入 `lilo -t` 命令以测试更改无误。
- 4. 输入不带选项的 `lilo` 命令应用更改。

在 `LILO` 提示符的菜单中，从图形界面选择 `new` 或输入 `new` 并按 Enter。如果五秒太快，请增加 `timeout` 值，例如 `100`。

在 `/etc/lilo.conf` 中使用的选项分为全局选项、单镜像选项和内核选项。`LILO` 有大量的文档可用。有关此处描述的任何选项或其他选项，你可以查看 `lilo.conf` 手册（输入 `man lilo.conf`）或 `/usr/doc/lilo/*` 中的任何文档。

是一些可以添加到 `/etc/lilo.conf` 的全局选项示例。全局选项适用于整个 `LILO`，而不是特定的镜像。

你可以使用 `default=label` （将 `label` 替换为镜像名称）来指定默认启动镜像。如果排除该选项，则 `/etc/lilo.conf` 文件中列出的第一个镜像作为默认。例如，要默认启动标记为 `new` 的镜像，在 `lilo.conf` 中添加以下行：

```bash
default=new
```

如果你想让 `LILO` 在启动默认镜像之前等待更长时间，将延迟从 5 秒更改为更大的值。这提供了更多时间启动不同的镜像。要将值从 5 秒（50）更改为 15 秒（150），添加以下行：

```bash
delay=150
```

你可以通过将该消息添加到文件中并更改 `message` 行来更改 `LILO` 提示符出现的消息。例如，你可以创建一个 `/boot/boot.message` 文件并在文件中添加以下单词：Choose linux, new, or dos。为了让该消息在启动提示符之前出现，向 `/etc/lilo.conf` 添加以下行：

```bash
message=/boot/boot.message
```
