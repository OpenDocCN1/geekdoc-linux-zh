

## IPython 也自带了基于 Qt 的控制台

```
Python.framework/Versions/2.7/lib/python2.7/posixpath.py
Docstring:
Common operations on POSIX pathnames.
```

```
%pdef %pdoc %pfile %pinfo %pinfo2 %popd %pprint %precision %profile %prun %psource %pushd %pwd %pycat %pylab %quickref %recall %rehashx %reload_ext %rep %rerun %reset %reset_selective %run %save %sc %sx %tb %time %timeit %unalias %unload_ext %who %who_ls %whos %xdel %xmode
```

不要直接导入此模块，导入 os 并将此模块引用为 os.path。 在 POSIX 系统上，'os.path' 是此模块的别名；在其他系统上（例如 Mac、Windows），os.path 以特定于该平台的方式提供相同的操作，并是另一个模块的别名（例如 macpath、ntpath）。

其中一些在非 POSIX 系统上也可能有用，例如用于操作 URL 的路径名组件。

你也可以使用双问号（??）来查看相关对象的源代码。

Magic functions: IPython 带有一些预定义的 'magic functions'，你可以用命令行风格的语法调用它们。 IPython 'magic' 命令通常以 % 为前缀，但如果标志 %automagic 被设置为开启，则可以不带前面的 % 调用 magic 命令。

要查看可用 magic functions 的列表，可以使用 'magic function %lsmagic'。 Magic functions 包括处理代码的函数，如 %run、%edit、%macro、%recall 等；影响 shell 的函数，如 %colors、%xmode、%autoindent 等；以及其他函数，如 %reset、%timeit、%paste 等。 IPython 大多数酷炫功能都是由 magic functions 驱动的。

### Example:

```
In [45]: %lsmagic
Available magic functions:
%alias %autocall %autoindent %automagic %bookmark %cd %colors %cpaste %debug %dhist %dirs %doc %docstring %edit %env %gui %hist %history %install_default_config %install_profiles %load_ext %loadpy %logoff %logon %logstart %logstate %logstop %lsmagic %macro %magic %page %paste %pastebin %pdb
```

Automatic is OFF, % prefix IS needed for magic functions

要查看任何 Magic Function 的帮助，调用 '%somemagic?' 以读取其 docstring。

### Python script execution and runtime code editing: 你可以使用 %run 运行任何 Python 脚本。 你也可以使用 -d 用 pdb 调试器控制运行 Python 脚本，或使用 -p 用 pdn 分析器运行。 你也可以使用 %edit 命令编辑 Python 脚本。 %edit 将在 $EDITOR 环境变量定义的编辑器中打开给定的 Python 脚本。

### Shell command support: 如果你只是想运行一个 shell 命令，你可以非常轻松地通过在命令前加上 ! 来实现。

### Example:

```
In [5]: !ps
  PID TTY          TIME CMD
 4508 ttys000   0:00.07 -bash
 84275 ttys001   0:00.03 -bash
 17958 ttys002   0:00.18 -bash
```

```
In [8]: !clang prog.c -o prog
prog.c:2:1: warning: type specifier missing, defaults to 'int' [-Wimplicit-int]
main()
...
1 warning generated.
```

Qt console : IPython 也自带了基于 Qt 的控制台。 这提供了一些仅在 GUI 中可用的功能，例如内联图形、多行编辑带语法高亮，以及图形化调用提示。

你可以通过以下方式启动 Qt 控制台：
$ ipython qtconsole

如果出现与缺少模块相关的错误，请确保已安装依赖包，例如 PyQt、pygments、pexpect 和 ZeroMQ。

![](img/3b256f430f51c98f1315671f6e4eec19_96_0.png)

## 具有 GUI 功能的 IPython Qt 控制台

> 正如你所见，将 Python 定制以满足所有 shell 环境需求是很容易的。 Python 模块如 os、subprocess 和 shutil 都可供你使用，用 Python 做几乎你需要的一切。 Python 将整个体验变成了一个更完整的套件。 你可以做标准 Python shell 的所有事情，并且拥有更方便的功能。 IPython 的 magic functions 确实提供了神奇的 Python shell 体验。 所以下次你打开一个 Bash 会话时，再想一想：为什么要满足于黄金，当铂金近在咫尺？

