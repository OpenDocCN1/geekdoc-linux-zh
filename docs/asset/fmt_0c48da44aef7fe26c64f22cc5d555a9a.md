
```bash
# cd /usr/local/etc && cp portsnap.conf.sample portsnap.conf
```

### A.6.4 首次运行 Portsnap

第一次运行 `portsnap(8)` 时，它需要下载整个 ports 树的压缩快照到 `/var/db/portsnap/`（如果从 Ports 安装，则是 `/usr/local/portsnap/`）。在2006年初，这约为 41 MB。

```bash
# portsnap fetch
```

一旦下载快照，可以将 ports 树的“实时”副本提取到 `/usr/ports/`。如果该目录已经创建了 ports 树（例如通过 CVS 创建），则这是必要的，因为它建立了一个基准，供 `portsnap` 之后确定 ports 树的哪些部分需要更新。

```bash
# portsnap extract
```

> 注意：默认安装时不会创建 `/usr/ports`。如果你运行 FreeBSD 6.0-RELEASE，应在使用 `portsnap` 之前创建它。在较新版本的 FreeBSD 或 Portsnap 中，此操作将在第一次使用 `portsnap` 命令时自动完成。

### A.6.5 更新 Ports Tree

在下载并提取 ports 树快照到 `/usr/ports/` 后，更新 ports 树包含两个步骤：获取压缩快照，以及使用它们更新实时 ports 树。这两个步骤可以由 `portsnap` 指定为单个命令：

```bash
# portsnap fetch
```

> 注意：某些旧版本的 `portsnap` 不支持此语法；如果失败，请尝试：

```bash
# portsnap fetch
# portsnap update
```

### A.6.6 通过 cron 运行 Portsnap

为了避免“瞬间流量”访问 Portsnap 服务器引起的问题，`portsnap fetch` 不通过 `cron(8)` 任务运行。相反，有一个特殊的 `portsnap cron` 命令，它在获取更新前会随机等待长达 3600 秒。强烈建议不要从 cron 任务运行 `portsnap update`，因为如果它在构建 port 的同时发生可能会导致严重问题。但是，通过向 `portsnap` 传递 `-I` 标志来更新 `INDEX` 文件是安全的。在 `/etc/crontab` 中添加以下行，将使 `portsnap` 更新其快照和 `INDEX` 文件，如果有任何已安装的 port 过期，它将发送邮件：

```
0 3 * * root portsnap -I cron update && pkg_version -V
```
