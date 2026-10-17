
# 其他 cron 文件

除了全局 `/etc/crontab` 文件外，取决于发行版还有其他定义 cron 任务的方法：

- `/etc/cron.d`
在发行版中，cron 守护进程还会分析 `/etc/cron.d` 目录下的所有文件。这些文件的规则与 `/etc/crontab` 相同。

- 用户特定的 crontab 文件
取决于发行版，用户特定的 crontab 文件存储在 `/var/spool/cron/` 或 `/var/spool/cron/tabs` 目录中。文件名指示适用于用户。这些文件中省略了六列。可以使用 `crontab` 命令更改用户特定的 cron 项。

- `cron.hourly`, `cron.daily`, `cron.weekly`, `cron.monthly`
在大多数发行版中，`/etc/crontab` 中的默认配置包含某些条目，导致 `/etc/cron.hourly/*` 中的所有脚本以 root 权限每小时执行一次，`etc/cron.daily/*` 每天一次。这些文件是普通的脚本文件，不适用 crontab 语法规则。但记得设置执行位（`chmod +x file`）！

`cron.daily`、..weekly 和 .monthly 中的自定义脚本文件名可能仅由数字、字母、连字符和下划线组成。只要文件名包含一个点，脚本将被忽略！如果安装了 Anacron 程序，来自 `/etc/cron..weekly` 和 .monthly 的脚本将不会执行。

## /etc/deluser.conf

Debian/Ubuntu 特有的文件 `/etc/deluser.conf` 包含了使用 `deluser` 和 `delgroup` 命令删除用户和组的默认设置。`deluser.conf` 文件由 `parameter=value` 格式的逐行条目组成。

- `BACKUP=0|1`
指定对 `REMOVE` 参数删除的文件进行备份。

- `BACKUP_TO`
指定备份目录的位置。

- `EXCLUDE_FSTYPE="fs1,fs2,...)"`
指定在搜索用户文件创建备份时应忽略哪些文件系统。

- `ONLY_IS_EMPTY=1`
导致仅在组为空时删除组

成员。

- `REM_HOME=0|1`
指定是否也应该删除该账户的主目录。

- `REM_ALL_FILES=0|1`
指定是否应该删除主目录之外的用户文件，例如打印缓存文件和电子邮件收件箱。

## 示例

以下行显示了 `deluser.conf` 中在 Ubuntu 上有效的默认设置：

## /etc/dnf/dnf.conf

软件包管理系统 DNF 的基础设置可以在 `/etc/dnf/dnf.conf` 中找到，该系统通常用于 Fedora 和 Red Hat。`/etc/yum.repos.d/` 下的 `*.repos` 文件也包含了各个独立软件包源的详细设置。

### 基础设置

- `clean_requirements_on_remove = true/false`
指定由于依赖关系而安装的软件包在所有引用该包的软件包卸载后，是否应该自动删除。即使此选项为 true，dnf 也不会在未询问的情况下删除通过 `dnf install` 明确安装的包。

- `color=never`
导致终端中的 dnf 命令不使用任何颜色。如果你想使用颜色，请使用 `color=always`。

- `exactarch=1`
导致 dnf 仅考虑架构与已安装软件包匹配的更新。因此，i386 软件包无法被较新的 x86_64 软件包替换。

- `gpgcheck=1`
导致 dnf 使用密钥确保软件包的真实性。也可以偏离 `dnf.conf` 中的设置，为每个软件包源单独设置 `gpgcheck`。插件决定了 dnf 是否考虑插件。

- `installonly_limit=n`
控制同时安装多少个旧版本的内核软件包。该设置影响所有以新包形式安装更新的包。此处理过程确保了受影响软件包的旧版本始终可用，作为回退。

- `keepcache=0`
导致下载的软件包在安装后不进行归档。通常情况下，这是一个非常有用的设置，因为软件包所需的空间随着时间推移会变得很大，而且通常没有理由再次安装这些软件包。然而，可能会出现 dnf 检测到安装并中止安装过程。在这种情况下，下载的软件包将被删除。如果你可以修复问题并重复更新，则所有软件包都必须重新下载。你可以通过使用 `keepcache=1` 来避免这种情况。要显式删除 `/var/cache/dnf` 中的下载包，你必须运行 `dnf clean packages`。

在当前的 Fedora 版本中，该文件仅包含几个设置：

```
# /etc/dnf/dnf.conf on Fedora

[main]

gpgcheck=1

installonly_limit=3

clean_requirements_on_remove=True

best=False

skip_if_unavailable=True
```

### 软件包源

软件包源通过 `/etc/yum.repos.d` 目录下的 `*.conf` 文件配置。在从 yum 切换到 dnf 时，该目录没有重命名为 `/etc/dnf.repos.d`。

- `[variant]`
指定后续设置与软件包源的哪个部分有关。

- `baseurl=url` 或 `mirrorlist=url`
指定软件包文件所在的位置。使用 `mirrorlist` 时，url 指向镜像服务器列表。dnf 会自动选择其中一个镜像。dnf 会将 url 中的 `$releasever`、`'$arch'` 和 `$basearch` 变量替换为 Linux 发行版的版本号及其架构。

- `enabled=0/1`
指示软件包源是否激活。

- `name=repone`
指定软件包源的名称。

- `metadata_expires`
控制从软件包源下载的元数据的有效时间。dnf 将元数据保存在缓存中，如果元数据尚未过期，则不再再次下载。这可以节省时间减少下载量，但可能导致 dnf 忽略软件包源的最近更改。如有必要，你可以使用 `dnf clean metadata` 强制删除本地元数据。这将强制 dnf 在下次执行时重新导入所有软件包源的元数据。

以下行是文件 `/etc/yum.repos.d/fedora.repo` 的节选。该文件包含了 Fedora 发行版基础软件包的软件包源定义。

```
[fedora]

name=Fedora releasever - $basearch

metalink=https://mirrors.fedoraproject.org/metalink

repo=fedora-releasever&arch=$basearch

enabled=1

metadata_expire=7d

repo_gpgcheck=0

type=rpm

gpgcheck=1

gpgkey=file:///etc/rpm/RPM-KEY-GPG-GPG-KEY-fedora-$releasever-$basearch

skip_if_unavailable=False
```

```
[fedora-source]

name=Fedora releasever - Source

...
```
