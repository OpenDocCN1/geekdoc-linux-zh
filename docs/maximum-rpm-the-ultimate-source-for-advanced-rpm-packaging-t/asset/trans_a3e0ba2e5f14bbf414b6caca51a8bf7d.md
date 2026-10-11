
# A.2.1.3.2. 存档区

此列表基于 RPM 2.3 版本。若要获取最新版本，请查看最新 RPM 源代码中的文件 lib/rpmlib.h。

头部分之后的部分是存档区。存档区包含构成软件包的实际文件。存档区使用 GNU zip 进行压缩。通过查看存档区的开头，我们可以验证这一点：

```
0000040: 0000 001f 8b08 0000 0000 0002 03ec fd7b ............  {
0000050: 7c13 d516 388e 4e92 691b 4220 010a 1428 ., .8.N.i.J...(
```

在此示例中，存档区从偏移量 043 开始。根据 /usr/lib/magic 文件的内容，gzip 压缩文件的前 2 个字节应为 1f8b，而这正是我们实际看到的。下一个字节（08）是 GNU zip 用于指示文件已通过 gzip 的 deflation 方法压缩的标志。第 8 个字节的值为 02，这意味着存档区是使用 gzip 的最大压缩设置进行压缩的。接下来的字节包含一个代码，指示存档区是在哪种操作系统下压缩的。此字节中的 03 表示压缩是在类 UNIX 操作系统下进行的。

RPM 包文件的剩余部分是压缩后的存档区。存档区解压后，它是一个带有 CRC 校验的 SVR4 格式普通 cpio 存档。

# A.3. 研究 RPM 文件的工具

在随 RPM 源代码分发的 tools 目录中，包含一些使用 RPM 库来提取包文件各个部分的小程序。这些工具通常由 RPM 开发人员用于调试目的，但也可用于更易于理解 RPM 包文件格式。以下是这些程序及其功能的列表：

- rpmlead—从包文件中提取引导部分（lead section）
- rpmsignature—从包文件中提取签名部分
- rpmheader—从包文件中提取头部
- rpmarchive—从包文件中提取存档区
- dump—以易读格式显示头部结构

前四个程序将 RPM 包文件作为输入。包文件可以从标准输入读取，也可以在命令行中包含文件名。在任何情况下，这些程序都写入标准输出。以下是使用 rpmlead 从包文件显示引导部分的方法：

```
$ rpmlead foo.rpm | od -x
0000000 abed dbee 0003 0000 0100 7072 2d6d 2e32
0000020 2e32 2d31 0331 0000 0000 0000 0000 0000
0000040 0000 0000 0000 0000 0000 0000 0000 0000
```

由于这些程序中的每一个也可以作为过滤器使用，因此以下命令与前面的命令等效：

```
# cat foo.rpm | rpmlead | od -x
0000000 abed dbee 0003 0000 0100 7072 2d6d 2e32
0000020 2e32 2d31 0331 0000 0000 0000 0000 0000
0000040 0000 0000 0000 0000 0000 0000 0000 0000
```

**dump** 程序与 **rpmsignature** 或 **rpmheader** 配合使用。它使解码头部结构变得轻而易举：

```
# rpmsignature foo.rpm | dump
Entry count: 3
Data count: 172

CT    TAG                         TYPE      OFSET   COUNT
Entry :   000  (1000)NAME            INT32_TYPE 0x00000000 00000001
          Data: 000 0x00d44c4f (281679)
Entry :   001  (1001)VERSION         BIN_TYPE    0x00000004 00000016
          Data: 000 b0 25 b0 97 15 97 01 32
          Data: 000 df 35 df 69 32 9c 53 75
Entry :   002  (1002)RELEASE         BIN_TYPE    0x00000014 00000152
          Data: 000 89 90 95 03 05 00 31 ed
          Data: 000 63 90 a5 52 08 f1 cb a2
          Data: 016 9b f9 01 01 43 7b 04 00
          Data: 024 9c 8e 0a 0a d4 37 90 36 4e
          Data: 032 df b0 9a 8a 22 b5 b0 b3
          Data: 040 dc 30 4c 6f 91 08 c1 50
          Data: 048 70 4e 2c 64 d8 8a 8f ca
          Data: 056 18 ab 5b 6f f0 41 66 c8
          Data: 064 d1 8a 01 c9 36 01 6e f0
          Data: 072 90 dd e9 56 31 42 61 b3
          Data: 080 b1 da 84 94 6b ef 9c 19
          Data: 088 45 74 c4 9f ee 17 35 01
          Data: 096 d1 05 fb 68 0c e6 71 5a
          Data: 104 60 f1 c6 90 27 9f 03 06
          Data: 112 28 ed 0b a0 08 55 9e 82
          Data: 120 2b 1c 2c de e8 e3 50 90
          Data: 128 62 60 0b 3c ba 04 69 a9
          Data: 136 25 73 1b bb 5b 65 ad e1
          Data: 144 b1 d2 c0 7f 8a fa 4a 9b
```

**dump** 程序的一个值得注意的方面是，它针对解码包文件的头部分进行了优化。当与 **rpmsignature** 一起使用时，它显示的是头中的标签名称，而不是签名标签名称。然而，数据在两种情况下都能正确显示。

# A.4. 使用 file(1) 命令识别 RPM 文件

如今，大多数类 UNIX 系统上的 magic 文件应包含识别 RPM 文件所需的信息。但如果您的系统不包含此信息，可以将以下信息添加到文件中：

```
#------------------------------------------------------------
#
# RPM: file(1) magic for Red Hat Packages
#
0       beshort   0xedab
>2      beshort   0xeedb          RPM
>>4     byte      x               v%d
>>6     beshort   0               bin
>>6     beshort   1               src
>>8     beshort   1               i386
>>8     beshort   2               Alpha
>>8     beshort   3               Sparc
>>8     beshort   4               MIPS
>>8     beshort   5               PowerPC
>>8     beshort   6               68000
>>8     beshort   7               SGI
>>10    string    x               %s
```

file 命令的输出简洁明了：

```
# file baz
baz: RPM v3 bin i386 vlock-1.0-2
```

在此情况下，名为 baz 的文件是一个版本 3 格式的 RPM 文件，其中包含 vlock 软件包 1.0 版本的第 2 次发布，该文件是为 Intel x86 架构构建的。

![](img/5ceb645f91e0f928013c644127692ba8_374_0.png)

# rpmrc 文件

**rpmrc** 文件用于控制 RPM 的操作。该文件中的条目几乎会影响 RPM 操作的方方面面。在这里，我们将更详细地描述 **rpmrc** 文件，以及用于显示 RPM 如何解释这些文件的命令。

## B.1. 使用 --showrc 选项

正如我们稍后会看到的，RPM 可以读取多个 **rpmrc** 文件，每个文件可以包含近 30 种不同类型的条目。这使得确定 RPM 实际使用的值变得困难。

幸运的是，有一个选项可以帮助理清这一切。--showrc 选项显示每个条目的值。输出分为两个部分：

- 架构和操作系统值
- **rpmrc** 值

架构和操作系统值定义了 RPM 运行的架构和操作系统。这些值定义了构建和安装软件包的环境。它们还定义了哪些架构和操作系统是兼容的。

**rpmrc** 值定义了 RPM 操作的许多方面。这些值的范围从 RPM 数据库的路径到列出为构建该软件包的人员姓名。

以下是 --showrc 输出的示例：

```
# rpm --showrc
ARCHITECTURE AND OS:
build arch        : i386
build os          : linux
install arch      : i486
install os        : linux
compatible arch list : i486 i386
compatible os list : linux
RPMRC VALUES:
builddir          : /usr/src/redhat/BUILD
buildroot         : (not set)
cpioin           : cpio
dbpath            : /var/lib/rpm
defaultdocdir     : /usr/doc
distribution      : (not set)
exclude docs       : (not set)
ftpport           : (not set)
ftpuser           : (not set)
messagelevel      : (not set)
netsharedpath     : (not set)
optflags          : -O2 -m486 -fno-strength-reduce
packager          : (not set)
pgp_name          : (not set)
```

