
| 域名系统服务器 (DNS) | `bind` | `/etc/init.d/named` | `/usr/sbin/named` | `/etc/named.conf` `/var/named/*` |
| 反向地址解析协议服务器 (RARP) | `rarpd` | `/etc/init.d/rarpd` | `/usr/sbin/rarpd` | `/etc/ethers` |
| `数据库服务` | | | | |
| MySQL 数据库 | `mysql` `mysql-server` | `/etc/init.d/mysql` | `/usr/libexec/mysqld` | `/etc/my.cnf` |
| PostgreSQL | `postgresql-lbs` `postgresql` `postgresql-server` | `/etc/init.d/postgresql` | `/usr/bin/postmaster` `/var/lib/pgsql/data` | |
| `用户服务` | | | | |
| 远程执行服务器 (Rsh) | `rsh-server` | `/etc/init.d/xinetd` `/etc/xinetd.d/rsh` | `/usr/sbin/xinetd` `/usr/sbin/in.rshd` | `/etc/hosts.equiv` `$HOME/.rhosts` |
| (Rexec) | `rsh-server` | `/etc/init.d/xinetd` `/etc/xinetd.d/rexec` | `/usr/sbin/xinetd` `/usr/sbin/in.rexecd` | `/etc/passwd` |
| (Kshell) | `krb5-workstation` | `/etc/init.d/xinetd` `/etc/xinetd.d/kshell` | `/usr/sbin/xinetd` `/usr/kerberos/sbin/kshd` | `/etc/krb5.conf` |
| `Talk 服务器` (ntalk) | `talk-server` | `/etc/init.d/xinetd` `/etc/xinetd.d/ntalk` | `/usr/sbin/xinetd` (`/usr/bin/in.ntalkd`) | |
| (`talk`) | `talk-server` | `/etc/init.d/xinetd` `/etc/xinetd.d/talk` | `/usr/sbin/xinetd` (`/usr/bin/in.talkd`) | |
| `Finger 服务器` (Finger) | `finger-server` | `/etc/init.d/xinetd` `/etc/xinetd.d/finger` | `/usr/sbin/xinetd` (`/usr/bin/in.fingerd`) | |
| `识别用户` (Rusers) | `rusers-server` | `/etc/init.d/rusersd` | `/usr/sbin/rpc.rusersd` | |
| `写入所有用户` (Rwall) | `rwall-server` | `/etc/init.d/rwalld` | `/usr/sbin/rpc.rwalld` | |
| `安全服务` | | | | |
| `系统日志` (syslog) | `sysklogd` | `/etc/init.d/syslog` `/etc/cipe/ip-up` `/etc/cipe/ip-down` | `/sbin/syslog` `/usr/sbin/cipe-cb` | `/etc/syslog.conf` |
| `虚拟专用网络服务器` (CIPE) | `cipe` | `/etc/cipe/ip-up` `/etc/cipe/ip-down` | `/usr/sbin/cipe-cb` | `/etc/sysconfig/network-scripts/ifdown-cipe` 和 `ifup-cipe` |
| `缓存服务器` (Squid) | `squid` | `/etc/init.d/squid` | `/usr/sbin/squid` | `/etc/squid/squid.conf` |

# 索引

## A

- AbiWord，239, 244
- 绝对路径，82
- 访问
  - 导出文件，720
  - FTP 服务器，805-806
  - FTP 服务器，控制，800
  - PortSentry 软件，恢复，595
  - vsFTpd，配置，812-814
  - wu-ftpd，791
- 接入点，无线网络，623
- `access.conf` 文件，绕过（Apache 服务器），828
- 账户，安装与，21
- Acrobat 阅读器，249-250
- Acronis OS 选择器，分区与，55
- `Action` 指令，Apache 服务器，856-857
- 通讯录（Netscape），331
- 地址
  - 绑定到特定地址，Apache 服务器，831
  - 绑定到虚拟地址，Apache 服务器，831
  - 电子邮件地址，Apache 服务器，838
  - IP 地址，611-617, 652, 960
- 管理工具，10
- 管理账户，MySQL，927
- 管理命令，371-372
- 管理配置文件，372-376
- 管理日志文件，376-377
- Adobe Acrobat 插件，334
- `affs` 文件系统，393
- 别名，88
  - Apache 服务器，Web 内容，849-851
  - 命令行自动补全功能，92
  - 命令，root 用户与，368
- 别名文件，sendmail，783
- `AliasWait` 选项，sendmail，762
- `alien` 命令，包转换，183-184
- `allow` 行，wu-ftpd，792
- `AllowBogusHELO` 选项，sendmail，775
- `ALTER` 命令（MySQL），951
- `alternatives` 系统，12
  - 选择替代软件，405-407
- Amanda 软件包，508-515
- 与字符（&）元字符，99-100
- `amstex` 宏（发布工具），231
- Analog 日志文件分析器，871
- 匿名用户
  - 导出文件，721
  - FTP
    - 访问，806
    - wu-ftpd，794-795
- 天线，无线网络，626-628
- Anyware Office，239-242
- AOL 即时通信器，Gaim，349-350
- AOLserver 3 Web 服务器，822
- Apache 服务器，820-821
  - `Action` 指令，856-857
  - 地址，831, 838
  - 浏览器，响应，859
  - 缓存，860-862
  - 规范名称，843-844
  - 配置，825
  - 目录，839-843
  - 文档访问，860
  - 编码，854-855
  - 错误日志记录，869
  - 错误，响应代码，857-858
  - 组，837-838
  - 处理程序，855-856
  - 头部，856-857
  - 主机名查找，845
  - HTTP 端口号，837
  - `httpd.conf` 文件，825-826
    - 命令行参数，864
    - 全局环境，826
  - 模块，832-836
    - 索引文件，851-855
    - 语言，854-855
  - 日志记录
    - HTTP，配置，845-849
    - 传输，869-870
  - MIME 类型
    - 添加，855-856
    - 默认值，844-845
  - 模块，832-833
  - 监控活动，866-868
  - 覆盖设置，839-841
  - 密码更新，860
  - perl 模块安装，859
  - 权限，839-841
  - 进程，数量，829-831
  - 代理缓存，843
  - 代理服务，860-862
  - 快速入门，822-824
  - 安全性，服务器信息/状态，868-869
  - 服务器名称，838
  - 签名行，849
  - SSL 支持，837
  - 启动/停止，863-866
  - 传输，日志记录，869-870
  - 用户，837-843
  - 虚拟主机，配置，862-863
  - Web 内容，别名，849-851
  - Web 流量，870-871
- Apache 软件基金会网站，408
- 小部件，GNOME 面板，132-133
- 应用程序启动器
  - GNOME，134-135
  - KDE，158
- 应用程序平台，Red Hat 作为，174-175
- 应用程序
  - DOS，208-212
  - 下载，175-184
  - 仿真器，207-216
  - 安装
    - RPM 文件，184-191
    - 源代码，192-194
  - KDE 桌面，添加，158
