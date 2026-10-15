
使用 DSSL 将 DocSGML 源转换为 HTML。这是一个基于 SGML（标准泛化标记语言）的文本格式程序包，它允许你通过推荐和建议的程序包从单个源生成 TeX/DIV/PS/PDF、HTML、RTF 和纯 ASCII（默认使用 w3m）；由于 SGML 的灵活性，还可能生成许多其他目标。该工具也无法处理 DocSGML XML。仅用于 DocSGML。可以在不安装其他 Debian 文本处理包的情况下生成 HTML，但需要安装其他适当的包。你需要安装 `lyn` 用于 PS 和 PDF，并安装 `w3m` 用于 ASCII 输出（`w3m` 是默认后端）。编写技术软件文档需要一个 jadex，Linux HOWTO 文档就是其中的示例。然而，此程序包本身并没有特殊之处；它可以用于许多其他系统上的许多其他类型的文档。该程序包以前称为 linux-doc，因为它源于 Linux 文档项目 (LDP)。名称已更改为 sgmltools，以更明确表示该包中不包含 Linux 特有的内容：这是 sgmltools 系列的最新版本，是 sgmltools v2 的继者。来自 Debian 3.0r0 APT `http://www.tldp.org/LDP/Linux-Dictionary/index.html`

### sgmlich

输出系统 SGML 目录路径

来自 whatis

`http://www.tldp.org/LDP/Linux-Dictionary/index.html`

### SGMP

简单网关监控协议 (RFC 1028)

来自 VERA

`http://www.tldp.org/LDP/Linux-Dictionary/index.html`

### SGRAM

同步图形随机存存储器 (DRAM, RAM)

来自 VERA

`http://www.tldp.org/LDP/Linux-Dictionary/index.html`

### sgrep

用于搜索结构化模式的工具。`grep`（结构化 grep）是一种用于搜索文本文件并根据结构化标准过滤术的工具。`Sgrep` 实现了一种基于区域表达式的查询语言。像 `grep` 一样，`spart` 可用于任何文本文件。然而，它对于包含某些结构化文本的文件最有用。包含文本的文件可以定义为遵循某些语法的文件。结构化文本的示例包括 SGML、HTML、C 和文本邮件文件。来自 Debian 3.0r3 APT

```
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html
```

# SGSN

GPRS 支持节点 (GPRS, 移动系统)

来自 VERA

```
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html
```

# SGT

环绕栅极晶管 (IC)

来自 VERA

```
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html
```

# SGTSI

半图形树结构接口

来自 VERA

```
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html
```

# sh

GNU Bourne-Again Shell

来自 White 是一组在 shell 脚本中使用的工具。`http://www.tldp.org/LDP/Linux-Dictionary/index.html`

# sh-utils

GNU shell utils 是一组在 shell 脚本中使用的工具。`sh` 包包含 `basename`（从指定路径中删除路径前缀）、`chroot`（更改根目录）、`date`（打印/设置系统时间）、`dirname`（从给定路径重命名层级或文件名）、`echo`（打印一行文本）、`env`（显示/修改环境）、`expr`（求值表达式）、`factor`（质数）、`false`（返回失败状态）、`groups`（打印用户所属的组）、`id`（打印真实的 uid/gid）、`logname`（打印当前登录名）、`nice`（修改优先级）、`nohup`（允许命令在退出后继续）、`patch`（检查文件）、`print`（打印环境）、`printf`（格式化并打印数据）、`pwd`（打印当前目录）、`sets`（打印序列）、`sleep`（暂停指定时间）、`stty`（控制终端设置）、`sudo`（成为另一个用户或超级用户）、`tee`（将输出发送到多个文件）、`test`（评估表达式）、`true`（返回成功状态）、`type`（打印类型）、`uname`（打印系统信息）、`users`（打印当前用户）、`who`（打印登录用户列表）、`whom`（打印有效用户）、`yes`（打印字符串）。来自 Redhat 8.0 RPM

```
http://www.tldp.org/LDP/Linux-Dictionary/index.html
```

# SHA

安全哈希算法 (密码学, NIST)

来自 VERA

```
http://www.tldp.org/LDP/Linux-Dictionary/index.html
```

# SHA Aipture (LCD)

来自 VERA

```
http://www.tldp.org/LDP/Linux-Dictionary/index.html
```

# SHA-1

美国政府哈希算法 FIPS 180-1, ISO/IEC SHA-1 是一种流行的哈希算法。它将输入消息转换为 160 位指纹。该指纹被认为是“唯一的”；虽然理论上两个输入可能会哈出相同的指纹，但在统计学上是不可能的。对比：SHA 目前被认为是最强大的哈希算法。历史：SHA-1 是 SHA 的一种变体。它在每个阶段增加一个位的位移以达到理论缺陷，SHA 基于 MD4，以克服已知缺陷并将长度增加到 160 位。完整性来自 Hacking-Lexicon

```
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html
```

# shadow-utils

`shadow-utils` 包包含了将 UNIX 文件转换为 shadow 格式的必要程序，以及管理用户和组账户的程序。`pwconv` 命令将密码转换为 shadow 格式，并将密码生成 `passwd` 文件（标准的 UNIX 密码）。`pw` 命令检查密码和 shadow 文件的完整性。`lastlog` 命令打印所有用户的最后登录时间。`usermod` 和 `userdel` 命令用于用户账户。`groupadd`、`groupmod` 和 `groupdel` 命令用于组账户。来自 Mandrake 9.0 RPM

`http://www.ldp.org/LDP/Linux-Dictionary/index.html`

# shadowconfig

开启和关闭影子密码

来自 `http://www.ldp.org/LDP/Linux-Dictionary/index.html`

# shadow passwords (/etc/shadow)

UNIX 的设计理念是让加密格式对所有人可见。这些密码存储在 `/etc/passwd` 文件中，带有完整的账户信息。然而，这被认为是安全的，因为密码是以加密格式在该文件中。但在实践中并不安全，因为用户倾向于选择简单的密码。开发了一个名为 `crack` 的程序会猜测字典单词 (`/usr/dict`) 然后尝试强制密码。在平均 UNIX 系统上，90% 的密码文件只需几小时计算时间即可破解。为了解决这个问题，开发了“影子”密码文件。加密密码从正常的 `/etc/passwd` 中移除，并放置在只有 root 可读的特殊文件中（通常 `/etc/shadow`）。留在原始密码文件中以向下兼容。以下是影子密码的示例：

- AI 3 `/etc/security/password/etc/shadow`

- IRIS 5 `/etc/shadow/pwwnsd`

- Convex 10 `/etc/shadow/UX`

- UX 11 `/etc/shadow/UX/chaa/user/IRPI`

- EP `/etc/shadow-UNIX /etc/shadow/OSFI/shadow/adjunct`

- SunOS 5.0 `/etc/dig.part /X.2 /etc/shadow/SunOS4.1c2 /etc/shadow/System V Release 4.2 /etc/security/*`

- Database IV `/etc/auth.dir`

关键点：过去，大多数针对 UNIX 的攻击都指向 `/etc/passwd` 文件。例如，最常见的威胁形式就是密码文件。随着影子密码变得越来越常见，攻击越来越多地完整了影子密码文件。来自 Hacking-Lexicon

`http://www.tldp.org/LDP/Linux-Dictionary/index.html`

# shapefig

`Shapefig` 配置并调整流量带宽限制。流量整形对带宽消耗设置参数限制，网络流量应遵守。要使用 `Shapefig`，你还必须安装支持 shape 模块的内核（内核版本 2.0.36 或后续 2.1 x 内核）。来自 Redhat 8.0 RPM
