
# Add these for mysql support
`/etc/mysql/mysql.cnf` r, `/#/{var/run/mysqld/mysqld.sock rw,`

# Add these for postgresql support
`#include <abstractions/openssl>` `#include <abstractions/ssl_certs>` `/#/.var/run/postgresql/s.PGSQL*[-0-9] rw,`

# Site-specific additions and overrides. See local/README for details.
`#include <local/usr/sbin.rsyslog>`

```
即使不知道语法，你也可以看出这些文件是简单的文本文件，它们支持注释、绝对路径和通配符（文件名的模式匹配），并允许或禁止特定的能力（capabilities），并规定了文件系统中的哪些位置和程序可以被访问或使用。
```

每条访问规则都指定了列表中的特定权限：

- 读取（read）
- 写入（write）
- 无限制执行（unconstrained execute）
- 无限制执行 - 清除环境（unconstrained execute - scrub the environment）
- 离散执行（discrete execute）
- 离散执行 - 清除环境（discrete execute - scrub the environment）
- 继承执行（inherit execute）
- 允许带有 `mmap(2)` 调用 的 `PROT_EXEC`（allow PROT_EXEC with mmap(2) calls）
- 链接（link）

这些权限列在行末尾。

`genprof` 是一个帮助你生成或更新配置程序。你可以提供执行文件的名称（如果它不在路径中，则提供路径），并可选地提供配置文件的路径。以下是一个示例：

```
matthew@semour-$ sudo genprof google-chrome
```

你将能够启动该程序并运行一段时间。完成后，你将获得机会选择允许或拒绝对每个函数的访问。该程序会在 `/etc/apparmor.d` 中写入一个文本文件，使用程序名称及其路径命名（在本例中为 `opt.google-chrome.google-chrome`，该程序直接从 Google [www.google.com/chrome/?platform=linux] 安装的，因此本示例所使用的系统上没有预装 AppArmor）。你可以根据需要编辑该文本文件，如果你想从投诉模式（complain mode）切换到强制模式（enforce mode），则必须这样做。

当你有一组涵盖了你所需的配置时，这些是你将经常使用的命令：

- start：按照如下方式使用 start 命令：
```
matthew@semour-$ sudo service apparmor start
```
- stop：按照如下方式使用 stop 命令：
```
matthew@semour-$ sudo service apparmor stop
```

## 412 第20章 保护你的机器安全

reload：按照如下方式使用 reload 命令：

```
matthew@seymour:- sudo service apparmor reload (or restart)
```

show status：按照如下方式使用 show status 命令：

```
matthew@seymour:- sudo service apparmor status
```
