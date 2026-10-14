
您的第一个任务是确定 `ifhp` 是否满足您的需求。如果您有 `postscript`、`HP` 激光喷或 `PCL` 兼容打印机，您可能想尝试一下。

`ifhp` 适用于大量打印机，其默认配置 `/etc/ifhp.conf` 包含许多（不是所有）打印机的默认设置。

参考 `ifhp` HTML 文档的第 2.2 节“配置 IFHP 和型号信息”，该文档位于：`file:/usr/share/doc/packages/ifhp-3.3.10/IFHP-HOWTO-2.html`

据报道，如果您的打印机支持此项功能，`ifhp` 可以检测到您的打印机型号——我的 `HP2000C` 系列喷墨打印机不支持此功能，因此我必须告诉它应该使用哪种型号。查看 `/etc/ifhp.conf` 并查找以“Printer Specific Configurations”（打印机特定配置）开头的部分。你会发现以 `[printer model> .... <printer model>]` 开头的条目，其中 `<printer model>` 是打印机型号名称，例如 `hpdj1600c`。尝试将这些条目中的一个匹配到打印机。

我发现任何 `hpdj` 型号都可以与我的打印机配合，因为它们都使用相似的 `PCL` 语言版本。您拥有这些信息，必须在使用 `ifhp` 打印过滤器时将其传递。。与您的 `printcap` 文件中类似的一行。（完整示例请参考列表 16-1。）

```
:ifhp-model=hpdj1600c, status@
```

除了设置型号外，我禁用了状态 `status` 功能，因为我的打印机不支持此功能。在 `ifhp.conf` 文件中，通过附加 '@' 字符来禁用功能。有关可用选项的更多信息，请参考 `IFHP` 文档 `/usr/share/doc/packages/ifhp-3.3.10`。当您完成编辑 `printcap` 文件后，重启 `LPD` 服务强制其重新读取 `printcap`。

```
/etc/rc.d/init.d/lpd stop
```

```
/etc/rc.d/init.d/lpd start
```

现在您已准备好测试您的新打印机设置了。首先尝试打印一个简单的文本文件。

```
lpr -HP2000C ~/.bashrc
```

在这里我选择打印一个 `UNIX` 文本文件。注意我使用 `-O` 选项指定打印机/队列名称。如果不指定，将使用默认打印机——由 `$PRINTER` 环境变量指定，如果未定义，则使用 `printcap` 文件中列出的第一个打印机。

您应该看到输出中有阶梯效应。这是 `ifhp` 输入过滤器的结果。如果文件没有打印，请确保您指定了正确的打印机设备（如 `/dev/lp0`），并且打印机已打开。接下来，检查打印队列以验证 `LPD` 确实接收并缓冲了您的任务。

```
lpq -HP20000C
```

如果您的作业没有打印，您可能会看到它仍在队列中。再等一秒看它是否打印。如果仍然不打印，说明存在两个问题之一——1) `LPD` 配置不当或 2) 您的输入过滤器未工作。经验表明，后者通常是罪祸首。尝试以下操作：

- 1. 编辑您的 `printcap` 并删除 `LPD` 条目。
- 2. 重启 `LPD` 服务
- 3. 尝试打印一个简单的文本文件。

这几乎等同于将文件“cat”到设备，`LPD` 管理将文件发送到打印机的行为。如果这有效，则确认您在 `IFHP` 上存在问题。阅读 `IFHP` 文档并确保您使用的是与您的打印机兼容的打印机型号。您可能会发现这需要您进行一些尝试错误。（对于我的 `hp200c`，在多次尝试后，我必须关闭状态——使用 `status@`。）您可能会发现以下内容对调试 `ifhp` 有用。

- 1. 创建包含一些 `ASCII` 文本的简单文本文件 `hi.txt`。
- 2. 切换 `ifhp` 所在的 `/usr/lib/filters`。尝试执行与 `LPD` 类似的命令：
  ```
  ./ifhp -Tconfig=/etc/ifhp.conf -Tmodel=dlj600c,status@ < hi.txt
  ```
  您应该能看到文件的文本。如果看到了，那么可能它正在工作——转到第 5 步。

3 如果第 2 步无效，编辑 `ifhp.conf` 并开启调试，找到文件开头名为 `DEBUG setup` 的部分。通过删除 '#' 字符取消注释 `#debug=5`。接下来指定一个文件将输出转储到，例如 `dev=/tmp/debug`。

4 重复第 2 步的命令。检查 `/tmp/debug`，如果没有发现任何令人大目的调试信息，继续执行第 5 步。否则重复第 3 步。

5 如果一切正常，将设备更改为 `/dev/<printer>`，其中 `<printer>` 是您的打印机设备——例如 `lp0`。

6 重复第 2 步的命令。如果读取器没有输出，尝试不同的打印机型号，并关闭某些功能，如状态和页码功能。

在您认为 `ifhp` 工作正常后，对 `/etc/printcap` 和 `/etc/ifhp.conf` 文件进行必要的更改。确保关闭、注释掉 `/etc/ifhp.conf` 中的 `debug=5` 条目和 `dev=` 条目。

# 第 16 章 打印机配置

每次更改 `printcap` 文件时，请记得重启 `LPD`。修改 `ifhp.conf` 时，你不需要重启 `LPD`。

## 配置 IFHP 处理不同文件类型

根据你的打印机能够打印的格式（如文本、`PCL` 和 `postscript`），你需要告诉 `ifhp` 如何处理这些文件格式，或者它是否需要处理这些格式。请记住，大多数 `Linux` 应用程序都打印 `postscript`，因此如果你的打印机不支持 `postscript`，你必须告诉它如何处理 `postscript`。

编辑 `/etc/ifhp.conf` 配置文件，并搜索以“Text and Incompatible file type conversion control”（文本和不兼容文件类型转换控制）开头的部分。

`ifhp` 有两种方法可以确定传入的文件类型：1) 使用内部检测程序，该程序仅限于检测 `pcl`、`pjl`、`text` 和 `postscript`；2) 使用 `Linux` 的 `file` 工具。

第一种方法最简单，但限于它能检测的文件类型。第二种方法依赖于外部的 `Linux` `file` 工具，该工具能够识别多种文件格式。尝试在命令行提示符下使用 `file` 工具。它接受一个参数——文件名。

```
> file ~/Fritz.jpg
```

`home/jduprey/Fritz.jpg: JPEG image data`

当 `ifhp` 使用 `file` 工具时，它会将 `file` 的输出转换为小写，并将所有空白替换为空格。

无论你选择哪种文件检测程序，下一步都很简单。定义一个 `file_output_match` 块，它由一个正则表达式组成，该正则应匹配文件检测程序的输出（`IFHP` 的内部程序或 `Linux` `file` 工具），随后是转换类型 `ps`、`pjl`、`pcl`、`unknown` 或 `raw`，最后是一个将文件类型转换为打印机特定格式的转换函数。以下是我用于基于 `PCL` 打印机的配置。

```
## 强制使用 file(i) 工具

default_language=text

forceconversion@

# UNIX  de file 工具的路径

file_util_path=/usr/bin/file -

## 模式与转换器

file_output_match = [

*postscript* raw /usr/bin/gs -sDEVICE=cdj550

sOutputFile-- -sPAPERSIZE=letter -q -

*pcl*]
```
