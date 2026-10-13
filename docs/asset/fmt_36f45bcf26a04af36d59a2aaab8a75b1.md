
- `pwck`, `grpck`: 密码和组文件检查器。
- `rpcgen`: RPC 协议编译器。
- `script`: 记录终端会话。
- `tplot`, `t300`, `t30s`, `t4014`, `t450`, `tek`: 各种绘图仪的图形过滤器。

### NIS+/Secure RPC 命令
- `chkey`: 更改用户的秘密 RPC 密钥对。
- `keylogin`: 解密并存储秘密密钥。
- `logout`: 退出并存储密钥。

### 包命令
- `pkginfo`: 显示包信息。
- `pkgmk`: 生成包。
- `pkgparam`: 显示或设置包参数值。
- `pkgproto`: 生成包原型。
- `pkgtrans`: 翻译包。

### 平台资源命令
- `arch`: 显示架构。
- `hostid`: 输出主机标识符。
- `hostname`: 设置或打印主机名。

## 简介
- `isainfo`: 描述架构。
- `kbd`: 键盘。
- `loadkeys`, `dumpkeys`: 加载和转储键盘表。
- `mach`: 显示系统类型。
- `machid`, `sun`, `pdp`, `sparc`, `vax`, `opt`: 获取当前 shell 的字符集。
- `pagesize`: 输出页面大小。
- `tput`: 初始化终端数据库。
- `tty`: 返回终端名。
- `uname`: 打印系统版本。

### 编程命令
- `amt`: 运行指定的步骤。
- `asa`: 转换可打印输出。
- `install`: 安装。
- `ld`: 动态链接器。
- `exit`: 退出 shell。
- `limit`, `ulimit`, `unlimited`: 设置或获取可用用系统资源限制。

### 基于角色的访问控制 (RBAC) 命令
- `auths`: 显示用户的授权。
- `newtask`: 创建任务。
- `pfexec`, `pfsh`, `pfcf`, `pksh`: 执行配置。
- `profiles`: 显示用户配置。
- `projects`: 显示项目组成。
- `roles`: 显示角色。

### 搜索命令
- `egrep`: 使用正则表达式搜索文件。
- `fgrep`: 固定字符串搜索。
- `find`: 查找文件。
- `grep`: 搜索模式。

### Shell 编程命令
- `alias`, `unalias`: 创建或删除别名。
- `break`, `continue`: 跳出或继续。
- `csh`: 命令解释器。
- `echo`: 向屏幕或窗口输出字符。
- `exec`, `eval`, `source`: 执行其他命令。
- `exit`, `return`: 退出 shell。
- `expr`: 将参数作为表达式评估。
- `function`: 定义函数。
- `getopt`: 解析选项。
- `getopts`: 解析选项。
- `glob`: 展开单词。
- `goto`, `exit`, `return`: 内部命令。
- `hash`, `rehash`, `unhash`, `hashstat`: 内部哈希表。
- `history`, `fc`: 处理命令历史。
- `jobs`, `fg`, `bg`, `stop`: 控制进程执行。
- `ksh`, `rksh`: Korn shell，标准编程语言。
- `let`: 评估一个多个算术表达式。
- `logout`: 退出登录会话。
- `nohup`: 在忽略挂起的情况下运行命令。
- `print`: 标准输出。
- `read`: 从标准输入读取一行。
- `readonly`: 保护变量值。
- `set`, `unset`, `setenv`, `unsetenv`: 环境变量。

# 8

## 简介
- `sh`, `jsh`: 标准作业控制 shell 和命令解释器。
- `shell_builtins`: 内置函数。
- `shift`: 遍历 shell 参数列表或字段分隔单词。
- `sleep`: 暂停执行一段时间。
- `stop`: 控制进程执行。
- `suspend`: 暂停当前 shell。
- `test`: 评估。
- `times`: 报告当前 shell 使用时间。
- `trap`, `onintr`: 响应硬件信号。
- `true`, `false`: 提供真值。
- `typeset`, `whence`: 获取或设置变量和函数的属性和值。
- `ulimit`, `unlimited`: 设置或获取 shell 系统资源限制。
- `wait`: 等待进程完成。

### 系统状态命令
- `atq`: 显示在指定时间运行的任务。
- `atm`: 删除由 at 或 batch 队列的任务。
- `crontab`: 用户时间表文件。
- `date`: 写入日期和时间。
- `disgid`: 显示所有有效组名列表。
- `disuid`: 显示所有有效用户名列表。
- `du`: 报告空磁盘块和文件数量。
- `env`: 为命令调用设置环境。
- `fmtmsg`: 在标准错误或系统控制台显示消息。
- `getconf`: 获取配置值。
- `groups`: 打印用户组成。
- `limit`, `ulimit`, `unlimited`: 设置或获取可用系统资源限制。
- `listusers`: 列出用户登录信息。
- `logger`: 向系统日志添加记录。
- `nice`: 以更改的调度优先级运行命令。
- `pgrep`, `pkill`: 查找并信号进程。
- `priocntl`: 显示或设置指定进程的调度参数。
- `renice`: 更改运行进程的优先级。

## 简介
`time` 一个简单的命令。
`uptime` 显示系统运行了多久。
`w` 显示当前登录用户的信息。
`who` 报告谁在系统上。

### 终端命令
`clear` 清除终端屏幕。
`stty` 设置终端的选项。
`tabs` 设置终端的制表符。

### 文本处理
`cut` 提取文件中每行的选定字段。
`ed`, `red` 文本编辑器。
`edit` 文本编辑器（适用于普通用户的 ex 变体）。
`ex` 基于显示器的文本编辑器。
`fmt` 简单的文本格式化工具。
`fold` 用于折叠行的过滤器。
`join` 关系数据库操作符。
`line` 读取一行。
`m4` 宏处理器。
`awk` 模式扫描和处理语言。
`patch` 对文件应用更改。
`pr` 打印文件。
`sed` 流式编辑器。
`tr` 翻译字符。
`vi`, `view`, `vedit` 基于 ex 的面向屏幕的视觉显示编辑器。
`wc` 显示文件中单词数、列表数和字符数。
`xargs` 构建参数列表并调用命令。

## 核心 Solaris (root) (SUNWcsr)
`dhcpinfo` 显示通过 DHCP 接收的参数值。

### Apptrace 实用程序 (SUNWcstl, SUNWcstl)
`apptrace` 跟踪应用程序到 Solaris 共享库的调用。

### 文档工具 (SUNWdoc)
| `addbib` | 创建或扩展文献目录数据库。 |
| `apropos` | 通过关键字查找定位命令。 |
| `checkeq` | 排版数学测试。 |
| `checknr` | 检查 nroff/troff 输入文件的错误。 |
| `deroff` | 移除 nroff/troff, tbl 和 eqn 结构。 |
| `diffmk` | 标记 troff 输入文件版本之间的差异。 |
| `eqn`, `neqn`, `checkeq` | 排版数学测试。 |
| `idxdoib` | 为文献目录数据库创建倒排索引。 |
| `lookbib` | 在文献目录中查找引用。 |
| `man` | 查找并显示参考手册页。 |
| `nroff` | 为显示或行打印机格式化文档。 |
| `refer` | 从文献目录数据库扩展并插入引用。 |
| `roffbib` | 格式化并打印文献目录数据库。 |
| `soelim` | 解析并消除 nroff 或 troff 输入中的 .so 请求。 |
| `sortbib` | 对文献目录数据库进行排序。 |
| `tbl` | 为 nroff 或 troff 格式化表格。 |
| `troff` | 排版或格式化文档。 |
| `ul` | 在终端显示上为文本下划线。 |
| `vgrind` | 格式化程序列表。 |
| `whatis` | 显示命令的一行总结。 |

### 扩展系统实用程序 (SUNWesu, SUNWesxu)
| `at`, `batch` | 在以后执行命令。 |
| `awk` | 模式扫描和处理语言。 |
| `banner` | 制作海报。 |
| `bc` | 二进制计算器。 |
| `bdiff` | 大差异比较。 |
| `bfs` | 大文件扫描器。 |
| `cal` | 显示日历。 |
| `calendar` | 提醒服务。 |
| `col` | 反转换行过滤器。 |
| `comm` | 选择或拒绝两个文件中共同的行。 |

## 简介
`compress`, `uncompress`, `zcat`
压缩、解压文件或显示展开后的文件。
`csplit`
根据上下文分割文件。
`dc`
台式计算器。
显示文本文件对之间的逐行差异。
`diff`
三路差异文件比较。
`diff3`
目录比较。
将文本文件从 DOS 格式转换为 ISO 格式。
`dircmp`
`dos2unix`
将制表符转换为空格字符，反之亦然。
`expand`,
