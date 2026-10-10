
第 12 行的 `LIBS` 包含了也传递给链接器的库选项。最后，变量 `LD` 在第 13 行为链接器定义。在这种情况下，链接器被构建在编译器可执行文件 `i386-elf-gcc` 中，因此我们使用 `XCC` 变量名来调用链接器。

`makefile` 的下一部分包含了构建规则或目标。目标是 `makefile` 尝试更新的目标。首先是第 16 行的 `all`。这是构建 ELF 文件的主目标。第 18 和第 19 行包含了构建 `basic1.o` 目标的信息。正如我们在第 19 行看到的，编译器使用变量 `XCC` 被调用，并传递了来自变量 `CFLAGS` 的后续标志。

第 21 和第 22 行是构建 `basic1` 目标的信息。`basic1` 目标是由链接器生成的 ELF 镜像，链接器选项位于第 22 行。

编译器和链接器的简要描述包含在 makefile 中。关于各种编译器标志的附加信息，在 bash 提示符下可以输入：

```
$ i386-elf-gcc --help
```

# 第 12 章 使用 eCos 示例

Makefile 还包含一个 `clean` 规则，它删除构建期间创建的文件，例如对象文件。这允许我们从上次构建后重新编译所有文件。要清理构建的文件，在 shell 提示符下使用命令 `make clean`。

在我们继续构建之前，让我们 eCos 库是如何链接到应用程序的。

- 1 START(vectors.o)
- 2 ENTRY(_start)
- 3 INPUT(.o)
- 4 GROUP(lib.a)

代码列表 12.4 目标

在代码列表 12.4 中，makefile 的第一部分设置了我们以后使用的变量，以便我们的 makefile 更于理解并允许重复使用变量而无需重新输入整个字符串。当我们想要使用一个变量时，我们使用 `$(VARIABLE_NAME)` 语法。无论字符串 `VARIABLE_NAME` 是否在变量使用处已声明或替换，在第 2 行，我们将变量 `PKG_INSTALL_DIR` 设置为我们在示例的上一个阶段构建的 eCos 库的位置。在第 5 行，我们将变量 `XCC` 设置为我们正在使用的编译器名称；在这种情况下，它是 `i386-elf-gcc`。

接下来，我们将构建标志赋予不同的变量。变量允许我们为了清晰以及在 makefile 的多处重复使用，用变量名代替长字符串。第一个变量是 `FLAGS`，如第 8 和第 9 行所示，包含了我们传递给编译器的标志。下一个变量是 `LDFLAGS`，如第 10 和第 11 行所示，包含了链接器的选项。`FLAGS` 和 `LDFLAGS` 两个变量在实际的 `makefile` 中位于同一行；但它们被分开了，以便显示所有选项。

第 12 行的 `LIBS` 包含了也传递给链接器的库选项。最后，变量 `LD` 在第 13 行为链接器定义。在这种情况下，链接器被构建在编译器可执行文件 `i386-elf-gcc` 中，因此我们使用 `XCC` 变量名来调用链接器。

## 第 4 步

接下来，我们可以构建镜像。在构建镜像之前，让我们花一点时间理解我们用于构建应用程序的 `makefile`。

```
## eCos库安装目录
PKG_INSTALL_DIR = /cd/d/workdir/ecos/install

## 这将编译器设置为 i386。
XCC = i386-elf-gcc

## 构建标志。
CFLAGS = -g -Wall -I$(PKG_INSTALL_DIR)/include -ffunction-sections -fdata-sections
LDFLAGS = -nostartfiles -L$(PKG_INSTALL_DIR)/lib -Wl,--gc-sections -Wl,--basic.map
LIBS = -ld
LD = $(XCC)

## 构建规则。
# Application
```

all: basic1

%.o: -c -o $@ $(CFLAGS) $(XCC)

basic1: %.o $(LD) $(LDFLAGS) -o $@ $(LIBS)

要将 ELF 镜像转换为 S-record 格式，我们使用 `objcopy` 工具。

```
$ i386-elf-objcopy -O srec basic1.o basic1
```

# 12.5 GNU size 的输出

| text data bss dec hex filename |
|---|---|---|---|---|
| 2 | 76900 | 544 | 16744 | 113188 | basic1.exe |

GNU size 的输出如代码列表 12.5 所示，makefilefile 的第一部分设置了我们以后使用的变量，以便我们的 makefile 更于理解并允许重复使用变量而无需重新输入整个字符串。当我们想要使用一个变量时，我们使用 `$(VARIABLE_NAME)` 语法。无论字符串 `VARIABLE_NAME` 是否在变量使用处已声明或替换，在第 2 行，我们将变量 `PKG_INSTALL_DIR` 设置为我们在示例的上一个阶段构建的 eCos 库的位置。在第 5 行，我们将变量 `XCC` 设置为我们正在使用的编译器名称；在这种情况下，它是 `i386-elf-gcc`。

接下来，我们将构建标志赋予不同的变量。变量允许我们为了清晰以及在 makefile 的多处重复使用，用变量名代替长字符串。第一个变量是 `FLAGS`，如第 8 和第 9 行所示，包含了我们传递给编译器的标志。下一个变量是 `LDFLAGS`，如第 10 和第 11 行所示，包含了链接器的选项。`FLAGS` 和 `LDFLAGS` 两个变量在实际的 `makefile` 中位于同一行；但它们被分开了，以便显示所有选项。

## 12.2 链接器被构建在编译器可执行文件 `i386-elf-gcc` 中，因此我们使用 `XCC` 变量名来调用链接器。

## 第 5 步

为了加载示例应用程序 RedBoot，我们输入命令：

```
RedBoot> load -v -m yMODEM
```

# 第 12 章 · 使用 eCos 的示例应用程序

![](img/e21b5ded81f449207668494619617bde_329_0.png)

图 12.9 HyperTerminal 发文件对话框。

![](img/e21b5ded81f449207668494619617bde_329_1.png)

图 12.10 HyperTerminal 传输状态对话框。

图 12.10 显示了应用程序到目标硬件的传输进度和相关信息，包括吞吐量和剩余时间。

完成后，对话框将关闭，RedBoot 会输出一条消息。RedBoot 输出消息的示例见代码列表 12.6。

- 1 入口点: 0x00108000, 地址范围: 0x00108000-0x0011aba0
- 2 xModem CRC 模式, 2(SOH)/215 (STX)/0(CAN) 数据包, 4 次重试

代码列表 12.6 我们的应用程序传输完成后 RedBoot 输出的消息。

在代码列表 12.6 的第 1 行，显示了我们刚刚加载的镜像内存信息。这些信息包含了入口点和应用程序使用的内存范围。第 2 行总结了传输统计数据。

# 第 6 步

现在我们准备好运行示例应用程序了。由于 RedBoot 知道我们应用程序的加载地址，因此我们不需要为 RedBoot 命令指定入口点。要运行我们的应用程序，在 RedBoot 提示符下输入以下命令：

```
RedBoot> go
```
