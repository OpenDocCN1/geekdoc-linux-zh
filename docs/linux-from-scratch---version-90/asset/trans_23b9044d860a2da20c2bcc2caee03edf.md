

## 6.61. Less-551

Less 软件包包含一个文本查看器。

预计编译时间：少于 0.1 SBU
所需磁盘空间：4.1 MB

### 6.61.1. 安装 Less

为编译准备 Less：

```
./configure --prefix=/usr --sysconfdir=/etc
```

配置选项的含义：

--sysconfdir=/etc
该选项告诉由该包创建的程序去 /etc 查找配置文件。

编译软件包：

```
make
```

此软件包不附带测试套件。

安装软件包：

```
make install
```

### 6.61.2. Less 的内容

已安装程序：
less, lessecho 和 lesskey

### 简要说明

- less | 文件查看器或分页器；它显示给定文件的内容，允许用户滚动滚动、查找字符串并跳转到标记
- lessecho | 在 Unix 系统上需要扩展文件名中的元字符（如 * 和 ?）
- lesskey | 用于指定 less 的按键绑定

## 6.62. Gzip-1.10

Gzip 软件包包含用于压缩和解压缩文件的程序。

预计编译时间：0.1 SBU
所需磁盘空间：20 MB

### 6.62.1. 安装 Gzip

为编译准备 Gzip：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

要测试结果，执行：

```
make check
```

在 LFS 环境中已知两个测试会失败：help-version 和 zmore。

安装软件包：

```
make install
```

移动一个需要位于根文件系统上的程序：

```
mv -v /usr/bin/gzip /bin
```

### 6.62.2. Gzip 的内容

已安装程序：
gunzip, gzexe, gzip, uncompress (gunzip 的硬链接), zcat, zcmp, zegrep, zdiff, zfgrep, zforce, zgrep, zmore 和 znew

### 简要说明

- gunzip: 解压缩压缩文件
- gzexe: 创建自解压的可执行文件
- gzip: 使用 Lempel-Ziv (LZ77) 算法压缩给定文件
- uncompress: 解压缩压缩文件
- zcat: 将指定的压缩文件解压到标准输出
- zcmp: 对 gzip 压缩的文件运行 cmp
- zdiff: 对 gzip 压缩的文件运行 diff
- zegrep: 对 gzip 压缩的文件运行 egrep
- zfgrep: 对 gzip 压缩的文件运行 grep
- zforce: 强制为所有给定的 gzip 文件添加 .gz 扩展，以便 gzip 不会再次压缩；这在文件名在传输过程中被截断时非常有用
- zgrep: 对 gzip 压缩的文件运行 grep
- zless: 对 gzip 压缩的文件运行 less
- zmore: 对 gzip 压缩的文件运行 more
- znew: 将文件从 compress 格式重新压缩为 gzip 格式。Z 转换为 .gz

## 6.63. IPRoute2-5.2.0

IPRoute2 软件包包含用于基础和高级 IPv4 网络的网络的程序。

预计编译时间：0.2 SBU
所需磁盘空间：13 MB

### 6.63.1. 安装 IPRoute2

此软件包包含的 arpd 程序将不会编译，因为它依赖于 Berkeley DB，而 LFS 中没有安装该数据库。但是仍然会安装 arpd 目录和帮助页。通过运行以下命令可以防止这种情况。如果需要 arpd 二进制文件，可以在 BLFS 书中找到编译 Berkeley DB 的说明，：http://www.linuxfromscratch.org/blfs/9.0/server/databases.html#db。

```
sed -i /ARPd/Makefile
rm -fv man/man8/arpd.8
```

还需要禁用构建两个需要 http://www.linuxfromscratch.org/blfs/9.0/postlfs/iptables.html 的模块。

```
sed -i 's/..ipt.o//' tc/Makefile
```

编译软件包：

```
make
```

此软件包没有可用的测试套件。

安装软件包：

```
make DOCDIR=/usr/share/doc/iproute2-5.2.0 install
```

### 6.63.2. IPRoute2 的内容

- 已安装程序：bridge, cstat (链接至 Inst), genl, ifcfg, ifstat, ip, Inst, nroute, rout, rtl, rtac, rtmon, rtptr, rtstat (链接至 Inst), ss 和 tc
- 已安装目录：/iproute2, /usr/lib/tc 和 /usr/share/doc/iproute2-5.2.0，

### 简要说明

- bridge: 配置网桥
- cstat: 连接状态工具
- geni: 通用链路工具前端
- ifcfg: ip 命令的 shell 封装 [注意它需要来自 http://www.skbuff.net/iputils/ iputils 包的 arping 和 rdisk 程序]
- ifstat: 显示接口统计，包括包括接口发送和接收的数据包数量
- ip: 主执行文件。它有多个不同的功能：
  - ip link <device>允许用户查看设备状态并进行更改
  - ip addr允许用户查看地址及其属性、添加新地址并删除旧条目
  - ip neighbor允许用户查看邻居绑定及其属性、添加新邻居条目并删除旧条目
  - ip rule允许用户查看路由策略并更改它们
  - ip route允许用户查看路由表并更改路由表规则
  - ip tunnel允许用户查看 IP 隧道及其属性并更改它们
  - ip maddr允许用户查看多播地址及其属性并更改它们
  - ip mroute允许用户设置、更改或删除多播路由
  - ip monitor允许用户持续监控设备、地址和路由的状态
- 提供 Linux 网络统计信息；它是旧 rstat 程序的更通用且功能更完整的替代品

