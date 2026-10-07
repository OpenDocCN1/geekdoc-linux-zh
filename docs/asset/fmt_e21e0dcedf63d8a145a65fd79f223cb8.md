
```
divert(-)
dnl 这是一个用于生成 /etc/sendmail.cf 的宏配置文件
dnl 文件. 如果你修改了此文件，你将不得不通过运行此宏配置通过 m4
dnl 预处理器重新生成
dnl /etc/sendmail.cf
dnl
dnl m4 /etc/sendmail.mc > /etc/sendmail.cf
dnl
dnl 你需要安装 sendmail-cf 软件包才能让此项操作
dnl 正常工作。
include(/usr/lib/sendmail-cf/m4/m4.m')
define('CONF_USER_ID','8:2')
OSTYPE('linux')
define('BITNET_RELAY')
define('CONF_RELAY','')
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('CONF_RELAY',true)
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
define('A=procmail -Y -m $h $f $u')
```

## 管理邮件列表

尽管 `sendmail` 提供了多种灵活的地址别名方法，但许多情况下需要额外的功能。邮件列表管理器（或更常见的列表服务器）提供了处理大型分发列表的能力，并结合高级功能，如版员、带有文件传输的归档、邮件摘要、自动订阅以及对无效地址的自动过滤。

列表服务器通常为每个列表的配置提供多个选项（回复作者、回复列表、任何人都可以向列表发布、发布仅限于订阅者、订阅对任何人开放、订阅必须确认等）。它们还提供了消息如何呈现给接收者的选项（带有自定义的页眉和页脚、主题前缀、页眉或正文中的过滤文本等）。

本节将简要介绍 `majordomo` 邮件列表管理器。`Majordomo` 是一个用 `Perl` 编写的免费列表服务器，除了允许切换到 `majordomo` 用户的封装程序外。配置文件（用于列表服务器以及每个单独的列表）均为纯文本，易于编辑。其他可用的邮件列表管理器列在侧栏中。

## 其他邮件列表管理器

虽然列表服务器的基本概念对所有邮件列表管理器都是，但某些软件包提供了截然不同的功能，并以不同的方式处理该任务。下面描述了 Linux 可用的其他列表服务器。

- **CRET ListProc 8.2**: 通过向 CREN（研究与教育网络协会）捐赠 2000 美元获得，该邮件列表管理器具有基于 Web 的管理、强大的日志记录功能和自动删除无效地址的功能。更多信息和免费试用版可以在 http://www.cren.net/listproc/ 找到。

- **listar 0123a**: 这个免费的邮件列表管理器（最初为 Linux 创建）具有非特权执行、通过电子邮件进行安全远程管理以及通过动态加载模块进行扩展的特点。详情和源代码可从 http://www.listar.org/ 获取。

- **L-Soft LISTSERV Classic**: 已使用十多年（最初在 IBM 主机计算机上），该软件包具有通过电子邮件传输文件、索引、摘要和订阅标记的功能。详情、定价信息和受限免费版可以从 http://www.lsoft.com/listserv/ 下载。

- **L-Soft LISTSERV Lite**: 基于 LISTSERV Classic 软件包，此免费列表服务器提供了许多相同的基本功能，但功能和扩展性有限。可以从 http://www.lsoft.com/listserv-lite.stm 获取。

# 第 19 章设置邮件服务器

### 安装 majordomo

`majordomo` 的当前版本是 1.94.4。`Majordomo` 在 Contributed RPMs 或任何 Red Hat 镜像站上提供 RPM 格式，源码分发可以从 http://www.greatcircle.com/majordomomo/ 获取。可以使用以下命令安装软件包：

```
rpm -ivv majordomomo-1.94.4-6.i3886.rpm
```

安装过程的输出如下：

```
D: counting packages to install

D: found 1 packages

D: looking for packages to download

D: retrieved 0 packages

D: New Header signature

D: Signature size: 68

D: Signature pad : 4

D: getsize : 72

D: Header + Archive: 309171

D: expected size : 309171

D: opening database mode 0x42 in //var/lib/rpm/

D: found 0 source and 1 binary packages

(dependency checks)

D: installing binary packages

D: package: majordomomo-1.94.4-6 files test - 0

D: file: /etc/logrotate.d/majordomomo action: create

D: file: /etc/majordomo.cf: create

D: file: /usr/doc/majordomomo-1.94.4/action: create

D: file: /usr/doc/majordomomo-1.94.4/Changel: create

D: file: /usr/doc/majordomomo-1.94.4/FAQ: create

D: file: /usr/doc/majordomomo-1.94.4/FUTURE: create

D: file: /usr/doc/majordomomo-1.94.4/INSTALL: create

D: file: /usr/doc/majordomomo-1.94.4/LICENSE: create

D: file: /usr/doc/majordomomo-1.94.4/NEWLIST: create

D: file: /usr/doc/majordomomo-1.94.4/NEWS: create

D: file: /usr/doc/majordomomo-1.94.4/README: create

D: file: /usr/doc/majordomomo-1.94.4/sequencer: create

D: file: /usr/doc/majordomomo-1.94.4/bulk_mailer: create

D: file: /usr/doc/majordomomo-1.94.4/aliases: create

D: file: /usr/doc/majordomomo-1.94.4/firewalls.cf: create

D: file: /usr/doc/majordomomo-1.94.4/firewalls.header: create

D: file: /usr/doc/majordomomo-1.94.4/firewalls.digest: create

D: file: /usr/doc/majordomomo-1.94.4/firewalls.trailer: create

D: file: /usr/doc/majordomomo-1.94.4/firewalls.vol: create

D: file: /usr/doc/majordomomo-1.94.4/list-info: create

D: file: /usr/doc/majordomomo-1.94.4/majordomo.html: create
```

### IV Red Hat 网络与服务器设置

```
D: file: /usr/src/majordomomo-1.94.4/majordomo.txt: create

D: file: /usr/src/majordomomo-1.94.4/majordomo.ps: create

D: file: /usr/src/majordomomo-1.94.4/majordomo: create

D: file: /usr/src/majordomomo-1.94.4/man/action: create

D: file: /usr/src/majordomomo-1.94.4/man/approve.1: create

D: file: /usr/src/majordomomo-1.94.4/man/approve-remind.1: create

D: file: /usr/src/majordomomo-1.94.4/man/bounce-remind.1: create

D: file: /usr/src/majordomomo-1.94.4/man/bounce.1: create

D: file: /usr/src/majordomomo-1.94.4/man/bounce.man: create

D: file: /usr/src/majordomomo-1.94.4/man/digest.1: create

D: file: /usr/src/majordomomo-1.94.4/man/digest-man: create

D: file: /usr/src/majordomomo-1.94.4/man/majordomo_B: create

D: file: /usr/src/majordomomo-1.94.4/man/majordomo_man: create

D: file: /usr/src/majordomomo-1.94.4/man/resend.1: create

D: file: /usr/src/majordomomo-1.94.4/man/resend.man: create

D: file: /usr/src/majordomomo-1.94.4/man/quick-digest: create
```
