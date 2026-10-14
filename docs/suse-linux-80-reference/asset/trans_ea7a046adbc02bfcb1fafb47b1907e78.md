

- 关于 postgres 软件包：PostgreSQL 及其所有组件已在原始软件包的基础上重新组织。包含初始化数据库的 `pg_datab` 软件包已不再需要。如果需要，初始化将由启动脚本执行。

- 关于 mutt 软件包：若干细节已更改。配置文件 `/etc/Muttrc` 和 `/etc/skel/.muttrc` 会尽可能保留其熟悉的行为。以下行：

  ```
  set autoedit=yes
  set edit_headers=yes
  ```

  确保在 `.muttrc` 中立即启动编辑器以撰写电子邮件。还有一些关键方面需要新的系统行为，例如 PGP。请阅读相关文档以了解更多信息。

## 从 7.0 到 7.1

问题与特殊功能：`http://sdb.suse.de/sdb/en/html/bugs71.html`。

- **内核：** 用于特殊 EIDE 芯片组的“底层”驱动程序已集成到标准内核中。`k_eide` 和 `eide` 不再需要作为单独的映像。这意味着如果你需要此驱动程序，就不再需要创建自己的启动盘。

- 运行级别已更改。请参阅第 299 页上的表 12.1。init 脚本现在位于 `/etc/init.d`。如果你已经创建了自己的脚本，应确保在更新前对它们进行备份。

- **DEFAULT_LANGUAGE：** 是 `/etc/rc.config` 中原变量 `LANGUAGE` 的新名称（自 SuSE Linux 8.0 起位于 `/etc/sysconfig/language`）。请参阅第 292 页上的*本地调整 — I18N/L10N*一节。

- `/etc/resolv.conf` 现在由 YaST 和 YaST2 直接写入，而不是由 SuSEconfig 写入。自 7.2 版起，此任务由 `aaa_base` 软件包中的脚本 `/sbin/modify_resolvconf` 执行。

- 软件包名称最多八个字符的限制已取消，许多软件包现在有了更具描述性的名称。

- dochost 软件包的功能已整合到 susehelp 软件包中，因此 dochost 已过时。

- 关于原 `ypclient` 软件包：该软件包现在分为 `ypbind` 和 `yp-tools`，init 脚本名为 `ypbind`。

- 关于 `jade_dsl` 软件包：为避免与 `rzsz` 软件包冲突，命令行工具 `sx` 现在称为 `s2x` 和 `sgml2xml`。

## 从 7.1 到 7.2

问题与特殊功能：`http://sdb.suse.de/sdb/en/html/bugs72.html`

- `rsh` 软件包已不复存在。不同的程序已被移入多个软件包：`talk`、`rsh`、`finger`、`rwho`、`telnet` 等。

  许多程序已为 IPv6 做好准备。因此，请确保 DNS 配置正确——否则你可能不得不等待 IPv6 查询的 DNS 超时。此外，在 `/etc/nsswitch.conf` 中，将条目 `dns` 替换为 `dns6`。

- 若干软件包已更名（见前一页），例如：
  - `series sgm`：软件包 `docbook-dsssl-stylesheets`、软件包 `docbook_3` 和软件包 `docbook_4`。

- 现在你必须安装软件包 `mod_php4`，而不是软件包 `mod_php`。

- Emacs 已被拆分为多个软件包：
  - 基础软件包 `emacs`。
  - 此外，你必须安装软件包 `emacs-x11`，它包含*带有* X11 支持的程序。
  - 软件包 `emacs-nox` 包含*不带* X11 支持的程序。
  - 软件包 `emacs-info`：info 格式的在线文档。
  - 软件包 `emacs-el` 包含用 Emacs Lisp 编写的未编译库文件——运行环境并不需要它们。
  - 如果需要，还可安装大量附加软件包：软件包 `emacs-auctex`（用于 \TeX）、软件包 `psgml`（用于 SGML/XML）、软件包 `gnuserv`（用于客户端-服务器环境）等。

- 为遵循当前 FHS（请参阅第 272 页上的*文件系统层次结构标准（FHS）*一节）所做的更改：
  - `/media`（原为 `/cdrom` 和 `/floppy`）

  在过渡期内将提供兼容链接。

## 从 7.2 到 7.3

问题与特殊功能：`http://sdb.suse.de/sdb/en/html/bugs73.html`。

- SuSE Linux 附带的 2.4 内核默认启用 IDE-DMA。如果你遇到与 DMA 相关的任何问题，始终可以回退到“安装 — 安全设置”启动选项。另请参阅第 32 页。

- 除了 `rc.config` 中定义的 DISPLAYMANAGER 变量（自 SuSE Linux 8.0 起位于 `/etc/sysconfig/displaymanager`）之外，还需要在 `/etc/inittab` 中设置正确的运行级别。YaST2 可以处理此事。另请参阅第 84 页上的*运行级别编辑器*一节。

- Samba：配置文件已移至 `/etc/samba` 目录，以提高清晰度。

- MySQL 现在使用 TCP wrapper 库来增强安全性。新的子软件包 `mysql-Max` 提供所有新增和增强功能，安装后即可自动使用。

- 为节省空间（超过 30 MB），`allman` 软件包不再包含在内。不过，手册页仍包含在各软件包中。

- 使用某些“特性”的 DocBook 文档会被 `db2x.sh`（软件包 `docbktst`）接受。依赖兼容文档的用户应使用 `--strict` 选项。

## 从 7.3 到 8.0

问题与特殊之处：`http://sdb.suse.de/sdb/en/html/bugs80.html`。

- 启动盘仅以软盘映像的形式提供（disks 目录）。只有在无法从 CD 启动时才需要启动盘。根据你的硬件或安装偏好，你还可以从映像模块（原 modules）和 modules2 创建软盘。有关创建这些磁盘的信息，请参阅第 44 页上的*在 DOS 中创建启动盘*和第 45 页上的*在类 UNIX 系统中创建启动盘*。

- YaST2 已完全取代 YaST1，即使在文本和控制台模式下也是如此。

- 某些 BIOS 需要内核参数 `real-mode-poweroff=off`，该参数直到内核版本 2.4.12 为止被称为 `real-mode-poweroff`。

- 不再需要 `rc.config` 中用于启动服务的 START 变量。如果运行级别目录中存在相应的链接，服务就会启动。这些链接通过 `insserv` 创建。

- 系统服务通过 `/etc/sysconfig` 下文件中的变量行进行配置。`/etc/rc.config.d` 中的设置将在更新时应用。

- `/etc/init.d/boot` 由多个脚本组成，并在必要时移至其他软件包（参见软件包 `kbd`、软件包 `isapnp`、软件包 `lvm` 等）。另请参阅第 301 页。

- 网络领域也有一些更改。有关详细信息，请参阅第 336 页上的*SuSE Linux 8.0 中的更改*一节。

- `logrotate` 用于管理日志文件。`/etc/logfiles` 不再需要。请参阅第 273 页上的*日志文件 — logrotate 软件包*一节。

- 可以通过在 `/etc/pam.d` 下的文件中输入相关配置，允许通过 telnet 或 rlogin 进行 root 登录。由于存在安全风险，`ROOT_LOGIN_REMOTE` 不能再设置为 yes。

- `PASSWD_USE_CRACKLIB` 可以使用 YaST2 激活。

- 如果用于 autofs 的 NIS 文件将通过 NIS 分发，则应使用 YaST2 NIS 客户端模块进行配置。在那里选择“启动自动挂载器”。这一方面已使 `USE_NIS_FOR_AUTOS` 变量过时。

- 用于快速查找文件的 locate 工具不再包含在标准软件安装中。如果需要，可稍后安装。如果已安装，`updatedb` 进程——与先前版本一样——将在计算机启动约十五分钟后自动激活。

## RPM — 发行版软件包管理器

在 SuSE Linux 中，RPM（rpm），即“Red Hat 软件包管理器”，充当软件包管理器。它使强大的 RPM 数据库对所有人可用：用户、系统管理员，当然还有软件包构建者。可以随时从数据库中查询有关已安装软件的详细信息。

本质上，rpm 有三种模式。在一种模式中，它从“源代码”编译软件应用程序并将其打包以供安装。在第二种模式中，它安装、升级并彻底卸载以 RPM 格式打包的软件。最后，在第三种模式中，它支持对软件包的查询，并维护已安装软件包的 RPM 数据库。

可安装的 RPM 归档文件以特殊的二进制格式打包。这些归档文件由待安装的程序文件和某些元信息组成，rpm 在安装期间使用这些元信息配置软件包，或将其存储在 RPM 数据库中作为文档记录。RPM 归档文件通常具有 .rpm 扩展名。

> **提示**
> 
> 对于许多软件包，软件开发所需的组件（库、头文件、包含文件等）已被放入单独的软件包中。仅当你想要自行编译软件时，才需要这些开发软件包，例如最新的 GNOME 软件包。这些开发软件包可以通过其名称扩展名 `-devel`（以前为 `dev` 或 `d`）识别；例如软件包 `alsa-devel`、软件包 `gimp-devel`、软件包 `kdelibs-devel` 等。

### 验证软件包的真实性

自 7.1 版起，SuSE RPM 软件包带有 GnuPG 签名：

```
1024D/9C800ACA 2000-10-19 SuSE Package Signing Key <build@suse.de>
Key fingerprint = 79C1 79B2 E1C8 20C1 890F 9994 A84E DAE8 9C80 0ACA
```

使用以下命令

```
earth:~ # rpm --verbose --checksig apache-1.3.12.rpm
```

验证 RPM 软件包的签名，以确定它是否确实来自 SuSE 或其他可信来源。对于从互联网下载的更新软件包，尤其建议这样做。我们的公共软件包签名密钥通常位于 /root/.gnupg/。

