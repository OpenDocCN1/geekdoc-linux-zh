
- `logrotate` 用于管理日志文件。`/etc/logfiles` 不再需要。请参阅第 273 页上的*日志文件 — logrotate 软件包*一节。

- 可以通过在 `/etc/pam.d` 下的文件中输入相关配置，允许通过 `telnet` 或 `rlogin` 进行 root 登录。由于存在安全风险，`ROOT_LOGIN_REMOTE` 不能再设置为 `yes`。

- `PASSWD_USE_CRACKLIB` 可以使用 `YaST2` 激活。

- 如果用于 `autofs` 的 NIS 文件将通过 NIS 分发，则应使用 `YaST2` NIS 客户端模块进行配置。在那里选择“启动自动挂载器”。这一方面已使 `USE_NIS_FOR_AUTOS` 变量过时。

- 用于快速查找文件的 `locate` 工具不再包含在标准软件安装中。如果需要，可稍后安装。如果已安装，`updatedb` 进程——与先前版本一样——将在计算机启动约十五分钟后自动激活。

## RPM — 发行版软件包管理器

在 SuSE Linux 中，`RPM`（`rpm`），即“Red Hat 软件包管理器”，充当软件包管理器。它使强大的 RPM 数据库对所有人可用：用户、系统管理员，当然还有软件包构建者。可以随时从数据库中查询有关已安装软件的详细信息。

本质上，`rpm` 有三种模式。在一种模式中，它从“源代码”编译软件应用程序并将其打包以供安装。在第二种模式中，它安装、升级并彻底卸载以 RPM 格式打包的软件。最后，在第三种模式中，它支持对软件包的查询，并维护已安装软件包的 RPM 数据库。

可安装的 RPM 归档文件以特殊的二进制格式打包。这些归档文件由待安装的程序文件和某些元信息组成，`rpm` 在安装期间使用这些元信息配置软件包，或将其存储在 RPM 数据库中作为文档记录。RPM 归档文件通常具有 `.rpm` 扩展名。

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

验证 RPM 软件包的签名，以确定它是否确实来自 SuSE 或其他可信来源。对于从互联网下载的更新软件包，尤其建议这样做。我们的公共软件包签名密钥通常位于 `/root/.gnupg/`。

## 管理软件包：安装、更新和卸载

通常，使用 `rpm -i (package).rpm` 即可简单地完成 RPM 安装。使用此命令时，软件包将被安装——但前提是满足其依赖要求且不与另一个软件包冲突。`rpm` 会通过错误信息提示需要安装哪些软件包来满足依赖关系。在后台，RPM 数据库确保不会产生冲突——一个特定文件只能属于一个软件包。通过选择不同的选项，你可以强制 `rpm` 忽略这些默认设置，但务必清楚自己在做什么。否则，你可能会损害系统的完整性，并可能危及系统的更新能力。

使用 `-U` 或 `--upgrade` 更新软件包。该选项会移除旧版本的文件并立即安装新文件。`rpm` 会以更谨慎的方式更新配置文件：

- 如果配置文件**未被**系统管理员修改，`rpm` 将安装相应文件的新版本。无需系统管理员执行任何操作。

- 如果在更新**之前**配置文件已被系统管理员修改，`rpm` 将以扩展名 `.rpmorig` 或 `.rpmsave`（备份文件）保存已修改的文件，并安装新软件包的版本，但前提是原始安装的文件与新版本不同。如果是这种情况，请将备份文件（`.rpmorig` 或 `.rpmsave`）与新安装的文件进行比较，并在新文件中再次进行你的修改。之后，请务必删除所有 `.rpmorig` 和 `.rpmsave` 文件，以免影响将来的更新。

- 如果配置文件已存在**且**在 `.spec` 文件中指定了 `noreplace` 标签，则会出现 `.rpmnew` 文件。

更新后，应在比较后删除 `.rpmsave` 和 `.rpmnew` 文件，以免妨碍将来的更新。如果之前 RPM 数据库未识别该文件，则会分配 `.rpmorig` 扩展名。否则，使用 `.rpmsave`。换句话说，`.rpmorig` 是从外部格式更新为 RPM 时产生的，而 `.rpmsave` 是从旧版 RPM 更新为新版 RPM 时产生的。`.rpmnew` 不透露系统管理员是否对配置文件进行了任何更改的信息。`-U` 选项不仅仅等同于使用 `(-e)` 选项卸载和使用 `(-i)` 选项安装。请尽可能使用 `-U`。

> **注意**
>
> 每次更新后，请检查 `rpm` 创建的所有备份文件。这些是你的旧配置文件。如有必要，将备份文件中的自定义设置合并到新配置文件中。完成此过程后，应删除扩展名为 `.rpmorig` 和 `.rpmsave` 的文件。

要移除软件包，请输入以下命令：

```bash
earth: # rpm -e {package}
```

只有在没有未解决的依赖关系时，`rpm` 才会删除该软件包。因此，例如，只要另一个应用程序需要 Tcl/Tk，理论上就不可能删除它。即使在这种情况下，RPM 也会请求数据库的协助。

如果由于某种原因且在异常情况下，即使不存在其他依赖关系，此类删除仍然不可能，那么使用 `--rebuilddb` 选项重建 RPM 数据库可能会有所帮助。请参阅下面关于 RPM 数据库的附注（第 75 页的 *RPM 查询* 一节）。

### RPM 查询

使用 `-q` 选项，`rpm` 会发起查询，从而可以检查 RPM 归档文件（通过添加 `-p` 选项），也可以查询已安装软件包的 RPM 数据库。可以使用多个开关来指定所需信息的类型（参见表 4.1）。

| 选项 | 描述 |
|---|---|
| `-i` | 软件包信息 |
| `-l` | 文件列表 |
| `-f {FILE}` | 查询 `{FILE}` 所属的软件包（必须使用 `{FILE}` 指定完整路径） |
| `-s` | 包含状态信息的文件列表（隐含 `-l`） |
| `-d` | 仅列出文档文件（隐含 `-l`） |
| `-c` | 仅列出配置文件（隐含 `-l`） |
| `--dump` | 包含完整详情的文件列表（与 `-l`、`-c` 或 `-d` 一起使用） |
| `--provides` | 列出软件包的功能，其他软件包可通过 `--requires` 请求这些功能 |
| `--requires, -R` | 软件包所需的功能 |
| `--scripts` | 安装/卸载脚本（预安装、后安装、卸载） |

*表 4.1：最重要的 RPM 查询选项* — (`-q` [`-p` ... `{package}`])

例如，命令

```bash
earth: # rpm -q -i rpm
```

将显示输出 3 中所示的信息：

```text
Name          : rpm                         Relocations: (not relocatable)
Version       : 3.0.3                       Vendor: SuSE GmbH, Germany
Release       : 47                          Build Date: Fri Dec 10 13:50:27
Install date  : Tue Dec 14 12:57:00 1999   Build Host: Cauchy.suse.de
Group         : unsorted                    Source RPM: rpm-3.0.3-47.src.rpm
Size          : 574084                      License: GPL
Packager      : feedback@suse.de
Summary       : RPM Package Manager
Description   :
RPM Package Manager is the main tool for managing software packages
of the SuSE Linux distribution.
[...]
```

**输出 3：rpm -q -i rpm**
