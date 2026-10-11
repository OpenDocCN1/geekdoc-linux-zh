
安装软件包：

```
make install
```

### 6.31.2. Grep 的包含内容

已安装的程序：`egrep`, `fgrep` 和 `grep`

#### 简短描述

- `egrep`: 打印匹配扩展正则表达式的行
- `fgrep`: 打印匹配固定字符串列表的行
- `grep`: 打印匹配基本正则表达式的行

## 6.32. Readline-7.0

Readline 软件包是一组库，提供了命令行编辑和历史记录功能。
预计编译时间：0.1 SBU
所需磁盘空间：15 MB

### 6.3.1. 安装 Readline

重新安装 Readline 会导致旧库移动到 `<libraryname>.old`。虽然这没有问题，但在某些情况下，它可能会触发 `ldconfig` 中的链接 bug。可以通过执行以下两条命令来避免这种情况：

```
sed -i '/MV.*old/d' Makefile.in
sed -i '/{OLDSUFF}/c:' support/shlib-install
```

为编译准备 Readline：

```bash
./configure --prefix=/usr --disable-static \
  --docdir=/usr/share/doc/readline-7.0
```

编译软件包：

```
make SHLIB_LIBS=-lncurses
```

该选项的含义：
`SHLIB_LIBS=-lncurses`
此选项强制 Readline 链接到 `libncursesw`（实际上是 `libncursesw`）库。
此软件包不带测试套件。

安装软件包：

```
make SHLIB_LIBS=-lncurses install
```

将动态库移动到更合适的位置并修复一些符号链接：

```bash
mv -v /usr/lib/lib{readline,history}.so.* /lib
ln -sf ../lib/$(basename /usr/lib/libreadline.so) /usr/lib/libreadline.so
ln -sf ../lib/$(basename /usr/lib/libhistory.so ) /usr/lib/libhistory.so
```

如果需要，安装文档：

```bash
install -v -m644 *.{pdf,html,dvi} /usr/share/doc/readline-7.0
```

### 6.3.2. Readline 的包含内容

已安装的库：`libhistory.so` 和 `readline.so`
已安装的目录：`/usr/include/readline`, `/usr/share/readline` 以及 `/usr/share/doc/readline-7.0`

#### 简短描述

- `history`: 为回溯历史行提供一致的用户界面
- `libreadline`: 帮助在需要提供命令行界面的离散程序之间保持用户界面的一致性

## 6.33. Bash-4.4

Bash 软件包包含了 Bourne-Again Shell 的修复。
预计编译时间：1.7 SBU
所需磁盘空间：56 MB

### 6.33.1. 安装 Bash

合并上游修复：

```bash
patch -Npl1 -i ../bash-4.4-upstream-fixes-1.patch
```

为编译准备 Bash：

```bash
./configure --prefix=/usr \
--docdir=/usr/share/doc/bash-4.4 \
--without-bash-malloc \
--with-installed-readline \
```

新配置选项的含义：

```
--with-installed-readline
```

此选项告诉 Bash 使用系统已安装的 readline 库，而不是使用它自带的 readline 版本。

编译软件包：

```bash
make
```

如果不运行测试套件，请跳到“安装软件包”。

要准备测试工作，请确保 `nobody` 用户可以向源码树写入内容：

```bash
chown -Rv nobody .
```

现在，以 `nobody` 用户身份运行测试：

```bash
su nobody -s /bin/bash -c "PATH=$PATH make tests"
```

安装软件包并将主执行文件移动到 `/bin`：

```bash
make install
mv -vf /usr/bin/bash /bin
```

运行新编译的 bash 程序（替换当前执行的程序）：

```bash
exec /bin/bash --login +
```

> 注意
> 使用的参数使 bash 进程成为交互登录 shell，并继续禁用哈希处理，以便在新程序可用时能被找到。

### 6.33.2. Bash 的包含内容

已安装的程序：`bash`, `bashbug` 和 `sh`（指向 bash 的链接）
已安装的目录：`/usr/share/doc/bash-4.4`

#### 简短描述

- `bash`: 一个广泛使用的命令解释器；它在执行给定命令行之前会对其进行许多类型的扩展和替换，因此使该解释器成为一个强大的工具
- `bashbug`: 一个 shell 脚本，帮助用户编写并发送关于 bash 的标准格式 bug 报告
- `sh`: 指向 bash 程序的符号链接；当作为 sh 被调用时，bash 尝试尽尽可能地模拟历史版本 sh 的启动行为，同时符合 POSIX 标准

## 6.34. Bc-1.06

Bc 软件包包含一个任意精度计算器。
预计编译时间：0.1 SBU
所需磁盘空间：6 MB

### 6.34.1. 安装 Bc

合并上游修复：

```bash
patch -Npl1 -i ../bash-4.4-upstream-fixes-1.patch
```

为编译准备 Bc：

```bash
./configure --prefix=/usr \
--with-readline \
--mandir=/usr/share/man \
--infdir=/usr/share/info
```

配置选项的含义：

```
--with-readline
```

此选项告诉 Bc 使用系统已安装的 readline 库。

编译软件包：

```bash
make
```

如果不运行测试套件，请跳到“安装软件包”。

要准备测试，请确保 `nobody` 用户可以向源码树写入内容：

```bash
chown -Rv nobody .
```

现在，以 `nobody` 用户身份运行测试：

```bash
su nobody -s /bin/bash -c "PATH=$PATH make tests"
```

安装软件包并将主执行文件移动到 `/bin`：

```bash
make install
mv -vf /usr/bin/bash /bin
```

运行新编译的 bash 程序（替换当前执行的程序）：

```bash
exec /bin/bash --login +
```

### 6.34.2. Bc 的包含内容

已安装的程序：`bc`, `dc`
已安装的目录：`/usr/share/doc/bc`

#### 简短描述

- `bc`: 任意精度计算器
- `dc`: 逆波兰表达式法计算器

## 6.35. Libtool-2.4

Libtool 软件包提供了通用的库构建支持。
预计编译时间：2.0 SBU
所需磁盘空间：43 MB

### 6.35.1. 安装 Libtool

为编译准备 Libtool：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

若要测试结果，请执行：

```
make check
```

安装软件包：

```
make install
```

### 6.35.2. Libtool 的包含内容

已安装的程序：`libtool`, `libtoolize` 和 `libtoold`
已安装的库：`libtool.so`
已安装的目录：`/usr/include/libtool`, `/usr/share/libtool`

#### 简短描述

- `libtool`: 提供通用的库构建服务
- `libtoolize`: 为软件包添加 libtool 支持的标准方法
- `libtoold`: 隐藏各种库的复杂性

## 6.36. GDBM-1.12

GDBM 软件包包含了 GNU 管理器。
预计编译时间：0.1 SBU
所需磁盘空间：9 MB

### 6.36.1. 安装 GDBM

为编译准备 GDBM：

```bash
./configure --prefix=/usr \
--enable-libgdbm-compat
```

编译软件包：

```
make
```

若要测试结果，请执行：

```
make check
```
