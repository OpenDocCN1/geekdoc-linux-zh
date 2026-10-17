
# 第 14 章

## 配置软件

在你下载并解压新软件后，你必须对其进行配置和微调以适应你的系统。通常情况下，你将进行的更改包括：

- 调整路径名称（例如，安装到 `/home/yourid/bin` 而不是 `/usr/local/bin`，因为你可能无法在后者安装软件）。
- 指定你正在运行的是哪种 Unix 系统。
- 插入你的电子邮件地址和类似的数据。
- 在两个或三个特定的系统设置中选择一个。每个系统应该选择哪一个，在你将使用的文件中会有明确的标记。

如果你正在安装一个将被编译的程序，你的步骤将与这些非常相似。如果你正在安装一个脚本，步骤可能会有所不同，但请继续阅读这些步骤，因为脚本和程序在修改内容的原则上是相同的。

你具体需要做哪些更改（在程序或脚本中）几乎总是记录在 `INSTALL` 文件中（或者如果软件没有附带 `INSTALL` 文件，则在 `README` 中——在 `Makefile` 中（针对程序）或你将运行的实际 `.pl` 或 `.sh` 文件中（针对脚本）。

**代码列表 14.2**。所以请务必阅读这些文件！本节的步骤假设你从下载的解压和解包文件的主目录开始。

```
jdoe /home/jdoe/src/yencode-0.46 $ README

这是 yencode，一个用于 Usenet "yEnc" 格式的编码器/解码包，根据 GNU 通用许可证许可。

### 特性

- 适用于所有 Unix 操作系统的可移植程序。

- 编码器可以输出任何大小的单部分或多部分编码归档。

- 智能解码器可以处理多个文件，包括乱序指定或文件名异常的文件。

- 易于使用的 Usenet 发布软件支持对单个文件或文件组进行单行发布，根据需要还可以创建 SFV/FRC 校验和文件。

- 可选扫描模式：在指定目录或递归地自动定位并解码单部分或多部分编码归档。

- 完全符合 yEnc 规范的所有版本（当前为 v1, v2, v3）。

- 正确实现了 CRC 值，包括多部分归档每个部分的 pcrc32，以及多部分归档最后一个部分的 crc32。

- 由 GNU gettext 提供全面的国际化（多语言）支持。

有关 yenc 的信息，请访问 http://www.yenc.org/。

无法访问很多系统类型。如果你在编译或安装此程序时遇到问题，请给我发邮件（或发送补丁！），我会尝试添加对你系统的支持。此版本已在 FreeBSD 和 Linux 上测试过。

国际化支持目前支持英语，因为我是一个无知的美国人。欢迎翻译。

此程序应被视为“alpha 质量”。它尚未在实际应用中经过广泛测试。请通过电子邮件向我的错误报告、评论和建议。将建议和错误报告发送到 <bboy@net>。
```

## 使用 `make install` 进行编译和安装

你的最后一步是将软件安装到 Unix 系统上。对于某些程序，你只需要将文件复制到你想要存放的目录即可：对于程序或脚本使用 `~/bin`，有时对于 Web 使用的脚本或程序使用 `cgi-bin`。然而，对于其他程序，你必须先进行编译再安装。

你可以使用 `make install` 来进行编译和安装，它会读取 `Makefile`（查看如何设置所有内容）并为你完成编译和安装工作（代码列表 14.4）。再次提醒，在开始之前务必仔细阅读指令，并准确完成。

```
jdoe /home/doe/src/yencode-0.46 $ make
cd . \
& CONFIG_FILES=CONFIG_HEADERS=config.h \
/bin/sh ./config.status
config.status: creating config.h
config.status: config.h is unchanged
make all -recursive
make[1]: Entering directory `/home/doe/src/yencode-0.46'
Making all in intl
make[2]: Entering directory `/home/doe/src/yencode-0.46/intl`
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory `/home/doe/src/yencode-0.46/intl`
Making in po
make[2]: Entering directory `/home/doe/src/yencode-0.46/po`
```

```
gcc -DLOCALED_IR="/home/doe/src/local" -DSYSYYPE="i686-pc-linux-gnu" -I. -I.,\n-I. ./lib -Iintl \-Wall -Wno-unused -gO2 -c -f ydecode.c ilo echo ''' /../ydecode.c
gcc -Wall -Wno-unused -gO2 -o ydecode.o crc file.o o ../libmisc
make[3]: Leaving directory `/home/doe/src/yencode-0.46/src`
make[2]: Leaving directory `/home/doe/src/yencode-0.46/src`
make[2]: Entering directory `/home/doe/src/yencode-0.46`
make[2]: Leaving directory `/home/doe/src/yencode-0.46`
make[1]: Leaving directory `/home/doe/src/yencode-0.46`
```

代码列表 14.4 向你的屏幕输出了大量的垃圾（但希望没有错误信息）。

使用 `make install` 进行编译和安装：

1. `make`

首先，在 shell 提示符下（在包含程序设置文件的主目录中）输入 `make`，以设置你在上一一节中指定的所有变量。代码列表 14.4 显示了 `make` 在屏幕上显示的内容。

如果你看到错误信息，且没有伴随“将继续使用其他东西”之类的令人安心的消息，你可能需要返回编辑 `Makefile`。当你成功编译且没有出现糟糕的错误信息时，就可以进入第 2 步。
