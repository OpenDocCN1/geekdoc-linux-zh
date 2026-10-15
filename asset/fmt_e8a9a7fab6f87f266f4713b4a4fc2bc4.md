
```bash
#!/usr/bin/bash
{
  echo -e "\n- Start remediation - logfiles have appropriate permissions and ownership"
  find /var/log -type f | while read -r fname; do
    bname=$(basename "$fname")
    case "$bname" in
      lastlog.* | wtmp | wtmp.* | btmp | btmp.*)
        stat -lc "%a" "$fname" | grep -P -- '^\h*[0,2,4,6][0,2,4,6],[0,4]*\h$$' && echo -e " changing mode on \"$fname\" && chmod u-x,o-w "$fname"
        stat -lc "%U" "$fname" | grep -P -- '^\h*(root)\h$$' && echo -e " changing group on \"$fname\" && chroot "$fname"
        stat -lc "%U" "$fname" | grep -P -- '^\h*(utmp)\h$$' && echo -e ""
        echo -e " changing group on \"$fname\" && chroot "$fname"
      *auth.log)
        stat -lc "%a" "$fname" | grep -P -- '^\h*[0,2,4,6][0,2,4,6],[0,4]*\h$$' && echo -e " changing mode on \"$fname\" && chmod u-x,o-w "$fname"
        stat -lc "%U" "$fname" | grep -P -- '^\h*(syslog)\h$$' && echo -e ""
        echo -e " changing owner on \"$fname\" && chroot "$fname"
        stat -lc "%G" "$fname" | grep -P -- '^\h*(root)\h$$' && echo -e ""
        echo -e " changing group on \"$fname\" && chroot "$fname"
      sssd)
        stat -lc "%a" "$fname" | grep -P -- '^\h*[0,2,4,6][0,2,4,6],[0,4]*\h$$' && echo -e " changing mode on \"$fname\" && chmod u-x,o-w "$fname"
        stat -lc "%U" "$fname" | grep -P -- '^\h*(SSSD)\h$$' && echo -e ""
        echo -e " changing owner on \"$fname\" && chroot "$fname"
        stat -lc "%G" "$fname" | grep -P -- '^\h*(root)\h$$' && echo -e ""
        echo -e " changing group on \"$fname\" && chroot "$fname"
      gdm|g3dm)
        stat -lc "%a" "$fname" | grep -P -- '^\h*[0,2,4,6][0,2,4,6],[0,4]*\h$$' && echo -e " changing mode on \"$fname\" && chmod u-x,o-w "$fname"
        stat -lc "%U" "$fname" | grep -P -- '^\h*(root)\h$$' && echo -e ""
        echo -e " changing owner on \"$fname\" && chroot "$fname"
        stat -lc "%G" "$fname" | grep -P -- '^\h*(root)\h$$' && echo -e ""
        echo -e " changing group on \"$fname\" && chroot "$fname"
      *,journal)
        stat -lc "%a" "$fname" | grep -P -- '^\h*[0,2,4,6][0,4]*\h$$' && echo -e " changing mode on \"$fname\" && chmod u-x,o-w "$fname"
        stat -lc "%U" "$fname" | grep -P -- '^\h*(root)\h$$' && echo -e ""
        echo -e " changing owner on \"$fname\" && chroot "$fname"
        stat -lc "%G" "$fname" | grep -P -- '^\h*(systemd)\h$$' && echo -e ""
        echo -e " changing group on \"$fname\" && chroot "$fname"
      *)
        stat -lc "%a" "$fname" | grep -P -- '^\h*[0,2,4,6][0,4]*\h$$' && echo -e " changing mode on \"$fname\" && chmod u-x,o-w "$fname"
        stat -lc "%U" "$fname" | grep -P -- '^\h*(syslog)\h$$' && echo -e ""
        echo -e " changing owner on \"$fname\" && chroot "$fname"
        stat -lc "%G" "$fname" | grep -P -- '^\h*(root)\h$$' && echo -e ""
        echo -e " changing group on \"$fname\" && chroot "$fname"
        esac
  done
  stat -Lc "%G" "$fname" | grep -Pq '^\h*(adm|root)\h$$' && echo -e "changing group on \$fname && chroot \$fname"
    esac
done
echo -e "- End remediation - logfiles have appropriate permissions and ownership"
```

注意：可能还需要对权限错误的日志软件进行配置。如果服务记录日志到其他位置，请确保日志文件具有正确的权限。

## 5 访问与授权

### 5.1 配置基于时间的调度器

`cron` 是一种基于时间的任务调度器，用于在固定的时间、日期或间隔运行任务、命令或脚本。`at` 提供在指定的日期和小时后执行命令或脚本的能力。

说明：

- 存在其他调度任务的方法，例如 `systemd` timers。如果使用了其他方法，应根据本地站点策略进行安全防护。
- `systemd` timers 是以 `.timer` 结尾的文件，用于控制 `.service` 文件或事件。
- `Timer` 可以作为 `cron` 和 `at` 的替代方案。
- `Timer` 内置支持日历时间事件、单调时间事件，并可以异步运行。
- 如果没有安装 `cron` 和 `at`，可以跳过此节。

#### 5.1.1 确保 cron 守护进程已启用并运行

适用范围：

- 1级服务器
- 1 级工作站

说明：

`cron` 守护进程用于在系统上执行批处理任务。注意：存在其他调度任务的方法，例如 `systemd` timers。如果使用了其他方法，应根据本地站点策略进行安全防护。

理由：

虽然系统中可能没有运行的用户任务，但系统确实有需要运行的安全监控维护任务，且使用 `cron` 执行它们。

审计：

运行以下命令验证 `cron` 是否启用：

```bash
# systemctl is-enabled cron
enabled
```

运行以下命令验证 `cron` 正在运行：

```bash
# systemctl status cron | grep 'Active: active (running)'
Active: active (running) since <Day Date>
```

修复：

运行以下命令启用并启动 `cron`：

```bash
# systemctl --enable cron
```

MITRE ATT&CK 映射：

| 技术 / 子技术 | 战术 | 缓解措施 |
|---|---|---|
| T1562, T1562.001 | TA0005 | M1018 |

#### 5.1.2 确保 /etc/crontab 的权限已配置

适用范围：

- 1级服务器
- 1 级工作站

说明：

`/etc/crontab` 文件用于 `cron` 控制自身的任务。此项中的命令确保 root 是文件的用户和组所有者，并且所有者可以访问文件。

注意：存在其他调度任务的方法，例如 `systemd` timers。如果使用了其他方法，应根据本地站点策略进行安全防护。

理由：

此文件包含由 `cron` 运行的系统任务的信息。对这些文件的写入权限可能让无权用户提升权限。读取权限可能让用户了解系统中运行的任务，并提供获得授权访问的方法。

审计：

运行以下命令并验证 Uid 和 Gid 均为 0/root，且 Access 未授予组权限：

```bash
# stat /etc/crontab
Access: (0600/-rw-------) Uid: ( 0/ root) Gid: ( 0/ root)
```

其他信息：

`NIST SP 800-53 Rev. 5`:

- AC-3
- MP-2

`CIS Controls`：

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | 3.3 配置数据控制列表 | 根据用户的认知需要配置数据控制列表。将数据控制列表（称为访问权限）应用于本地和远程文件系统、数据库和应用程序。 | | | |
| v7 | 14.6 通过访问列表保护信息 | 通过文件系统、网络共享、声明或应用程序特定的访问控制列表保护存储在系统上的所有信息。这些控制将强制只有授权的人员根据职责访问信息的原则。 | | | |

修复：

运行以下命令设置 `/etc/crontab` 的所有者和权限：

```bash
# chown root:root /etc/crontab
# chmod og-rwx /etc/crontab
```

`CIS 控制`：

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | **3.3 配置数据访问控制列表** 根据用户的“知情需要”配置数据访问控制列表。将数据访问控制列表（也称为访问权限）应用于本地和远程文件系统、数据库和应用程序。 | | | | |
| v7 | **14.6 通过访问控制列表保护信息** 使用文件系统、网络共享、声明、应用程序或数据库特定的访问控制列表来保护存储在系统上的所有信息。这些控制将强制执行原则：即只有授权的人员根据其职责范围内的访问信息需求才能访问该信息。 | | | | |

`MITRE ATT&CK 映射`：

| 技术 / 子技术 | 战术 | 缓解措施 |
|---|---|---|
| T1053, T1053.003 | TA0002, TA0007 | M1018 |

#### 5.1.3 确保 /etc/cron.hourly 权限已配置（自动）

配置适用性：

- 级别 1 - 服务器
- 级别 1 - 工作站

描述：

此目录包含每小时运行一次的系统 `cron` 任务。目录中的文件无法通过 `crontab` 命令操作，而是由系统管理员使用文本编辑器进行编辑。以下命令将读/写和搜索权限限制为 root 用户和组，防止普通用户访问此目录。

> 注意：还存在其他方法（如 `systemd` 定时器）用于调度任务。如果使用了其他方法，应该删除 `cron`，并根据本地站点策略对替代方法进行安全保护。

原理：

为非特权用户授予此目录的写权限可能会为他们提供获取未经授权提升权限的手段。为此目录授予读取权限可能会让无权限用户了解如何获取提升权限或绕过审计控制。

审计：

运行以下命令并验证 Uid 和 Gid 均为 0/root，且 Access 未向组或其他授予权限：

```bash
# stat /etc/cron.hourly/
Access: (0700/drwx------) Uid: ( 0/root) Gid: ( 0/root)
```

修复：

运行以下命令设置 `/etc/cron.hourly` 目录的所有者和权限：

```bash
# chown root:root /etc/cron.hourly/
# chmod og-rwx /etc/cron.hourly/
```

`CIS 控制`：

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
| --- | --- | --- | --- | --- |
| v8 | 3.3 配置数据访问控制列表：根据用户的“知情需要”配置数据访问控制列表。将数据访问控制列表（也称为访问权限）应用于本地和远程文件系统、数据库和应用程序。 | | ● | ● |
| v7 | 14.6 通过访问控制列表保护信息：使用文件系统、网络共享、声明、应用程序或数据库特定的访问控制列表来保护存储在系统上的所有信息。这些控制将强制执行原则：即只有授权的人员根据其职责范围内的访问信息需求才能访问该信息。 | | ● | ● |

`MITRE ATT&CK 映射`：

| 技术 / 子技术 | 战术 | 缓解措施 |
| --- | --- | --- |
| T1053, T1053.003 | TA0002, TA0007 | M1018 |

#### 5.1.4 确保 /etc/cron.daily 权限已配置（自动）

配置适用性：

- 级别 1 - 服务器
- 级别 1 - 工作站

描述：

`/etc/cron.daily` 目录包含每天运行一次的系统 `cron` 任务。目录中的文件无法通过 `crontab` 命令操作，而是由系统管理员使用文本编辑器进行编辑。以下命令将读/写和搜索权限限制为 root 用户和组，防止普通用户访问此目录。

> 注意：还存在其他方法（如 `systemd` 定时器）用于调度任务。如果使用了其他方法，应该删除 `cron`，并根据本地站点策略对替代方法进行安全保护。

原理：

为非特权用户授予此目录的写权限可能会为他们提供获取未经授权提升权限的手段。为此目录授予读取权限可能会让无权限用户了解如何获取提升权限或绕过审计控制。

审计：

运行以下命令并验证 Uid 和 Gid 均为 0/root，且 Access 未向组或其他授予权限：

```bash
# stat /etc/cron.daily/
Access: (0700/drwx------) Uid: ( 0/root) Gid: ( 0/root)
```

修复：

运行以下命令设置 `/etc/cron.daily` 目录的所有者和权限：

```bash
# chown root:root /etc/cron.daily/
# chmod og-rwx /etc/cron.daily/
```

`CIS 控制`：

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | 3.3 配置数据访问控制列表 根据用户的“知情需要”配置数据访问控制列表。将数据访问控制列表（也称为访问权限）应用于本地和远程文件系统、数据库和应用程序。 | ● | ● |
| v7 | 14.6 通过访问控制列表保护信息 使用文件系统、网络共享、声明、应用程序或数据库特定的访问控制列表来保护存储在系统上的所有信息。这些控制将强制执行原则：即只有授权的人员根据其职责范围内的访问信息需求才能访问该信息。 | ● | ● |

`MITRE ATT&CK 映射`：

| 技术 / 子技术 | 战术 | 缓解措施 |
|---|---|---|
| T1053, T1053.003 | TA0002, TA0007 | M1018 |

#### 5.1.5 确保 /etc/cron.weekly 权限已配置（自动）

配置适用性：

- 级别 1 - 服务器
- 级别 1 - 工作站

描述：

`/etc/cron.weekly` 目录包含每周运行一次的系统 `cron` 任务。目录中的文件无法通过 `crontab` 命令操作，而是由系统管理员使用文本编辑器进行编辑。以下命令将读/写和搜索权限限制为 root 用户和组，防止普通用户访问此目录。

> 注意：还存在其他方法（如 `systemd` 定时器）用于调度任务。如果使用了其他方法，应该删除 `cron`，并根据本地站点策略对替代方法进行安全保护。

原理：

为非特权用户授予此目录的写权限可能会为他们提供获取未经授权提升权限的手段。为此目录授予读取权限可能会让无权限用户了解如何获取提升权限或绕过审计控制。

审计：

运行以下命令并验证 Uid 和 Gid 均为 0/root，且 Access 未向组或其他授予权限：

```bash
# stat /etc/cron.weekly/
Access: (0700/drwx------) Uid: ( 0/root) Gid: ( 0/root)
```

修复：

运行以下命令设置 `/etc/cron.weekly` 目录的所有者和权限：
