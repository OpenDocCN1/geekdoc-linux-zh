
16 Installing...latest/contrib/cron/cron-3.0.1-5.tar.bz2

17 Installing...latest/crypt/crypt-1.0-1.tar.gz

18 Installing...latestlatest/ctags/ctags-5.0.1-tar.gz

19 Installing...latest/contrib/cvs/cvs-11.1.0.tar.gz

20 Installing...latest/cygrunsrv/cygrunsrv-0.94-2.2.tar.bz2

21 Installing previous version...latest/cygwin/cygwin-1.3.3-2.tar.bz2

22

23

24

25 mbox note: Installation Complete

26 2001/09/27 12:18:34 Ending cygwin install

```
**代码列表 10.1** Cygwin 安装示例日志内容。
```

## 10.2.1.2 升级 Cygwin 工具

Cygwin 升级过程详见附录 C，以防你需要最新版本 Cygwin 工具提供的错误修复或功能增强。

注意：此时不要在你的开发平台上运行 Cygwin 工具的升级程序。如果你这样做了，你的平台所拥有的 Cygwin 工具将与书中测试的工具不同。本节供你以后在需要（或想要）升级 Cygwin 工具时参考。

## 10.2.2 安装特定平台的交叉开发工具

接下来，我们将安装允许我们为特定的处理器（在本例中为 Intel x86）构建 eCos 及其应用程序的工具。交叉开发工具被用于为我们的特定平台（在本例中为 Intel x86）构建 eCos 库。正如我们在第 12 节中看到的，在构建构建应用程序时，我们也会使用这些相同的工具。

我们不需要经历配置和构建 i386 GNU 交叉开发工具的步骤，CD-ROM 上已提供了预编译版本。这消除了生成错误的 GNU 工具的可能性，考虑到需要输入的命令字符串，这种错误非常容易。这些工具将用于书中包含的示例。用于配置和构建 GNU 交叉开发工具的程序位于附录 D，“构建 GNU 交叉开发工具”中。

注意：CD-ROM 上还包含了 PowerPC GNU 交叉开发工具的预编译二进制版本，位于 `gnu\ppctools` 目录下的 `ppgcnutools.tar.bz2` 文件。这些工具将在第 13 节中使用。

特定平台的交叉开发工具可以分为三个组：

- GNU 二进制工具（通常称为 binutils）
- GNU C/C++ 编译器
- 带有 Insight 接口的 GNU Insight 调试器

安装 GNU 交叉开发工具所需的文件位于 CD-ROM 的 `gnu/i386gnutools.tar.bz2` 目录下。我们正在使用的 GNU 交叉开发工具版本见表 10.2。

### 表 10.2 GNU 交叉开发工具版本

| 工具 | 版本 |
|---|---|
| GNU 二进制工具 | 2.11.2 |
| GNU C/C++ 编译器 | 2.95.2 |
| 带有 Insight 接口的 GNU 调试器 | 5.1 |

尽管 GNU 二进制工具和 GNU C/C++ 编译的版本不是最新的，但已确认可以在书中用于 i386 PC 目标平台的开发环境中工作。如果你使用了不同的处理器架构，可能需要你升级到更新的版本。在升级之前，最好搜索 eCos 讨论列表，看看是否有描述新版本问题的帖子。

注意：我们在设置中使用的 GNU C/C++ 编译器版本 2.95.2 不支持附录 A“支持的处理器和评估平台”中所示的所有处理器。ARM Thumb、Hitachi SH、MN10300/AM33、NEC MIPS VR4300 和 NEC V850 处理器需要安装 GNU C/C++ 编译器的快照。可以在网上找到快照：http://gcc.gnu.org/pub/gcc/snapshots

GNU 交叉开发工具的版本以及每组工具的额外文档可以在它们各自的主页找到：

- GNU 二进制工具—http://sources.redhat.com/binutils
- GNU C/C++ 编译器—http://gcc.gnu.org
- 带有 Insight 接口的 GNU Insight 调试器—http://sources.redhat.com/insight

安装完成后，交叉开发工具位于 `D:\cywin\tools\H-i86-pc-cywin\bin` 子目录下。

GNU 二进制工具的邮件列表和发帖地址可以在网上找到：

- 讨论邮件列表—http://sources.redhat.com/ml/binutils
- 发帖至—binutils@sources.redhat.com

GNU C/C++ 编译器的邮件列表和发帖地址可以在网上找到：

- 讨论邮件列表—http://gcc.gnu.org/ml/gcc
- 发帖至—gcc@gcc.gnu.org
- 额外的讨论邮件列表—http://gcc.gnu.org/lists.html

GNU Insight 调试器 (GDB) 的讨论邮件列表和发帖地址可以在网上找到：

- Insight 调试器讨论邮件列表—http://sources.redhat.com/ml/insight
- 发帖至—insight@sources.redhat.com
- GDB 讨论邮件列表—http://sources.redhat.com/ml/gdb
- 发帖至—gdb@sources.redhat.com
- 额外的 GDB 讨论邮件列表—http://sources.redhat.com/gdb/mailing-lists

## 步骤 1

打开 bash 命令行。可以通过点击 Cygwin 原生工具安装时创建的桌面上的 Cygwin 快捷方式，或者通过菜单“开始 -> 程序 -> Cygnus Solutions -> Cygwin Bash Shell”来实现。

打开 shell 后，当前的工作目录是 `D:\cygwin\home\xxx`，其中 xxx 是你的用户名。我们通过在 bash 提示符输入以下命令切换到 Cygwin 根目录：

```
$ cd /
```

## 步骤 2

将 i386 GNU 交叉开发工具解压到我们的 Cygwin 目录结构中。命令是：

```
$ tar xjvf /cygdrive/e/gnu/i386gnutools.tar.bz2
```

> 注意：安装 Cygwin 时，CD-ROM 驱动器默认挂载为 `/cygdrive/e/`。在上述命令中应将 `/e/` 替换为 CD-ROM 的实际驱动器号。执行此命令后，我们在 `D:\cywin\tools\H-i86-pc-cywin\bin` 目录下。

## 步骤 3

我们需要挂载临时临时目录。命令是：

```
$ mount /cygdrive/e /tmp
```

## 步骤 4

接下来，我们为新的交叉开发工具设置路径。bash 命令是：

```
$ export PATH=/cygdrive/e/gnu/i386gnutools:$PATH
```

## 步骤 5

我们可以通过输入命令验证 i386 GNU 交叉开发工具是否正确安装：

```
$ i386-elf-gcc --version
```

如果一切正常，将输出以下信息：

```
2.95.2
```

如果信息错误，你需要验证工具是否正确解压到正确的目录。

## 配置 Windows Host

通过右键点击桌面上的“我的电脑”将交叉开发工具添加到 Windows 路径。显示属性对话框。选择“高级”选项卡。在“用户变量”下选择“Path”。点击“编辑”。

## 10.2.3 安装 eCos 开发工具包

eCos 开发工具包的安装包含多个阶段。此安装所需的文件位于 CD-ROM 的 `ecos` 目录下。我们将 eCos 开发工具包安装到 `D:\ecos` 目录。

`ecos-v2a-snap.tar.bz` 包含了 eCos 源码库版本 2 发布快照的源码文件。此外还包含了 eCos 配置工具。

在安装过程中，我们使用版本 2 配置工具和版本 1.3 配置工具。为了像我们在第 12 节中那样构建 RedBoot 和 eCos 镜像，我们将使用版本 2 配置工具。安装版本 1.3 配置工具用于内存布局 (MLT)，它在第 11 节中有描述。

此外还包含了包管理工具和 eCos 命令行配置工具。

Linux 安装文件位于 CD-ROM 的 `ecos\linux` 目录下。关于在 Linux 平台上安装 eCos 的更多信息可以在网上找到：http://sources.redhat.com/ecos/getstart.html

## 步骤 1

打开 bash shell 并输入命令切换到 D 盘：

```
$ cd d:
```

现在通过以下命令解压源码文件：

```
$ tar xvf /cddrive/e/ecos/ecos-v2a-snap.tar.bz2
```
