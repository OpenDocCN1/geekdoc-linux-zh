
## 6.9. Glib 内容

已安装程序：

已安装的库：`ld-2.27.so`, `libBkenLocale.[a,so]`, `LibSegFault.[a,so]`, `libdl.[a,so]`, `libc.[a,so]`, `lib_nonshared.a`, `libcid.[a,so]`, `libcrypt.[a,so]`, `libg.[a,so]`, `libieee.a. libm.[a,so]`, `libmchecka.[a,so]`, `libmenusage.[a,so]`, `libndl.[a,so]`, `libnss_compat.so`, `libnss_ds.so`, `libnss_files.so`, `libnss_hesid.so`, `libnss_nis.so`, `libnss_nisplus.so`, `libthread.[a,so]`, `libthread_nonshared.a`, `libresol.[a,so]`, `libprcvc.so`, `libt.[a,so]`, `libthread_db.[a,so]`, `libutil.[a,so]`.

已安装的目录：

`/usr/include/arpa`, `/usr/include/bits`, `/usr/include/gnu`, `/usr/include/net`, `/usr/include/netush`, `/usr/include/nettalak`, `/usr/include/net25`, `/usr/include/netcomque`, `/usr/include/netinet`, `/usr/include/netipx`, `/usr/include/netiuc`, `/usr/include/netpacket`, `/usr/include/netrom`, `/usr/include/netrose`, `/usr/include/nfs`, `/usr/include/protocols`, `/usr/include/rpc/`, `/usr/include/rpcsvc`, `/usr/include/sys`, `/usr/lib/audit`, `/usr/lib/gconv`, `/usr/lib/local`, `/usr/libexec/get`, `/usr/share/lib18`, `/usr/share/zoneinfo`, `/var/cache/nscd`, and `/var/lib/n_db`

### 简要描述

- `catchsev` | 可用于在程序因段错误终止时创建跟踪堆栈
- `gencat` | 生成消息目录
- `getconf` | 显示文件系统特定变量的系统配置值
- `entent` | 从管理数据库中获取条目
- `iconv` | 执行字符集转换
- `iconfig` | 创建快速加载的 icon 模块配置文件
- `ldconfig` | 配置动态链接器运行时绑定
- `ldd` | 报告每个给定的程序或共享库需要哪些共享库
- `ldibc4c` | 辅助 `ldd` 处理对象文件
- `locale` | 打印关于当前语言区域的各种信息
- `localedef` | 编译位置规范
- `makedb` | 从文本输入创建简单的数据库
- `mtrace` | 读取并解释内存跟踪文件，并以人类可读的格式显示摘要
- `nscd` | 为常见的名称服务请求提供缓存的守护进程
- `pldd` | 列出运行进程使用的动态共享对象
- `sln` | 静态链接的程序
- `struss` | 跟踪指定命令的共享库过程调用
- `sprof` | 读取并显示共享对象的分析数据
- `tzselect` | 询问用户系统位置并报告相应的时区描述
- `xtrace` | 通过打印当前执行的函数来跟踪程序的执行
- `dump` | 时区转储器
- `zic` | 时区编译器
- `ld-2.27.so` | 共享库可执行文件的辅助程序
- `libBrokenLocale` | Glibc 内部使用的一种黑科技，用于让损坏的程序（例如某些 Motif 应用）运行。更多信息请参阅 `glibc-2.27/locale/broken_cur_max.c` 中的注释
- `libSegFault` | 段错误信号处理器，由 `catchsegy` 使用
- `liban` | 异步名称查找库
- `libc` | 主 C 库
- `libcidn` | Glibc 内部使用，用于在 `getaddrinfo()` 函数中处理国际化域名
- `libcrypt` | 密码学库
- `libdl` | 动态链接接口库。以前是 `g++` 的运行时库
- `libg` | 不包含任何函数的空库。在此模块中链接将强制执行由电气电子工程师 (IEEE) 定义的数学函数错误处理规则。默认是 POSIX.1 错误处理
- `libm` | 数学库
- `libcheck` | 链接时开启内存分配检查
- `libmemusage` | 内存用于帮助收集程序的内存使用信息
- `libnsl` | 网络服务库
- `libnss` | 名称服务切换库，包含解析主机名、用户名、组名、别名、协议等函数
- `libthread` | POSIX 线程库
- `libresolv` | 包含创建、发送和解释到 Internet 名称服务器包的函数
- `libprcsv` | 包含提供杂项 RPC 服务的函数
- `librt` | 包含 POSIX.1b 实时扩展指定的多数接口
- `libthread_db` | 包含有助于构建多线程程序调试器的函数
- `libutil` | 包含许多不同 Unix 工具使用的“标准”函数代码

## 6.10. 调整工具链

现在最终的 C 库已经安装，是时候调整工具链，以便将新编译的程序链接到这些库了。

首先，备份 `/tools` 链接器，并用我们在第 5 章中制作的调整链接器替换它。我们会在 `/tools/$(uname -m)-pc-linux-gnu/bin` 中创建一个链接：

```bash
mv -v /tools/bin/{ld,ld-old}
mv -v /tools/$(uname -m)-pc-linux-gnu/bin/{ld,ld-old}
mv -v /tools/bin/ld-new,ld
ln -sv /tools/bin/ld /tools/$(uname -m)-pc-linux-gnu/bin
```

接下来，添加 GCC 规范文件指向新的动态链接器。删除所有 "tools" 实例即可获得动态链接器的正确路径。调整规范文件使 gcc 知道哪里找到正确的头文件和 Glibc 部分。使用 `sed` 命令可以实现：

```bash
gcc -dumpspec | sed -e '^@tools@$g' \
-e '^@startfile_prefix_spec;/(n;s@*//usr/lib/@' \
-e '^@cpp/(n;s@@-system /usr/include/@' \
-dinarame $(gcc --print-libgcc-file-name)'/specs
```

检查规范文件以验证预期更改已生效是一个良好的做法。
确保基本功能正常工作至关重要。

## 6.11. Zlib-1.2.11

Zlib 软件包包含某些程序使用的压缩和解压程序。

预计编译时间：少于 0.1 SBU
所需磁盘空间：4.5 MB

### 6.11.1. 安装 Zlib

为编译准备 Zlib：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

执行以下命令以测试结果：

```
make check
```

安装软件包：

```
make install
```

需要将共享库移动到 `/lib`，结果是 `/usr/lib` 中的 `.so` 文件需要重新创建：

```
mv -v /usr/lib/libz.so.* /lib
ln -sf ../lib/$(readlink /usr/lib/libz.so) /usr/lib/libz.so
```

### 6.11.2. Zlib 内容

已安装的库：`libz.{a,so}`

### 简要描述

- `zlib`：包含某些程序使用的压缩和解压函数

## 6.12. File-532

File 软件包包含一个用于确定给定文件或文件类型的工具。
预计编译时间：0.1 SBU
所需磁盘空间：16 MB

### 6.12.1. 安装 File

为编译准备 File：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

执行以下命令以测试结果：

```
make check
```

安装软件包：

```
make install
```
