

## 查询选项

| **使用此选项** | **执行此操作** |
| :--- | :--- |
| `--a, --all` | 查询所有已安装的软件包。 |
| `--c, --configfiles` | 仅列出配置文件。 |
| `--changelog` | 显示软件包的更改信息。 |
| `--d, --docfiles` | 仅列出文档文件。 |
| `--dump` | 显示以下信息：路径名、文件大小、修改时间、MD5 校验和、模式、所有者、组、iconfig、isdoc、redev 和符号链接。与以下选项之一配合使用：`-l`、`-c` 和 `-d`。 |
| `-f filename`, `---file filename` | 查询拥有指定文件名的软件包。 |
| `--filesby pkg` | 列出每个软件包中的所有文件。 |
| `-g group`, `--group group` | 查询具有指定组的软件包。 |
| `-l`, `-list` | 列出软件包中的文件。 |
| `-last` | 首先安装最新的软件包。 |
| `package` | 查询该软件包。 |
| `--provides` | 列出该软件包提供的功能。 |
| `-p package` | 查询指定的软件包文件。 |
| `-querybnumber n` | 查询第 n 个数据库目录。 |
| `-R, --requires` | 列出该软件包依赖的软件包。 |
| `-s, --state` | 显示软件包中文件的状态。 |
| `--scripts` | 列出在安装和卸载过程中使用的特定于软件包的 shell 脚本。 |
| `--specfile spec file` | 解析并查询指定的 spec 文件，如同其是一个软件包一样。 |
| `--triggeredby package` | 查询指定的软件包。 |
| `--triggers, --triggerscripts` | 显示触发器脚本。 |
| `--triggerscripts` | 显示所选软件包的所有触发器脚本。 |
| `--whatprovides virtual` | 查询所有提供该虚拟功能的软件包。 |
| `--whatrequires capability` | 查询所有需要该功能才能正常工作的软件包。 |

## 验证选项

| **使用此选项** | **执行此操作** |
| :--- | :--- |
| `--nofiles` | 在验证时忽略缺失的文件 |
| `--nomd5` | 在验证时忽略 MD5 校验和错误 |
| `--nopgp` | 在验证时忽略 PGP 检查错误 |
| `--checksig package` | 检查指定软件包的数字签名 |

## 卸载选项 (-e)

| **使用此选项** | **执行此操作** |
| :--- | :--- |
| `--allmatches package` | 移除所有匹配该软件包的版本 |
| `--nodeps` | 省略依赖检查 |
| `--noscripts` | 跳过预卸载和后卸载脚本 |
| `--notriggers` | 跳过由软件包移除触发的脚本 |
| `--test` | 测试卸载而不实际删除文件 |

## 构建选项 (-b)

| **使用此选项** | **执行此操作** |
| :--- | :--- |
| `--ba` | 构建二进制和源代码软件包 |
| `--bb` | 构建二进制软件包 |
| `--bc` | 基于 spec 文件构建软件包 |
| `--bi` | 基于 spec 文件安装软件包 |
| `--bl` | 检查以确保所有必需的文件都存在 |
| `--bp` | 执行 spec 文件中的准备阶段 |
| `--bs` | 构建源代码软件包但不构建二进制文件 |
| `--buildroot directory` | 使用指定的目录代替默认的 BuildRoot 目录 |
| `--clean` | 在软件包制作完成后移除构建树 |
| `--rebuild` | 重新构建源代码软件包 |
| `--recompile` | 安装源代码软件包并进行完整重新编译 |
| `--rmsource` | 在构建后移除源文件和 spec 文件 |
| `--short-circuit` | 直接跳转到指定阶段 |
| `--sign` | 使用 GPG 签名签署软件包 |
| `--target architecture vendor OS` | 为指定的体系结构、供应商和操作系统（OS）创建软件包 |
| `--test` | 测试而不实际构建 |
| `--timecheck n` | 指定正在打包的文件的最大年龄 n（以秒为单位） |

## 重建数据库选项

| **使用此选项** | **执行此操作** |
| :--- | :--- |
| `rpm --initdb` | 构建新数据库 |
| `rpm --rebuilddb` | 重建现有数据库 |

## 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `rpm -ivh newpackage.rpm` | 安装指定的软件包 (`newpackage.rpm`)，该软件包之前从未被安装过。 |
| `rpm -Uvh newversion.rpm` | 升级指定的软件包 (`newversion.rpm`)，或者如果未找到之前的版本则安装该软件包。 |
| `rpm -Fvh newversion.rpm` | 仅当存在之前版本时，升级指定的软件包 (`newversion.rpm`)。 |
| `rpm -ivh --nodeps new-package.rpm` | 安装指定的软件包 (`newpackage.rpm`)，忽略软件包依赖。 |
| `rpm -ivh --force new-package.rpm` | 安装指定的软件包 (`newpackage.rpm`)，必要时覆盖软件包和文件。 |
| `rpm -e unwanted` | 卸载指定的软件包 (`unwanted`)。 |
| `rpm -Uvh --oldversion installed-program oldpackage.rpm` | 将当前已安装的软件包 (`installed-program`) 降级到更早的版本 (`oldpackage.rpm`)。 |
| `rpm -q installed-program` | 显示指定已安装软件包 (`installed-program`) 的版本号。 |
| `rpm -qa` | 显示所有已安装软件包的列表。 |
| `rpm -qa \| grep -i string` | 显示仅包含指定字符串的已安装软件包列表。 |

## rpmfind

`rpmfind [ option ] package`

在可访问互联网的 RPM 软件包数据库中搜索指定的软件包。默认情况下，该实用程序搜索 http://rpmfind.org。您可以使用 -s 选项指定不同的服务器。此处记录的版本为 1.4。如果您的系统未安装此实用程序，您可以从 http://www.rpm.org 获取最新版本。

### 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| `--apropos keyword` | 浏览 RPM 数据库，查找描述标签中包含指定关键字的所有软件包 |
| `--auto` | 在不确认的情况下执行传输 |
| `-h` | 列出所有可用选项 |
| `--latest` | 获取最新可用的软件包 |
| `--source` | 查找源代码软件包 |
| `-s URL` | 将默认服务器更改为指定的 URL |
| `--upgrade` | 建议升级所需的软件包及其所有依赖项 |
| `-v` | 显示可用消息 |

### 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `rpmfind --apropos gqview` | 显示其描述中任何位置都包含指定字符串 (`gqview`) 的所有软件包。 |
| `rpmfind --latest ghostview` | 显示指定软件包 (`ghostview`) 的最新可用版本。 |
| `rpmfind --upgrade ghostview` | 如果可用，则为指定软件包 (`ghostview`) 查找升级包。 |

## runlevel

`runlevel [ filename ]`

报告当前系统运行级别，如默认运行级别配置文件 (`/var/run/utmp`) 或指定的配置文件名所显示。

## tmpwatch

`tmpwatch [ option ] [ n ] [ directory ]`

如果指定目录中的文件在 *n* 小时内未被访问，则删除所有文件。此命令清理临时目录（例如 /tmp 中的目录），防止它们占用过量的磁盘空间。

### 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| `-u, --atime` | 使用最后访问时间来决定是否删除文件。这是默认设置。 |
| `-m, --mtime` | 使用最后修改时间来决定是否删除文件。 |
| `-a, --all` | 删除所有文件类型，而不仅仅是常规文件和目录。 |
| `-f, --force` | 即使 root 没有写入权限也删除文件。 |
| `--test` | 显示将被删除的文件，而不实际删除它们。 |
| `-v` | 显示所有消息。 |

## useradd

`useradd [ option ] username`

`useradd --D [ option ] username`

使用指定的用户名创建新用户（或更新现有用户）。创建新的用户帐户时，此命令会自动配置适当的系统文件并复制 /etc/skel 中的文件。使用 -m 选项创建新的主目录（命名为 /home/username）。有关创建新帐户时可用选项，请参阅“帐户创建选项”表。

