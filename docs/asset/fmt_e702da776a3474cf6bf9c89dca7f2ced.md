
checking for C compiler default output name... a.out

checking whether the C compiler works... yes

```
checking whether we are cross compiling... no
```

creating `config.h`

`configure`: creating `./config.status`

`config.status`: creating `Makefile`

`root@camus:usr/local/src/ruby-1.8.6-p111# make`

`root@camus:usr/local/src/ruby-1.8.6-p111# make`

```
gcc -g -02 -DRUBY_EXPORT -D_GNU_SOURCE=1 -I.- -I. -c array.c
gcc -g -02 -DRUBY_EXPORT -D_GNU_SOURCE=1 -I.- -I. -c bignum.c
make[1]: Leaving directory /usr/local/src/ruby-1.8.6-p111/ext/zlib/
making ruby
make[1]: Entering directory /usr/local/src/ruby-1.8.6-p111
gcc -g -02 -DRUBY_EXPORT -D_GNU_SOURCE=1 -ldynamic -Wl,-export-dynamic main.o -ruby-static -ld -lcrypt -lm -o ruby
make[1]: Leaving directory /usr/local/src/ruby-1.8.6-p111/
root@camus:usr/local/src/ruby-1.8.6-p111#
```

最后（见列表 28.3），输入 `make` 将生成的镜像安装到它们所在的位置（如 `Makefile` 中指定的和通过配置定义的）。其他选项如 `install`（它是 `Makefile` 中的规则）通常也是可用的，包括 `test`（对生成的镜像运行配置后的测试）或 `clean`（移除构建的对象）等。要完全清理分发目录，通常包含 `dist-clean`。

## 列表 28 最后安装过程

```
root@camus:/usr/local/src/ruby-1.8.6-p111# make install
./minuby --instry.rb -dest-dir=".ext" -extout=".ext" -make="make"
mflags="--make-flags*--installed-list installed.list -mantype="doc"
installing binary commands
installing command scripts
installing library scripts
installing headers
installing manpages
installing extension objects
installing extension scripts
root@camus:/usr/local/src/ruby-1.8.6-p111# ruby -version
ruby 1.8.6 (2007-09-24 patchlevel 111) [i686-linux]
root@camus:usr/local/src/ruby-1.8.6-p111#
```

# 第 28 章 GNU/Linux 管理基础

## 高级软件包工具 (APT)

高级软件包工具 (`APT`) 是一种用于处理 Debian 及其 Linux 发行版中软件包的命令行实用。它简化了软件的安装、升级和删除。

### 表 28.2 apt-get 命令

| apt-get 命令 | 说明 |
| :--- | :--- |
| update | 同步软件包索引 |
| upgrade | 安装已安装包的最新版本 |
| dist-upgrade | 安装所有依赖包的最新版本 |
| install | 安装多个新包 |
| remove | 删除已安装包 |
| source | 让 apt 获取源码 |
| check | 更新包索引并检查 |
| autoclean | 清除过期的软件包 |

### Lua 脚本语言

`Lua` 是一种小型、可嵌入其他系统（如游戏）以扩展它们的脚本语言。它是一种有趣的语言，因此拥有它很有用。

## 列表 28.4 使用 apt-cache 查找软件包

```
root@camus:~# apt-cache search lua
ogen - 一个自动化文本文件生成器
perl - 嵌入 Perl 5 语言
example-content - Ubuntu 示例内容
exuberant-ctags - 源代码定义的标签索引
...
loldevua-dev - 将 C/C++ 与 Lua 集成的工具 - 开发文件
loldevua - 将 C/C++ 与 Lua 集成的工具 - 运行时库
lightpd-mod-cml - lightpd 的缓存元语言模块
lua-mode - 编辑 Lua 程序的 Emacs 模式
lua40 - 具有简单过程语法的小型嵌入语言
lua40-doc - Lua 4.0 编程语言的文档
lua5.1 - 简单、可扩展的嵌入编程语言
lua5.1-doc - Lua 5.1 编程语言的文档
luocket - Lua 5.0 的 TCP/UDP 套接库
luocket-dev - Lua 5.0 的 TCP/UDP 套接库开发
```

## 列表 28.5 使用 apt-get 安装新包

```
root@camus:~# apt-get install lua5.1
Reading package lists... Done
Building dependency tree... Done
```

# 548 GNU/Linux 应用程序编程

将安装以下新软件包：
`lua5.1`
0 个升级，1 个新安装，0 个待移除，58 个未升级。
需要获取 112kB 的归包。
解压后将使用 283kB 的额外磁盘空间。
获取: http://us.archive.ubuntu.org dapper/universe lua5.1 5.1-1 [112kB]
已在 1 秒内获取 112kB (69.6KB/s)
正在选择已取消选择的软件包 lua5.1。

(正在读取数据库 ... 当前已安装 30053 个文件和目录。
正在从 .../archives/lua5.1_5.1-1_i386.deb 解压 lua5.1 ...
正在设置 lua5.1 (5.1-1) 

```
root@camus:~# lua
Lua 5.1 Copyright (C) 1994-2006 Lua.org, PUC-Rio
```

如列表 28.5 所示，系统读取软件包列表和依赖树，并找到要安装的软件包。`apt-get` 工具确定了归包的大小（将下载的内容）以及安装所需的空间。然后下载、解压并安装软件包。最后，执行 `lua` 解释器以演示完成的整个。
如果 `Lua` 有任何在系统中未被满足的依赖项，这些软件包也会被下载并安装，以确保所需的软件包是完整的。
现在来看 apt 的真正实力：它还具有移除软件包的能力。这在传统的安装过程中是无法实现的，但因为 apt 会跟踪某个软件包安装了哪些内容，因此它可以使用这些信息移除已安装的内容。列表 28.6 展示了如何使用 `apt-get` 移除软件包。

## 列表 28.6 使用 apt-get 移除已安装的软件包

```
root@camus:/home/mtj# apt-get remove lua5.1
正在读取软件包... 完成
正在构建依赖树... 完成
以下软件包将被 REM移除：
lua5.1
0 个升级，0 个新安装，1 个待移除，58 个未升级。
需要获取 0B 的归包。
解压后将释放 283kB 磁盘空间。
确定继续吗 [Y/n]? Y
(正在读取数据库 ... 当前已安装 33060 个文件和目录。
正在移除 lua5.1 ...
root@camus:/home/mtj#
```
