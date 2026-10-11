
## 命令

`ispell [common-flags] [-M|-N] [-Lcontext] [-V] files`

`ispell [common-flags] -I`

`ispell [common-flags] [-f file] [-s] {-a|-A}`

`ispell [-d file] [-w chars] -c`

`ispell [-d file] [-w chars] -e[e]`

`ispell -v[v]`

`ispell` 是一个拼写检查器。它根据字典检查文件中的单词，并建议替代的拼写方式。

示例：检查 "`thesis.txt`" 文件中单词的拼写：

`ispell thesis.txt`

`ispell` 具有一定的交互性；以下按键有效：

- `R` 完全替换拼写错误的单词。
- `Space`（空格格）仅本次接受该单词。
- `A` 在本次 `ispell` 会话剩余时间内接受该单词。
- `I` 接受单词，保持其在文件中的大小写形式，并更新私有字典。
- `U` 接受单词，并将其全小写版本添加到私有字典。
- `0-n` 替换为建议的单词之一。
- `L` 在系统字典中查找单词（由 `WORDS` 编译选项控制）。

### 400 杂杂

- `X` 写此文件的剩余部分，忽略拼写错误，并开始下一个文件。
- `Q` 立即退出并保持文件不变。
- `!` 终端转义（Shell escape）。
- `^L` 重绘屏幕。
- `^Z` 挂起 `ispell`。
- `?` 显示帮助屏幕。

### 命令行选项

- `-M` 在屏幕底部显示微菜单。
- `-L` 在显示中包含指定行数的上下文。
- `-V` 以 "`cat -v`" 的样式显示。
- `-t` 指定输入文件为 TeX 或 LaTeX 格式。
- `-n` 指定输入文件为 nroff/troff 格式。
- `-b` 告诉 `ispell` 通过在文件名后添加 `.bak` 来创建备份文件。
- `-x` 不创建备份文件。
- `-B` 将缺少空格的连写单词作为拼写错误报告。
- `-C` 将连写单词视为合法的复合词。
- `-P` 不要生成额外的根/后缀组合。
- `-m` 生成字典中不存在的可能的词根/后缀组合。
- `-S` 按可能的正确性对猜测列表进行排序。
- `-d file` 指定替代的字典文件。

### 命令 401

- `-p file` 指定替代的个人字典。
- `-w chars` 指定可以作为单词部分的额外字符。
- `-W n` 指定始终有效的单词长度。
- `-T type` 假设所有文件使用指定的格式类型。
- `-n` 指定 nroff/troff 输入模式。
- `-t` 指定 TeX/LaTeX 输入模式。
- `-b` 为每个输入文件生成备份文件。
- `-x` 除非发生错误否则不生成备份文件。
- `-B` 将连写单词（例如 runogether）视为错误。
- `-C` 将连写单词（例如 runogether）视为合法的复合词。
- `-m` 始终显示建议包含在字典中的词根/后缀组合。
- `-P` 当当前字典中没有合理可能性时，仅显示建议包含在字典中的词根/后缀组合。
- `-S` 不对可能的替换单词列表排序。
- `-d file` 使用指定的字典文件而不是默认文件。
- `-p` 使用指定的个人字典文件而不是默认文件。
- `-w` 允许指定的非字母字符。
- `-W` 指定一个“始终有效”的单词长度。
- `-T` 指定用于生成字符串字符的默认格式类型。
- `-l` 生成拼写错误的单词列表。

![](img/3ac9b27762bf6b1e48d880d6f0f96f8b_430_0.png)

### `printf FORMAT [ARGUMENT]...`

与 `printf` 函数类似。`FORMAT` 包含：

- `%d`, `%i` 十进制数
- `%o` 无符号八进制
- `%x`, `%X` 无符号十六进制
- `%u` 无符号十进制
- `%c` 单个字符
- `%s` 字符字符串
- `%f` 双精度；默认精度为 6
- `%e`, `%E` 双精度，默认精度为 6
- `%g`, `%G` 双精度；如果指数小于于 -4 或 >= 6
- `%p` 字面量指针

## 命令

`rpm -i [install-options] <package_file>`
`rpm -q [query-options]`
`rpm -V|y|--verify [verify-options]`
`rpm --checksig <package_file>`
`rpm -e <package_name>`
`rpm -b|t|O [build-options] <package>`
`rpm --rebuild`
`rpm --setperms [query-specifiers]`
`rpm --setids [query-specifiers]`
`rpm --show`

Red Hat 包管理器。`RPM` 有十种模式：安装、查询、验证、签名检查、卸载、构建、数据库和显示。

示例：从 CD 安装 WordPerfect：`rpm -i /mnt/cdrom`

### 通用选项

- `-vv` 非常详细。打印调试信息。
- `--keep-temps` 不要移除临时文件。
- `--quiet` 不打印任何可能的错误消息。

### 杂杂

- `--help` 显示详细用法。
- `--version` 显示版本号。
- `--file` 使用指定的文件代替 `/etc/rpmrc` 和 `$HOME/.rpmrc`。
- `--root` 所有操作位于 `<dir>`。
- `--dbpath` 使用路径下的 RPM 数据库。
- `--ftproxy` 指定主机作为 FTP 代理。
- `--ftpport` 指定端口。

### 安装和升级选项

- `-i` 安装新包。
- `-U` 升级包。注意在两种情况下，包可以指定 ftp URL。如果是这样，`rpm` 将在安装之前完成。
- `--force` 等同于 `--replacegs,--replacefiles` 和 `--oldpackage`。
- `-h,--hash` 显示包存档的哈希标记。配合 `-v` 进行良好显示。
- `--oldpackage` 允许用旧包替换新包。
- `--percent` 显示包包的百分比。
- `--replacefiles` 强制 `rpm` 安装来自其他已安装包的文件。
- `--replacegs` 如果某些包已安装，强制 `rpm` 安装包。

### 查询选项

- `-q package_name` 告诉 `rpm` 查询指定的包。
- `-a` 查询所有已安装的包。
- `--whatrequires <capability>` 查询所有需要指定能力才能正常工作的包。
- `--whatprovides <virtual>` 查询提供 `virtual` 能力的所有包。
- `-f <file>` 查询拥有文件的包。

### 信息选择选项

- `-i` 显示包信息（名称、版本和描述）。
- `-R` 列出此依赖的包。
- `--provides` 列出此包提供的能力。
- `--changelog` 显示包的变更信息。
- `-l` 列出包中的文件。
- `-s` 显示包中文件的状态（正常、未安装、已替换）。
- `-d` 仅列出文档文件。
- `-C` 仅列出配置文件。
- `--scripts` 列出作为安装/卸载过程部分的包特定 shell 脚本。
- `--triggers` 显示包中的任何触发脚本。

## 命令

`--dump` 导出文件信息如下：path size mtime md5sum mode owner group isconfig isdoc rdev symlink。必须与 `-l`, `-c`, `-d` 之一使用。

`-V`, `-y`, `--verify`
验证选项将安装的包与存储在 `rpm` 数据库中的信息进行比较。verify 选项的输出是一个 8 个字符的字符串，点表示测试通过或以下字符之一表示测试失败：

- `5` MD5 和
- `S` 文件大小
- `L` Svmlink
- `T` Mtime
- `D` 设备
- `U` 用户
- `G` 组
- `M` 模式（包括权限和文件类型）

### 签名检查

`--checksig` 检查包内置的 PGP 签名以确保包的完整性和来源。

### 卸载选项

`--e package_name` 卸载指定的包。
`--allmatches` 所有匹配 `package_name` 的包版本。
`--noscripts` 抑制预安装或卸载脚本的执行。
`--notriggers` 不执行由删除此包触发的脚本。
`--nodeps` 告诉 `rpm` 在删除包之前跳过通常执行的损坏依赖检查。
`--test` 不实际卸载包，仅报告卸载的潜在问题。

### 构建选项

- `-b` 用于指定构建源为一个 spec 文件。
- `-t` 用于指定 spec 文件包含在 gzipped 压缩的 tar 包中。
- `-bp` 执行来自 spec 文件的 `"%prep%"` 阶段。这通常涉及解包源码并应用任何补丁。
- `-bl` 告诉 `rpm` 执行检查以确保所有文件都存在。
- `-bc` 告诉 `rpm` 执行 spec 文件中的 `"%build%"` 阶段。
- `-bi` 告诉 `rpm` 执行 spec 文件中的 `"%install%"` 阶段。
- `-bb` 告诉 `rpm` 构建二进制包。
- `-ba` 告诉 `rpm` 构建二进制包和源码包。

### 其他选项

- `--short-circuit` 直接跳到指定的阶段。
- `--timecheck` 指定正在打包的文件最大年龄（以秒为单位）。
- `--clean` 在制作包后删除构建树。
- `--rmsource` 告诉 `rpm` 在构建后删除源码文件和 spec 文件。
- `--test` 抑制构建阶段的执行。
- `--sign` 告诉 `rpm` 在包中嵌入 PGP 签名。
- `--rebuild <source_package_file>` 构建一个新的二进制包。

### 为现有 RPM 签名

- `-resign <binary_package_file>` 为现有包插入新的 PGP 签名。

### PGP 签名

显然，为了使用 PGP 签名，RPM 必须能够找到 PGP 软件包，并且必须有一个包含 RPM 公钥的公钥环。如果 PGP 包位于默认位置以外的任何地方，你应该在你的 `/etc/rpmrc` 文件中设置以下变量：

- `-pgp_path` `/usr/rpm` 的替换路径。必须包含你的密钥环。
- `-signature` 签名类型。目前仅支持 pgp。
- `-pgp_name` 你希望使用其密钥对你的包签名的“用户”名称。
- `-sign` 此选项将导致你在构建包时被提示输入“密码 phrase（pass phrase）”。

### 重建数据库选项

- `-rebuilddb` 重建数据库信息
- `-rpm --showrc` 显示 RPM 将用于所有在 rpmrc 文件中可能设置的选项的值。

### FTP 选项

RPM 源可以是 FTP 站点。使用以下 URL 语法：
`ftp://<user>:<password>@hostname/path/to/package.rpm`

- `-ftppxy <hostname>` 使用指定的主机名作为所有传输的代理服务器。
- `-ftpport <port>` 使用指定的 TCP 端口进行 ftp 连接。

`strfile [-iersx] [-c char] sourcefile [outputfile]`

`unstr [-c char] datafile[.ext] [outputfile]`

`strfile` 的输入是一个包含行组的文件，这些行组默认由 `%` 符号分隔。它会创建一个包含头部结构和文件偏移量表的数据文件（`sourcefile.dat`，除非另有指定）。

`unstr` 按照头部文件 `datafile` 中列出的顺序打印 `sourcefile` 中的字符串。

示例：此命令除了维护 `fortune`（幸运言）程序数据库外，真的没大用。要显示 `fortune` 文件 `pithy.dat` 的内容：

`unstr pithy`

| 标志 (Flag) | 描述 (Description) |
|---|---|
| `-c char` | 将分隔符更改为指定的字符。 |
| `-i` | 在排序字符串时忽略大小写。 |
| `-o` | 按字母顺序排序字符串。 |
| `-r` | 随机访问字符串。 |
| `-s` | 静默选项（完成后不显示摘要消息）。 |
| `-x` | 在头部中设置 `STR_ROTATED` 位。 |

### 第 4 部分

### 网络

### 第 29 章

### TCP/IP

#### 引言

`TCP/IP` 代表传输控制协议/网际协议，指的是一组用于在分布式计算机网络之间传输消息的数据传输协议集合。

本节中的示例将基于以下网络（见图 29-1）：

| Odin | Fenris | Loki | Thor |
|---|---|---|---|
| red Hat 5.2 | Caldera 1.3 | Win '95 | Win '98 |
| 192.168.100.1 | 192.168.100.80 | 192.168.100.10 | 192.168.100.20 |

![](img/29-142_0.png)

图 29-1 示例网络

#### OSI 参考模型

大多数关于 `TCP/IP` 的讨论都带有 `OSI`（开放系统互连）参考模型。`OSI` 模型创建于 1978 年，用于开发网络标准。现实世界的协议设计者从以来一直忽略它，但当人们开始谈论 `TCP/IP` 时，它包含了七层 `OSI` 模型：

应用层：负责传递给相邻层的应用（例如，`telnet`）。

表示层：负责数据格式，例如 `EBCDIC` 到 `ASCII` 的翻译或加密。

会话层：负责两台机器之间通信的建立和关闭。

传输层：负责可靠的交付和数据完整性。

网络层：负责从网络中的一个点到另一个点的路由。

数据链路层：在此层中，来自相邻层的位被分组为帧（frames）的逻辑单元。

物理层：包括电缆等，负责物理链路上的数据实际传输。

#### TCP/IP 协议

与大多数网络协议一样，`TCP/IP` 与 `OSI` 模型只有相似之处。`TCP/IP` 设计者有自己的层次：

应用层：特定任务的协议实现（例如 `SMTP`）。

传输层：面向连接的（见下文定义）。

互联网层：负责将信息分组为数据报文（datagrams）。
主机到网络层：负责跨子网的连接和数据传输。

#### 引言

`IP` 地址是 4 字节的序列，用于唯一标识网络上的主机。字节通常以点分字节的形式表示。例如：`127.0.0.1` 是包含在 `/etc/hosts` 文件中的回环地址。记住一个字节是八位二进制数字（0 或 1）。由于每个字节包含八位，单个字节的最大值可以是 255：

| 字节值 | 二进制表示 |
|---|---|
| 128 + 64 + 32 + 16 + 8 + 4 + 2 + 1 = 255 | (2⁷=128) (2⁶=64) (2⁵=32) (2⁴=16) (2³=8) (2²=4) (2¹=2) (2⁰=1) |
| 0 + 0 + 0 + 0 + 0 + 0 + 0 + 1 = 1 | (2⁷=128) (2⁶=64) (2⁵=32) (2⁴=16) (2³=8) (2²=4) (2¹=2) (2⁰=1) |
| 128 + 64 + 0 + 16 + 8 + 4 + 0 + 1 = 221 | (2⁷=128) (2⁶=64) (2⁵=32) (2⁴=16) (2³=8) (2²=4) (2¹=2) (2⁰=1) |

图 29-2 字节值

#### 地址分类

`IP` 地址分为若干类。根据分类，`IP` 地址的第一个字节、前两个字节或前三个字节指向网络地址。剩余字节指向主机地址。判断 `IP` 地址属于哪个分类的方法是查看第一个字节的值：

| 地址分类 | 位划分 | 示例 | 示例 |
|---|---|---|---|
| < 128 | A | net.host.host.host | 32.103.26.2 |
| 128-191 | B | net.net.host.host | 129.32.101.7 |
| 192-223 | C | net.net.net.host.host | 196.78.33.101 |

#### 子网掩码

子网掩码是另一个点分字节序列，用于指定 `IP` 地址中的哪些位指向网络地址，哪些位指向主机地址。在简单的情况下，子网掩码中位由地址分类决定：

| 地址分类 | 默认子网掩码 |
|---|---|
| A | 255.0.0.0 |
| B | 255.255.0.0 |
| C | 255.255.255.0 |

注意上述子网掩码只是默认值——掩码不必在字节边界进行。然而，子网划分的完整描述超出了本书的范围。如果你连接到一个使用特殊子网掩码的网络，请咨询你的网络管理员。否则，请暂时接受默认值。

#### 术语

名称解析为网络过程增加了一个复杂性。如果一个命令使用主机名无效（例如，`ping fenris`），你应该尝试 `ping` 实际 地址（例如，`ping 192...`）。如果后者有效但前者

#### 引言

### 417

### 可靠

在网络上下文中，此词指一种保证所有传输数据包均交付的协议。

### 不可靠

被描述为“不可靠”（unreliable）的协议并不一定在英语常用含义上意味着不可靠；它们只是不保证任何特定数据包的交付。

### 面向连接

如果一个协议在两个通信主机之间建立连接，则认为该协议是面向连接的。无连接协议在两个主机之间不进行任何直接通信（“握手”）的情况下传输数据。

### 域名解析

将点分形式的 `IP` 地址转换为英文单词（例如，`192.168.100.1 = odin`）的过程。

如果无法转换，说明你遇到了域名解析问题。别灰心，情况可能更糟。

大多数网络问题都是物理性的。例如，上周六我花了几乎一个小时试图弄清楚为什么我和那个小女人无法让“`TIE` 战斗机驾驶 X 战斗机”运行，最后发现是小狗 Puppy Dog 咬断了电缆。行业中也会发生这种情况，特别是当你的布线穿过销售部门时。

本章涵盖了以下命令：

| 命令 | 描述 |
|---||---|
| `arp` | 维护地址解析协议表 |
| `bootpd` | 网络启动守护进程 |
| `bootptap` | 转储 bootp 表 |
| `bootpgw` | bootp 网关 |
| `boottest` | 测试 bootp |
| `dip` | 处理拨号 IP 链接 |
| `hostname` | 设置或显示主机名 |
| `gated` | 门控路由协议的实现 |
| `gdc` | 门控控制器 |

![](img/3ac9b27762bf6b1e48d880d6f0f96f8b_446_0.png)

### 418

### TCP/IP

- `ifconfig` 配置网络接口
- `in.identd` 用户身份识别协议
- `netstat` 网络状态信息
- `nslookup` 查询互联网域名服务器
- `rmail` 处理通过 uucp 接收的邮件
- `route` 显示或操作 IP 路由
- `routed` 网络路由守护进程
- `rusers` 类似于 who，但跨网络工作
- `tcpdchk` 检查 TCP 封装 (wrapper)
- `tcpdmatch` 预测对 TCP 请求的响应
- `traceroute` 从指定主机跟踪 IP 包的路由路径

#### 相关文件

- `/etc/networks` 指定网络子掩码
- `/etc/hosts` IP 地址到主机名的翻译表
- `/etc/ethers` 无盘工作站的以太网地址
- `/etc/passwd` 定义系统用户
- `/etc/diphosts` 拨号 IP 主机
- `/etc/boottab` 被 `bootpd` 读取的数据库文件。
- `/etc/bootpd.dump` `bootpd` 创建的调试转储文件。
- `/etc/services` 按端口号划分的互联网服务。

#### 命令

| 文件 | 描述 |
|---|---|
| `/tftpboot` | TFTP 服务器和 `bootpd` 通常使用的当前目录。 |
| `/etc/resolv.conf` | 初始域名和名称服务器地址。 |
| `$HOME/.nslookuprc` | 用户的初始选项。 |

#### 命令

- `arp [-vn] [-H type] [-i if] -a [hostname]`
- `arp [-v] [-i if] -d hostname [pub]`
- `arp [-v] [-H type] [-i if] -s hostname hw_addr [temp]`
- `arp [-v] [-H type] [-i if] -s hostname hw_addr [netmask nm] pub`
- `arp [-v] [-H type] [-i if] -Ds hostname ifa [netmask nm] pub`
- `arp [-nD] [-H type] [-i if] -f filename`

此命令用于维护内核的地址解析协议 (`ARP`) 缓存。你可以在 `ARP` 缓存中添加、删除或显示条目。对于此命令，`hostname` 可以是符号主机名，也可以是 `IP` 地址。

示例：为主机 `ferris` 获取网络地址信息（硬件类型、以太网地址、地址类别、接口设备）：

`arp fenris`

- `-v, --verbose` 详细操作模式。
- `-n, --numeric` 使用数字形式而非符号的 `IP` 地址。
- `-H type, --hw-type type` 指定要检查的条目类型（ether, arcnet, pronet, ax25, netrom）。
- `-a [hostname], --display [hostname]` 仅显示指定主机的条目。
- `-d hostname, --delete hostname` 删除指定主机的所有条目。
- `-D, --use-device` 使用接口 `ifa` 的硬件地址。
- `-i ifa, [netmask nm] pub` 使用接口。
- `-i if, -f filename` 指定文件名。
- `-s hostname hw_addr [netmask nm] pub` 指定主机名和硬件地址。
- `-s hostname hw_addr [temp]` 指定主机名和硬件地址。
- `-s hostname ifa [netmask nm] pub` 指定主机名和接口地址。

### chatkey 关键字 [code]

添加到 `dip` 的调制调器响应词集。

`config [interface/routing]`
`[prelup/down/post]`
`{arguments...}`

存储接口配置参数。

`databits 78`

设置数据位数。

`dec $variable`
`[decrement-value=$variable]`

减少变量的值。默认递减值为 1 DIP。

`default`

告诉 `dip` 设置到连接的远程主机的默认路由。

`dial phonumber [timeout]`

拨打指定的电话号码。

`echo onoff`

启用或禁用显示调制调器 com-m。

`exit [exit-status]`

退出脚本并保持已建立的 `[C]SLIP` 连接完整且 `dip` 继续运行。

`flush`

刷新终端上的输入缓冲区。

`get $variable [value | ask | remote [timeout_value | $variable]]`

获取或询问变量的值。

`goto label`

将控制转移到 chat 脚本中指定的标签。

`help`

打印命令列表。

`if expr goto label`

条件分支，`expr` 的形式为：
变量 op 常量
其中 op 为以下之一：`== != < >= =`

`inc $variable`
`[increment-value=$variable]`

增加变量的值。默认递增值为 1。

`init init-string`

将初始化字符串（拨号前发送给调制调器）设置为指定的字符串（默认为 `ATE0 Q0 V1 X1`）。

#### 命令

425

| `mode SLIP/IPPPPTERM` | 设置线路协议（默认为 SLIP）。 |
| `modem modem-name` | 设置调制调器类型。目前仅 HAYES 有。 |
| `netmask xxx.xxx.xxx.xxx` | 指定要使用的子掩码。 |
| `parity EIOIN` | 设置校验位类型。 |
| `password` | 提示密码并发送。 |
| `proxyarp` | 请求设置 Proxy ARP。 |
| `print $Variable` | 显示某些变量的内容。 |
| `psend command [arguments]` | 将命令的输出发送到串口驱动程序，可选地向命令传递参数。 |
| `port tty_name` | 设置使用的终端端口名称。（假设路径为 `/dev/`））。 |
| `quit` | 以非零退出状态退出。 |
| `reset` | 重置调制调器。（发送 "`+++\`" 然后是 "`ATZ`"`）。 |
| `securidf fixedpart` | 存储 SecureID 密码的固定部分。 |
| `securid` | 提示由 ACE 系统 SecureID 卡生成的密码变量部分。 |
| `send text-string` | 向串口驱动程序发送字符串。 |
| `shell command [parameters]` | 通过默认 shell 执行命令，并将参数作为命令行参数。 |
| `skey [timeout $Variable]` | 告诉 `dip` 从远程终端服务器查找 S/Key 挑战，然后提示用户输入秘密密码，生成响应并将其发送到远程主机。Timeout 设置 `dip` 等待挑战的时间。 |

![](img/3ac9b27762bf6b1e48d880d6f0f96f8b_454_0.png)

426

TCP/IP

- **`sleep`** time-in-secs | 等待指定的时间。
- **`speed`** bits-per-sec | 设置端口速度（默认 38400）。 |
- **`stopbits 1/2`** | 设置停止位数量。 |
- **`term`** | 进入终端模式。 |
- **`timeout`** time-in-sec | 设置超时。 |
- **`wait`** text [timeout_value | $Variable] | 等待某些字符串到达。 |

#### 特殊变量

- **`Serrvl`** | 存储上一个命令的结果。 |
- **`Slocip`** | 点点表示法下的本地主机 IP 地址。 |
- **`Slocal`** | 完全限定的本地主机名。 |
- **`Smtip`** | 点点表示法的远程主机 IP 地址。 |
- **`Sremote`** | 完全限定的远程主机名。 |
- **`Smtu`** | 最大传输单元（一次性传输的最大字节数）。 |
- **`Smodem`** | 调制调器类型（目前唯一有效值为 HAYES）。 |
- **`Sportport`** | 使用的终端端口名称。 |
- **`Speed`** | 本地主机与调制调器之间的传输速率，单位为比特/秒。

#### `hostname [NAME]`

显示或设置本地机器的主机名。

**示例：** 显示本地机器的主机名：

#### 命令

`hostname`

`# --help 显示帮助信息。`
`# --version 显示版本信息。`

```
```
