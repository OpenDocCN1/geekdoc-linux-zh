

```bash
example# /usr/krb5/bin/ktutil
ktutil: rkt /etc/krb5/krb5.keytab
ktutil: list
slot KVNO Principal
---------------------
1 8 host/vail@ACME.COM
2 5 host/denver@ACME.COM
ktutil: delete 2
ktutil: l
slot KVNO Principal
---------------------
1 8 host/vail@ACME.COM
ktutil: wkt /tmp/krb5.keytab
ktutil: q
example# mv /tmp/krb5.keytab /etc/krb5/krb5.keytab
example#
```

## 文件 (Files)

/etc/krb5/krb5.keytab
密钥beros（Kerberos）客户端的密钥表（keytab）文件。

/etc/krb5/krb5.conf
Kerberos 配置文件。

## 属性 (Attributes)

请查看 attributes(5) 以获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
|可用性 | SUNwkrbu |

## 参见 (See Also)

SEAM(5)

## last — 显示登录和注销信息

# 概要 (Synopsis)

```
/usr/bin/last [-a] [-n number] [-number] [-f filename] [name] [tty]... 新！
```

# 描述 (Description)

last 命令用于显示用户和终端的登录及注销信息。last 命令查找 /var/adm/wtmpx 文件，该文件记录了所有的登录和退出。你可以使用参数来指定感兴趣的用户或终端名称。如果你指定了多个参数，将打印适用于参数的信息。例如，`last root console` 会列出 root 的所有会话以及控制终端上的所有会话。last 显示指定用户和终端的会话，按时间顺序排序，指示会话开始的时间、持续时间以及发生会话的终端。last 还指示会话是进行中还是由于重启被中断的。

伪用户 reboot 在系统重启时登录。因此，以下示例显示了重启之间的平均时间。

```bash
castle last reboot
reboot system boot Thu Mar 4 11:10
reboot system boot Thu Mar 4 07:35
reboot system boot Wed Mar 3 18:40
```

```
wtmp begins Wed Mar 3 18:40
castle%
```

不带参数的 last 会按反序显示所有登录和注销的记录，如下例所示。

```bash
castle% last
winsor  console :0 Thu Mar 4 11:13 still logged in
reboot  system boot Thu Mar 4 11:10
winsor  console :0 Thu Mar 4 07:38 - 08:46 (01:07)
reboot  system boot Thu Mar 4 07:35
root     console :0 Wed Mar 3 19:55 - 19:55 (00:00)
winsor  console :0 Wed Mar 3 19:52 - 19:54 (00:02)
winsor  console :0 Wed Mar 3 19:51 - 19:52 (00:00)
root     console :0 Wed Mar 3 18:44 - 19:51 (01:06)
root     console :0 Wed Mar 3 18:43 - 18:43 (00:00)
reboot  system boot Wed Mar 3 18:40
```

如果 last 被中断，它将指示在 /var/adm/wtmpx 中的搜索进度。如果通过退出信号（由 Control-\ 产生）中断，last 将指示搜索进度并继续搜索。

# 选项 (Options)

- -a 在最后一列显示主机名。
- -n number|number
> 将显示的的条目数量限制为 `number` 指定的数量。这些选项的功能是等价的；`-number` 选项仅作为过渡工具提供，将在未来的版本中移除。
- -f filename 使用指定的文件作为计数文件代替 /var/adm/wtmpx。

## 环境变量 (Environment Variables)

日期和时间格式基于 `LC_ALL`、`LC_TIME` 或 `LANG` 环境指定的本地语言，其优先级顺序如下。

## 文件 (Files)

/var/adm/wtmpx

计数文件。

## 属性 (Attributes)

请查看 attributes(5) 以获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
|可用性 | SUNWesu |

## lastcomm

 参见
utmpx(4), attributes(5)

## lastcomm - 反序显示最后执行的命令

# 概要 (Synopsis)

```
/usr/bin/lastcomm [-f file] [-x] [command-name]... [user-name]... (terminal-name)...
```

# 描述 (Description)

lastcomm 命令显示存储在 /var/adm/pacct 文件中的之前执行的计数命令信息。不带参数的 lastcomm 显示当前计数文件生命周期内记录的所有命令。如果你指定了参数，lastcomm 只显示与 `command-name`、`user-name` 或 `terminal-name` 匹配的条目。

如果启用了扩展计数，lastcomm 会尝试从扩展进程计数文件中获取数据，并记录适当的数据 (acct(1M))（新！）。如果启用了标准进程计数，lastcomm 从当前标准计数文件 (acct(2)) 获取数据。

如果 terminal-name 为 -，则该进程没有控制 TTY。该进程可能是在启动期间执行的。如果 terminal-name 为 ??，则无法将控制 TTY 解析为可打印名称。

对于每个进程条目，lastcomm 显示以下信息：

- * 调用该进程时的命令名。
- 一个或多个指示进程特殊信息的标志位。这些标志位具有以下含义：
  * F 进程执行了 fork 但没有执行 exec。
  * S 进程作为 setuid 程序运行。
- 运行该进程的用户名。
- 用户登录时所在的终端（如果适用）。
- 进程使用的 CPU 时间（秒）。
- 进程退出的日期和时间。

# 选项 (Options)

- -f file 使用文件作为计数数据的源。文件可以是扩展进程计数文件，也可以是标准进程计数文件。Solaris 8 版本新功能。
- -x 使用当前激活的扩展进程计数文件。如果扩展进程计数未激活，lastcomm 将产生输出。Solaris 8 版本新功能。

## 示例 (Examples)

以下示例显示了重启之间的平均时间。

```bash
castle last reboot
reboot system boot Thu Mar 4 11:10
reboot system boot Thu Mar 4 07:35
reboot system boot Wed Mar 3 18:40
```

```
wtmp begins Wed Mar 3 18:40
castle%
```

不带参数的 last 按反序显示所有登录和注销的记录，如下例所示。

```bash
castle% last
winsor  console :0 Thu Mar 4 11:13 still logged in
reboot  system boot Thu Mar 4 11:10
winsor  console :0 Thu Mar 4 07:38 - 08:46 (01:07)
reboot  system boot Thu Mar 4 07:35
root     console :0 Wed Mar 3 19:55 - 19:55 (00:00)
winsor  console :0 Wed Mar 3 19:52 - 19:54 (00:02)
winsor  console :0 Wed Mar 3 19:51 - 19:52 (00:00)
root     console :0 Wed Mar 3 18:44 - 19:51 (01:06)
root     console :0 Wed Mar 3 18:43 - 18:43 (00:00)
reboot  system boot Wed Mar 3 18:40
```

