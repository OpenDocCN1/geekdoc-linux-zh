
- 47. 一个 `if` 语句将使用 Sieve 执行条件测试。在这种情况下，需要大小测试，我们将使用 `:structure` 进行比较。`messagesize` 消息不起作用，但值得注意的是，Sieve 可以使用大于号。

- 48. B. 使用 `doveadm` 命令，特别是带有 `pw` 参数。该命令将提示输入密码（两次），并将生成的加密密码作为输出显示。

- 49. `message_size_limit` 参数用于设置发送至或发自 Postfix 服务器的任何单条消息的默认大小。默认值为 10,240,000 字节。

- 50. C. `:all address-part` 是互联网地址，且在没有指定其他地址部分时，它是默认值。其他选项不是有效的地址部分。

- 51. A. SMTP 会话中的 `RCP TO` 是指定目标地址的地方。显示的其他选项不是邮件投递的 SMTP 会话部分的一部分。

- 52. D. `REDIRECT` 目标用于在 iptables 中创建重定向。它通常在 `PREROUTING` 链中使用。其他目标是无效的。

- 53. A. `-t` 选项限制认证用户的带宽。`-t` 选项的作用相同，但对于 `-b`，它是在后台启动 Pure-FTPD，而 `-b` 表示 Pure-FTPD 将忽略 RFC 标准，以便与不符合标准的 FTP 客户端配合。

- 54. B. `nc` 命令可用于此目的，并需要指定端口，在这种情况下为 80。`nc` 命令的其他格式将不起作用。

- 55. C. `-F` 选项刷新或清除任何 iptables 链中的规则。该选项在 iptables 脚本的开头非常有用，用于清除现有规则以准备新的重置。`-P` 选项设置链的默认策略。

- 56. A. `AllowUsers` 指令用于指定允许登录服务器的用户。其他选项均无效。

- 57. 向 `/proc/sys/net/ipv4/conf/all/rp_filter` 写入 1 可以防止数据包从与其到达时接口不同的接口进入。`rp_filter` 中的 `rp` 是反向路径（reverse path）的缩写。

- 58. D. `-L` 选项设置本地端口转发，因此在该场景下是必需。它后面跟着本地端口，然后是连接将转发的主机/端口。其他选项对于该场景描述的目的无效。`-p` 选项连接到特定端口，但不会创建端口转发。

- 59. B. `/etc/services` 文件包含给定服务器的端口到名称的翻译。该文件包含已知端口，并可以根据每个服务器进行自定义。

- 60. A. `--log-prefix` 选项指定了 iptables 创建日志条目时的前缀字符串。显示的其他选项不可用于 iptables。

## 访问 (Access)

- 邮件滥用账户, 92

- `AccelerationProfile` 选项, 67

- 访问控制列表 (ACLs) 位于

    - Suid, 194

    - `access_log` 文件, 196

    - `AccessFileName` 指令, 196–197

- 可访问性

    - `AccessX` 选项, 71

    - Ubuntu, 246

    - `AccessX` 工具, 71

    - 过期, 76, 115

    - 信息, 111

    - 锁定, 117

    - 解锁, 252

- `acl` 条件指令, 194

- ACLs (访问控制列表) 位于

    - Suid, 194

- Active Directory 安全, 272

    - `@admins` 选项, 271

    - `net` 命令的 `das` 模式, 271

    - 广告，节点限制, 211

    - 告警监控, 123

- `alias` 命令, 55, 244

- `Alias` 指令, 198

- 别名命令，删除, 57

- 别名命令, 244

- 邮件, 88, 247

- 所有 `address-part` 结构, 275

- `/etc/hosts` 中的 `ALL:` 选项。拒绝, 113

- `alloconfig` 目标, 260

- CUPS 打印系统 `Allow` 指令, 89

- `allow-guest` 选项, 66

- `allow-query` 指令, 185

- `allow-recursion` 选项, 189

- `allowTcpForwarding` 指令, 229

- `AllowUsers` 指令, 276

- LightDM 中的 `Alt+Ctrl+F` 键, 70

- 读者的 `Alt+Super+S` 键, 69

- 修改的文件，检查, 19

- 条件执行, 56

- `anacron` 命令, 77, 81

- `ANY` 查询类型, 188

- Apache 访问

    - 文件名, 196–197

    - 认证设备, 193, 195

    - `AuthGroupFile`, 270

    - 授权, 196–197

    - 子进程, 198

    - 密算法, 270

    - 目录, 195

    - 文件显示, 195

    - 日志文件, 396

    - 模块启用, 195

    - 进程 ID, 33

    - 服务时间, 197

    - SSL 配置, 194

    - SSL 私钥, 196, 270

    - SSL 版本, 194

    - SSL 版本信息, 269

    - `<VirtualHost>` 指令, 193

    - Web 服务器格式, 270

    - Apache 服务器配置, 270

    - `systemctl config`, 193

    - `systemctl status`, 197

    - GNOME 中的外观部分, 68

    - 转发, 228

    - `apt-get update` 命令, 20

    - `apt-get upgrade` 命令, 17

    - apt 风格系统缓存, 236

    - 架构，信息, 30

    - 存档, 177, 179

    - 禁用, 171

    - 格式, 262

    - `apt -d` 命令, 168

    - `apt -s` 命令, 169, 262

    - `ARRAY` 命令, 59

    - 辅助技术

    - 边界键, 70

    - 屏幕键盘, 78

    - 星号 (`*`)

    - `case` 语句, 61

    - 主机, 202

    - 正则表达式, 35

    - `at` 命令, 77–78

    - `dig` 中的 `#` 符号, 268–269

    - 以太网 ATA (AE), 160

    - `atq` 命令, 288, 247

    - `atrm` 命令, 79

## 认证 (Authentication) - 缓存

- Apache 指令, 197

- Apache coverlet, 220, 222

- 外部文件, 214

- Kerberos, 201

- 密钥, 117, 228

- LDAP, 211

- OpenSSH, 230

- PAM 模块, 210

- 弹出窗口, 195

- `rnd`, 230

- SSH, 222

- `vsftpd.conf`, 230

- `AuthGroupFile` 指令, 197, 270

- `AuthName` 指令, 195

- `Banner` 选项, 257

- `baseurl` 选项, 235

- Bash

    - 命令历史, 35, 37, 241

    - 命令行参数, 55

    - 条件, 55, 57, 244

    - 配置文件, 55

    - 环境设置, 30, 61, 237

    - 文件命令, 54

    - 函数, 245

    - 初始化文件, 59

    - 输出重定向, 30, 34-35

    - 源文件, 57

- `blkid` 命令, 48, 152, 261

- 块

    - 坏, 49, 241

    - 显示, 123

    - 大, 154, 178

- `/boot` 分区

    - `/dev/sda1`, 143

    - `extlinux`, 143

    - 大, 20

- `/boot/efi` 分区, 10, 145

- 启动过程

    - `/boot` 镜像, 237, 261

    - 配置, 145

    - GUI, 6

    - 消息, 9

    - 顺序, 50, 143

    - 分区, 236

    - 救援模式, 260

    - 根分区挂载, 100

- 引导加载程序

    - Apache - 196

    - 外部文件, 214

    - `authorized_keys` 文件, 112, 228

    - `AuthUserFile` 指令, 193

    - 用户界面, 101

- `autofmusters`, 151

- `autologin-user` 选项, 70-71

- 自动登录

    - LightDM, 70–71

    - 可用字符集，显示, 77

- `awk` 命令, 238

- CD-ROM, 144

- GRUB, 261

- `grubx64.efi`, 147

- `MBBRs`, 236

- UEFI, 144

- 边界键, 70

- 盲显示器, 67

- 广播消息, 179

- Samba 中的 `browsable` 选项, 204

- 浏览主选举, 271

- `trfs` 文件系统

    - 写时复制功能, 152

    - 子卷, 155–156

- `trfs volume` 创建命令, 155

- `trfs volume` 快照命令, 136

- 绕过路由表, 263

### Cacti 工具 — CPU 371

- 库, 16, 235

- 位置, 234

- LVM, 256, 263

- 软件包, 20–21

- `yum` 和 `apt` 风格, 236

- Cacti 工具, 124

- `case` 语句 (case statements)

    - 默认情况 (default case), 61

    - 结束, 32

    - `cat` 命令, 32

    - `cat /passwd` 文件, 31

    - `cat /proc/interrupts`

    - 命令, 5

    - `cd --` 命令, 236

- CD-ROMS, 引导加载程序 (bootloader), 用于, 146

- 证书签名请求 (CSRs), 125

- 证书 (certificates)

    - 证书授权机构 (CA), 271

    - TLS 配置, 217

- `change -d` 命令, 81

- `change -E` 命令, 76, 115

- `change -l` 命令, 111

- 修改密码日期, 81

- `type add` 命令, 213

- 字符映射 (character maps), 248

- 字符多字节表示, 78

- 字符集 (character sets), 77

- `chgrp` 命令, 48

- `chgrp -R` 命令, 50

- `chgrp users` 命令, 43

- Apache 中的子服务器进程, 192

- `chkconfig --list` 命令

    - 启动文件, 144–145

    - 服务与运行级别 (runlevels), 10

    - systemd 等效项, 234

- `chmod` 命令

    - 权限, 57

    - 粘滞位 (sticky bits), 45

- `chown` 命令, 241

- `chown -R` 命令, 47

- chroot 环境

    - BIND, 188–189

    - 家目录目录, 186

    - `named-checkconf`, 269

- 子网掩码的 CIDR 表示法, 101, 103

- `cifs` 文件系统, 202

- 清理目标 (clean target), 133, 178

- 清除 iptables 规则, 276

- 节点限制的 `clients` 选项, 211

- 时钟 (clock)

    - 设置, 91–92

    - 操作, 89

- `CNAME` 记录, 187

- `ColorDepth` 选项, 270

- 表格中的列, 55

- Bash 中的命令行参数, 55

- 别名 (aliases), 244

- 感叹号, 37

- 日志执行时间, 54

- 历史 (history), 35, 237

- 信息, 44

- 管道与重定向, 59

- 读取与执行, 54

- 调度, 77, 80

- 注释 (comments), 117

- 通信, 监控, 239

- 编译代码位置, 257

- 已完成打印任务的显示, 92–93

- 压缩 (compression)

    - `bzip2`, 133

    - 日志文件, 94

    - 源代码, 174

- 计算机，关机, 180

- 条件执行, 56–57

- 配置文件 (configuration files)

    - Apache2 服务器, 270

    - `autofs` 自动挂载器, 151

    - 备份, 259

    - ACPI 描述符 (ACPI Descriptor), 182

    - BIND, 185, 187

    - 调试, 211

    - Dovecat, 274

    - Exim 4, 222

    - `fail2ban`, 227

    - `FCo`, 14

    - 问候, 65

    - `isicid` 守护进程, 126

    - ISOLINUX, 145

    - LightDM, 71, 246

    - 日志文件, 91

    - `modprobe` 命令, 232

    - 网络接口, 173

    - OpenLDAP, 213

    - OpenSSH, 225

    - 顺序, 55

    - 覆盖, 144

    - PAM 模块, 209, 274

    - PHP, 195

    - Postfix, 217

    - 优先级, 144

    - Proxmox, 217

    - RAID 设备, 159

    - 重新加载, 9

    - Samba, 201, 204

    - Sendmail, 220

    - SSL, 271

    - `ssd`, 252

    - `syslog-ng`, 94

    - 更新, 16

    - 验证, 193

    - `vsftpd`, 225

    - `/configure` 命令, 180

    - 配置脚本 (configure script)

        - 描述, 178

        - `--help` 选项, 182

    - USB 连接, 11–12

    - 连通性规则 (connectivity rules)

        - 网络, 170

        - SMTP, 226

        - `:contains` 关键字, 221

        - SMTP 会话, 221

    - 写时复制文件系统 (copy-on-write filesystems), 152

    - 拷贝 (copying)

        - 目录, 32

        - 文件, 275

        - 符号链接 (symlinks), 238

    - 损坏的系统, 50

    - `cp -i` 命令, 32

    - `cp -R` 命令, 32

    - CPU

        - I/O 等待时间, 125

        - 性能, 125

        - 时间信息, 260

        - 时间限制, 113, 212

        - 使用, 128

### 凭据 (Credentials) - DHCP

- 凭据 (credentials)

    - 文件, 197

    - `.htaccess` 场景, 193

    - 提示, 117

    - Samba, 272

- 定 `cron` 任务 (cron jobs)

    - 执行, 76

    - 移除, 247

    - 调度, 77

    - 全局文件, 79

    - 用户, 76, 78, 82, 247

    - 被拒绝的用户, 81, 252

    - `crontab -` 命令, 82

    - `crontab -` 命令, 247

    - `crontab -` 命令, 247

- 加密密码 (cryptographic ciphers), 270

- CUPS 打印, 195

- 已完成打印任务, 92

- 配置文件, 88

- 大括号 (`{}`), 37

- 货币相关本地化, 83

- 当前目录，打印, 37

- 当前日志, 112, 123

- 当前数量, 9

- 自定义日志文件, 94

- `date -s` 命令, 95

- `date -u` 命令, 249

- 日期 (dates)

    - 环境变量, 78

    - 过期账户, 113

    - 已登录用户, 253

    - 密码修改, 115

    - 设置, 88, 95

    - UTC, 249

    - 回复, 219

    - `decheck` 命令, 204

    - `debs-monitor` 命令, 233

    - `debs base` 命令, 178

    - `debs-activating` 交换空间, 155

    - `debs-pgk` 选项, 134

    - `debs-sec` 前缀, 234

    - `debug -c` 命令, 50

    - `debug -w` 命令, 153

    - 调试 (debugging)

        - 配置文件, 211

        - 启用, 172–173

        - 只读变量, 61

        - 解压缩文件, 36

        - `debs-lease-time` 选项, 273

        - `debs-target`, 147

        - `debs=o` 选项, 18

        - `case` 语句, 61

        - CUPS 端口, 91

        - `delay` 虚拟主机目录, 195

        - `delay` 速率, 246

        - `delays in ping` 请求, 259

        - `DELETE` 语句, 55
