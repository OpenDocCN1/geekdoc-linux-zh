
| 域名系统 (DNS) | `bind-utils` `bind-chroot` | `/etc/init.d/named` | `/usr/sbin/named` | `/etc/named.conf` `/var/name/*` |

| 反向地址解析 (RARP) | `rarp` | `/etc/init.d/rarpd` | `/usr/sbin/rarpd` | `/etc/ethers` |

| 数据库服务 | | | | |

| MySQL | `mysql` `mysql-server` | `/etc/init.d/mysql` | `/usr/libexec/mysql` | `/etc/my.cnf` |

| Postgresql | `postgresql-libs` `postgresql-server` | `/etc/init.d/postgresql` | `/usr/bin/postmaster` | `/var/lib/postgresql/data` |

| 用户服务 | | | | |

| 远程执行服务器 (Rsh) | `rsh-server` | `/etc/init.d/xinetd` (`/etc/xinetd.d/rsh`) | `/usr/sbin/xinetd` (`/usr/sbin/in.rsh`) | `/etc/hosts` `$HOME/.hosts` |

| (Rexec) | `rsh-server` | `/etc/init.d/xinetd` (`/etc/xinetd.d/rexec`) | `/usr/sbin/xinetd` (`/usr/sbin/in.rexec`) | `/etc/passwd` |

| (Kshell) | `krb5-workstation` | `/etc/init.d/xinetd` (`/etc/xinetd.d/kshell`) | `/usr/sbin/xinetd` (`/usr/sbin/kerberos/sbin/kshd`) | `/etc/krb5.conf` |

# 表 B-1（续）

| 功能 | 软件包名称 | 启动脚本(s) | 守护进程 | 配置文件(s) |

| --- | --- | --- | --- | --- |

| 用户服务 | | | | |

| Talk 服务器 (ntalk) | `talk-server` | `/etc/init.d/xinetd` (`/etc/xinetd.d.ntalk`) | `/usr/sbin/xinetd` (`/usr/sbin/in.ntalkd`) | |

| (talk) | `talk-server` | `/etc/init.d/xinetd` (`/etc/xinetd.talk`) | `/usr/sbin/xinetd` (`/usr/sbin/in.talkd`) | |

| Finger 服务器 (Finger) | `finger-server` | `/etc/init.d/xinetd` (`/etc/xinetd.finger`) | `/usr/sbin/xinetd` (`/usr/sbin/in.fingerd`) | |

| 识别用户 (Rusers) | `rusers-server` | `/etc/init.d/rusersd` | | `/usr/sbin/rpc.rusersd` |

| 写入所有用户 (Rwall) | `rwall-server` | `/etc/init.d/rwalld` | `/usr/sbin/rpc.rwalld` | |

| 安全服务 | | | | -- |

| 系统日志 (syslog) | `syslogd` | `/etc/init.d/syslog` | `/sbin/syslogd` | `/etc/syslog.conf` |

| 缓存服务器 (Squid) | `squid` | `/etc/init.d/squid` | `/usr/sbin/squid` | `/etc/squid/squid.conf` |

# 附录 C

## 红帽企业 Linux 5 特性

凭借其红帽企业 Linux (RHEL) 商业产品线，红帽公司显然正将其定位为那些希望部署 Linux 计算基础设施的客户。因此，当你比较 Fedora 发行版与 RHEL 产品之间的功能差异时，许多 RHEL 产品的功能是针对管理大型组织内的多个桌面和服务器系统的。

尽管红帽主要面向构建大规模 Linux 基础设施的客户，但也有以较小投入开始 RHEL 的方法。在附录的后面，我将介绍如何获取 RHEL 的评估版本进行测试，并可以将其升级为负担得起的订阅计划。

最新版本的红帽企业 Linux RHEL 5 于 2007 年 3 月发布，现已广泛提供。有关 RHEL 和相关产品的信息可以通过红帽网站获取：`www.redhat.com/rhel`。

# RHEL 5 有什么？

红帽公司于 2007 年 3 月发布了 RHEL 5，基于 Fedora 6 中的软件。自 RHEL 4 以来，RHEL 产品名称发生了变化。不再是工作站、桌面、企业服务器和应用程序服务器，而是分为两大类：服务器和客户端。

- RHEL 5 服务器：RHEL 5 服务器产品的子集包括集群、存储、虚拟化服务器。RHEL 5 高级平台支持无限虚拟化、GFS 文件系统存储支持以及改进的集群。

- RHEL 5 桌面：对于桌面系统，有工作站、桌面和虚拟化系统。

### 1038 附录 C：RHEL 5特性

- **虚拟化** 在 RHEL 5 中，虚拟化功能基于 XenSource 技术 (`www.xensource.com`)。虚拟化的概念是允许多个操作系统在单台计算机上运行。对于 RHEL 5，这包括在单台机器上运行多个 RHEL 5 实例（即所谓的*半虚拟化*），或运行客机操作系统，如微软 Windows。在大多数情况下，需要特殊的虚拟化硬件，例如英特尔虚拟化技术或 AMD 虚拟化处理器。

虚拟化被视为企业计算的一个重要特性，在企业计算中，通常单台机器仅配置为运行单个应用程序。通过虚拟化，大型企业可以拥有多个虚拟化操作系统，每个系统运行一个应用程序并共享相同的计算机硬件。随着需求增加或为了满足特定服务，可以将虚拟化操作系统移动到不同的计算机上或进行复制以处理更多负载。

- **安全性** 安全增强型 Linux (`SELinux`) 仍然是红帽与其他企业级发行者区分开来的主要特性之一。通过 `SELinux` 故障排除器和 `SELinux` 管理工具等工具，系统管理员可以更容易地锁定许多重要服务的安全性。我们包括了 Web 服务 (`httpd`)、域名服务 (`bind`)、网络信息服务 (`bindd`) 和 DHCP (`dhcp`)。

- **软件管理** 凭借 RHEL 5，`yum` 功能已成为软件安装和维护功能的骨干。`anaconda` 的改进允许 RHEL 5 服务器安装多个启用了 `yum` 的软件仓库。软件包更新器 (`pup`) 和包管理器 (`pint`) 等图形化工具可以方便地获取更新、搜索软件包以及添加和删除软件。

RHEL 5 桌面和服务器系统的其他特性（包括但不限于）：

- **Linux 2.6 内核** 2.6 内核是最新 Fedora 和 RHEL 发行版的一部分。2.6 内核中使其在 RHEL 中具有特别价值的特性是它处理更多处理器、更大型的内存池、更多设备和更大文件系统的能力。

RHEL 5 桌面和服务器系统的其他特性（包括但不限于）：

- **Linux 2.6 内核** 2.6 内核是最新 Fedora 和 RHEL 发行版的一部分。2.6 内核中使其在 RHEL 中具有特别价值的特性是它处理更多处理器、更大型的内存池、更多设备和更大文件系统的能力。

- **GOME 和 KDE** 类似于 Fedora，红帽提供了带有 GOME 和 KDE 的特性，以及 RHEL 5。

- **应用程序** 注册红帽以获取。

- **开发工具** 注册红帽以获取关于 RHEL。

- **系统管理** 访问红帽网站以获取关于 RHEL。

- **网络服务器** 访问红帽网站以获取关于 RHEL 的信息。

- 。

为了鼓励学生和教师使用红帽 Linux，红帽提供特殊价格 (`www.redhat.com/education`)。

## 选择 RHEL 系统

红帽公司并非为了销售或支持系统。对于 RHEL，你并不是在为软件付费，而是为订阅付费，这包含了。

> 注意：访问红帽网站 (`www.redhat.com/subscription`) 获取最新价格。

以下是可用价格：

- RHEL 高级平台：$499

- RHEL 服务器：$399

- RHEL 桌面：$299

- RHEL 工作站：$219

- RHEL 多操作系统桌面：$120

- RHEL 基础桌面：$80

- RHEL 学术桌面：$30

- RHEL 学术服务器：$60

- RHEL 主机：请联系红帽

- RHEL IBM Power：请联系红帽

- RHEL Itanium：请联系红帽

- RHEL x86/x64：请联系红帽

- RHEL AMD：请联系红帽

要比较不同 RHEL 订阅的价格和服务，请参考 `www.redhat.com/desktop/compare`。要比较服务器订阅，请参考 `www.redhat.com/server/compare`。

## 获取 RHEL 评估订阅
