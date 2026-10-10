
### dconf

`dconf` `read` `KEY`

`dconf` `list` `DIR`

`dconf` `write` `KEY` `VALUE`

`dconf` `reset` `[-f]` `PATH`

`dconf` `compile` `OUTPUT` `KEYDIR`

`dconf` `update`

`dconf` `watch` `PATH`

`dconf` `dump` `DIR`

`dconf` `load` `DIR`

`dconf` `help` `[COMMAND]`

#### 描述
`dconf` 程序可以对 `dconf` 数据库执行各种操作，例如读取或写入单个值或整个目录。此工具直接作用于 `dconf`，不使用 `gsettings` schema 信息。因此，它无法对值进行类型和一致性检查。如果需要此类检查，可以使用 `gsettings(1)` 工具作为替代方案。

`DIR` 参数必须是目录路径（以 `'/'` 开头并结尾），`KEY` 参数必须是键路径（以 `'/'` 开头，但不以 `'//'` 结尾），`PATH` 参数可以是目录路径也可以是键路径。

`OUTPUT` 参数必须是写入（二进制）`dconf` 数据库的位置，而 `KEYFILEDIR` 参数必须是一个包含键文件的 `.d` 目录。

`VALUE` 参数必须是 `GVariant` 格式，例如，一个字符串必须包含显式引号：`"foo"`。此格式也用于在输出值时。

请注意，`dconf` 需要一个 D-Bus 会话总线连接才能将更改写入 `dconf` 数据库。

#### 命令
`read`
读取键的值。

`list`
列出目录的子键和子目录。

`write`
向键写入新值。

`reset`
重置键或整个目录。对于目录，必须指定 `-f`。

`compile`
从键文件编译二进制数据库。结果始终是小端字节序，因此可以安全地安装在 `share` 中。如果在大端机器上使用，`dconf` 将在读取时自动交换内容。

`update`
更新系统的 `dconf` 数据库。

`watch`
监控键或目录的变化。

`dump`
将整个子路径转储到标准输出。输出采用类似于键文件的格式，值使用 `GVariant` 语法。

`load`
从标准输入填充子路径。预期的格式与 `dump` 产生的格式相同。

`help`
显示帮助并退出。如果给出 `COMMAND`，则显示该命令的帮助。

#### 环境变量
`DCONF_PROFILE`
此环境变量决定使用哪种 `dconf` 配置文件。参见 `dconf(7)`。

#### 参见
`dconf(7)`, `gsettings(1)`, `dconf-editor(1)`

### dd - 转换并复制文件

#### 概要
```
dd [OPERAND]...
dd OPTION
```

#### 描述
复制文件并根据操作数进行转换和格式化。

```
bs=BYTES
```
一次读写最多 `BYTES` 字节

```
cbs=BYTES
```
一次转换 `BYTES` 字节

```
conv=CONVS
```
根据逗号分隔的符号列表转换文件

```
count=N
```
仅复制 `N` 个输入块

```
ibs=BYTES
```
一次读取最多 `BYTES` 字节（默认值: 512）

```
if=FILE
```
从 `FILE` 而不是标准输入读取

```
iflag=FLAGS
```
根据逗号分隔的符号列表读取

```
obs=BYTES
```
一次写入 `BYTES` 字节（默认值: 512）

```
of=FILE
```
写入 `FILE` 而不是标准输出

```
oflag=FLAGS
```
根据逗号分隔的符号列表写入

```
seek=N
```
在输出开始处跳过 `N` 个 `obs` 大小的的块

```
skip=N
```
在输入开始处跳过 `N` 个 `ibs` 大小的的块

```
status=LEVEL
```
打印到 stderr 的信息级别；`'none'` 抑制错误消息以外的所有内容，`'noxfer'` 抑制最后的传输统计，`'progress'` 显示定期的传输统计。

`N` 和 `BYTES` 后可以跟以下乘法后缀：`c =1`, `w =2`, `b =512`, `kB =1000`, `K =1024`, `MB =1000*1000`, `M =1024*1024`, `xM =M` `GB =1000*1000`, `G =1024*1024`，以此类推 `T`, `E`, `Y`。

每个 `CONV` 符号可以是：

```
ascii
```
从 EBCDIC 转换为 ASCII

```
ebcdic
```
从 ASCII 转换为 EBCDIC

```
ibm
```
从 ASCII 转换为备用 EBCDIC

```
block
```
用空格填充 `cbs-size` 的换行符终止记录

```
unblock
```
将 `cbs-size` 末尾的空格替换为换行符

```
ucase
```
将大写改为小写

```
sparse
```
将小写改为大写

```
swab
```
对于 `NUL` 输入块，尝试寻址而不是写入输出

```
sync
```
每同步一对 `ibs-size` 大小的输入字节；当与 `block` 或 `unblock` 使用时，用空格填充而非 `NUL`

```
nocreat
```
如果输出文件已存在则失败

```
notrunc
```
不创建输出文件

```
noerror
```
在读取错误后继续

```
async
```
在物理写入输出数据之前

```
fsync
```
同样写入元数据

```
append
```
模式追加

```
direct
```
写入元数据

直接作用于 I/O

```
fullblock
```
完整块

```
dsync
```
同样写入元数据

```
nonblock
```
非阻塞使用

```
noatime
```
不更新访问时间

```
nocache
```
丢弃缓存

```
notty
```
不分配终端

```
nofollow
```
不跟踪符号链接

```
count_bytes
```
计数

详细文档见：`http://www.gnu.org/software/`

### deallocvt - 释放空闲虚拟终端

#### 概要
`deallocvt [N]`

#### 描述
该命令释放所有空闲虚拟终端的内存和数据结构。如果给出一个多个参数 `N`，则释放对应的 `/dev/ttyN`。

如果一个虚拟终端不是前台终端，没有进程对其打开读取或写入，且屏幕上没有文本，则它就是空闲的。

#### 参见
`chvt(1)`, `openvt(1)`

### delv - DNS 查询与验证工具

#### 概要
```
delv [@server] [-4] [-6] [-a anchor-file] [-b address] [-c class] [-d level] [-i] [-m] -p port|[-q name] [-t type] [-x addr] [name] [type] [class] [queryopt...]
delv [-h]
delv [-v]
delv [queryopt...] [query...]
```

#### 描述
`delv`（实体查询与验证）是一个发送 DNS 查询并验证结果的工具，使用了与 `named` 相同的内部解析器和验证器。

`delv` 将向指定的服务器发送获取和验证所需的所有查询；这包括原始请求查询、跟随 `CNAME` 或 `DNAME` 链的后续查询，以及用于建立信任链的 `DNSKEY`、`DS` 和 `DLV` 记录。它不执行迭代解析，而是模拟了配置了 DNSSEC 验证和转发的服务器的行为。

默认情况下，使用内置的 DNSSEC 信任锚对根区域 `(.)` 以及 ISC DNSSEC 旁路验证区域 (`"dlv.isc.org"`) 进行验证。`delv` 返回的记录要么经过完全验证，要么未签名。如果验证失败，输出中包含失败的解释；可以详细跟踪验证过程。由于 `delv` 不依赖外部服务器执行验证，因此它可以在本地 DNS 服务器可能不可信的环境中检查 DNS 响应的有效性。

除非指定特定的服务器，`delv` 将尝试 `/etc/resolv.conf` 中列出的所有服务器。如果没有找到可用的服务器地址，`delv` 将向本地地址发送查询（IPv4 为 `127.0.0.1`，IPv6 为 `::1`）。

当没有给出命令行参数或选项时，`delv` 将对 `"."`（根区域）执行 `NS` 查询。

#### 简单用法
`delv` 的典型调用方式如下：
```
delv @server name type
```
其中：

`server`
是要查询的名称服务器的名称或 IP 地址。它可以是点分十进制表示的 IPv4 地址，也可以是冒号分隔表示的 IPv6 地址。当提供的 `server` 参数为主主机名时，`delv` 在查询该名称服务器之前会解析名称（但注意，此初始查找不会通过 DNSSEC 验证）。

如果未提供 `server` 参数，`delv` 将查询 `/etc/resol.conf`；如果在该文件中找到地址，则只使用该地址的服务器。如果使用了 `-4` 或 `-6` 选项中的任一，则仅尝试对应传输协议的地址。如果未找到可用的地址，`delv` 将向本地地址发送查询（IPv4 为 `127.0.0.1`，IPv6 为 `::1`）。

`name`
是要查找的域名。

`type`
表示所需的查询类型 – `ANY`、`A`、`MX` 等。`type` 可以是是任何有效的查询类型。如果未提供 `type` 参数，`delv` 将对 `A` 记录进行查找。

#### 选项
`-anchor-file`
指定从文件中读取 DNSSEC 信任锚点。默认是 `/etc/bind.keys`，该文件随 `BIND 9` 一起，包含根区域（`"."`）和 DNSSEC 旁路验证区域（`dlv.isc.org"`）的信任锚点。

与查询或 `DLV` 信任锚点名称匹配匹配密钥将被忽略；这些密钥名称可以使用 `+dlvNAME` 和 `+root=NAME` 选项进行覆盖。
