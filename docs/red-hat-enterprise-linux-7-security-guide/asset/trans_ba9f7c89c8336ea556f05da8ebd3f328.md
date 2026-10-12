

cap_fe=0

cap_fe 字段记录文件或目录对象基于文件系统的能力的有效位设置。

cap_fver=0

cap_fver 字段记录文件或目录对象基于文件系统的能力的版本。

## 第4条记录

type=PROCTITLE

type 字段包含记录的类型。在此示例中，PROCTITLE 值指定该记录给出了触发此审计事件的完整命令行，该事件由调用内核的系统调用触发。

```
proctitle=636174002F6574632F7373 82F737368645F636F6E6669677
```

proctitle 字段记录用于调用被分析进程的完整命令行。该字段以十六进制编码形式记录，以防止用户影响审计日志解析器。该文本解码为触发此审计事件的命令。在使用 ausearch 命令搜索审计记录时，使用 -i 或 --interpret 选项可自动将十六进制值转换为其人类可读的等价值。636174002F6574632F737382F737368645F636F6E6669677 值被解释为 x86_64。

上述分析的审计事件仅包含事件可能包含的所有字段的一个子集。有关所有事件字段及其解释的列表，请参见第 B.1 节“审计事件字段”。有关所有事件类型及其解释的列表，请参见第 B.2 节“审计记录类型”。

### 示例 6.6. 额外的 audit.log 事件

以下审计事件记录了 auditd 守护程序的成功启动。ver 字段显示了启动的审计守护程序的版本。

```
type=DAEMON_START msg=audit(1363713609.192:5426): auditd start, ver=2.2 format=raw kernel=2.6.32-358.2.1.el6.x86_64 audit=1000 pid=4979 subj=unconfined_u:system_r:auditd_t:s0 res=success
```

以下审计事件记录了 UID 为 1000 的用户尝试登录为 root 用户失败的情况。

```
type=USER_AUTH msg=audit(136475353.159:24270): user pid=3280 uid=1000 auid=1000 ses=1 subj=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023 msg='op=PAM:authentication acct="root" exe="/bin/su" hostname=? addr=? terminal=pts/0 res=failed'
```

## 6.7. 搜索审计日志文件

ausearch 实用程序允许您搜索审计日志文件中的特定事件。默认情况下，ausearch 搜索 /var/log/audit/audit.log 文件。您可以使用 ausearch 选项 -if file_name 命令指定其他文件。在一个 ausearch 命令中提供多个选项等价于在字段类型之间使用 AND 运算符，并在同一字段类型的多个实例之间使用 OR 运算符。

### 示例 6.7. 使用 ausearch 搜索审计日志文件

要搜索 /var/log/audit/audit.log 文件中的登录失败尝试，请使用以下命令：

```
~]# ausearch --message USER_LOGIN --success no --interpret
```

要搜索所有账户、组和角色更改，请使用以下命令：

```
~]# ausearch -m ADD_USER -m DEL_USER -m ADD_GROUP -m USER_CHAUTHTOK -m DEL_GROUP -m CHGRP_ID -m ROLE_ASSIGN -m ROLE_REMOVE -i
```

要搜索由特定用户执行的所有已记录操作，使用该用户的登录 ID（audit），请使用以下命令：

```
~]# ausearch -ua 1000 -i
```

要搜索从昨天至今的所有失败的系统调用，请使用以下命令：

```
~]# ausearch --start yesterday --end now -m SYSCALL -sv no -i
```

有关所有 ausearch 选项的完整列表，请参见 ausearch(8) 手册页。

## 6.8. 创建审计报告

aureport 实用程序允许您生成针对记录在审计日志文件中的事件的摘要和列式报告。默认情况下，会查询 /var/log/audit/ 目录中的所有 audit.log 文件以创建报告。您可以使用 aureport 选项 -if file_name 命令指定运行报告所针对的其他文件。

### 示例 6.8. 使用 aureport 生成审计报告

要为过去三天（不包括当前示例日期）记录的已记录事件生成报告，请使用以下命令：

```
~]# aureport --start 04/08/2013 00:00:00 --end 04/11/2013 00:00:00
```

要为所有可执行文件事件生成报告，请使用以下命令：

```
~]# aureport -x
```

要为上述可执行文件事件报告生成摘要，请使用以下命令：

```
~]# aureport -x --summary
```

要为所有用户的失败事件生成摘要报告，请使用以下命令：

```
~]# aureport -u --failed --summary -i
```

要为每个系统用户的所有失败登录尝试生成摘要报告，请使用以下命令：

```
~]# aureport --login --summary -i
```

要从搜索用户 ID 1000 的所有文件访问事件的 ausearch 查询生成报告，请使用以下命令：

```
~]# ausearch --start today --loginuid 1000 --raw | aureport -f --summary
```

要为所有被查询的审计文件以及它们包含的事件时间范围生成报告，请使用以下命令：

```
~]# aureport -t
```

有关所有 aureport 选项的完整列表，请参见 aureport(8) 手册页。

## 6.9. 其他资源

有关 Audit 系统的更多信息，请参见以下来源。

### 在线资源

- Linux Audit 文档项目页面：https://github.com/linux-audit/audit-documentation/wiki。

### 已安装的文档

audit 包提供的文档可以在 `/usr/share/doc/audit/` 目录中找到。

### 手册页

- audispd.conf(5)
- auditd.conf(5)
- ausearch-expression(5)
- audit.rules(7)
- audispd(8)
- auditctl(8)
- auditd(8)
- aulast(8)
- aulastlog(8)
- aureport(8)
- asearch(8)
- ausyscall(8)
- autrace(8)
- auvirt(8)

# 第 7 章. 使用 OpenSCAP 进行合规性和漏洞扫描

## 7.1. Red Hat Enterprise Linux 中的安全合规性

合规性审计是一个确定给定对象是否遵循合规性策略中写明的所有规则的过程。合规性策略由安全专家定义，他们指定所需的设置，通常以检查清单的形式，用于在计算环境中使用。

合规性策略在不同组织之间甚至在同一组织内的不同系统之间可能存在很大差异。这些策略之间的差异基于这些系统的用途及其对组织的重要性。自定义软件设置和部署特征也引发了对自定义策略检查清单的需求。

Red Hat Enterprise Linux 提供允许完全自动化合规性审计的工具。这些工具基于安全内容自动化协议（SCAP）标准，旨在自动化调整合规性策略。

### Red Hat Enterprise Linux 7 支持的安全合规性工具

- **SCAP Workbench** – scap-workbench 图形实用程序旨在对单个本地或远程系统执行配置和漏洞扫描。它还可以用于基于这些扫描和评估生成安全报告。
- **OpenSCAP** – openscap 命令行实用程序旨在对本地系统执行配置和漏洞扫描，验证安全合规性内容，并基于这些扫描和评估生成报告和指南。
- **脚本检查引擎 (SCE)** – SCE 是 SCAP 协议的扩展，允许管理员使用脚本语言（如 Bash、Python 或 Ruby）编写其安全内容。SCE 扩展在 openscap-engine-sce 包中提供。
- **SCAP 安全指南 (SSG)** – scap-security-guide 包提供了针对 Linux 系统的最新安全策略集合。指南包括实用加固建议的目录，并在适用时链接到政府要求。该项目弥合了通用策略要求和特定实施指南之间的差距。

如果您需要在远程多个系统上执行自动化合规性审计，您可以利用适用于 Red Hat Satellite 的 OpenSCAP 解决方案。有关更多信息，请参见第 7.8 节“使用 Red Hat Satellite 中的 OpenSCAP”和第 7.10 节“其他资源”。

## 7.2. 定义合规性策略

安全或合规性策略很少从头开始编写。ISO 27000 标准系列、衍生作品和其他来源提供了安全策略模板和实务建议，应该有助于起步。然而，建立信息安全管理计划的组织需要修改策略模板以符合其需求。策略模板应根据其与公司环境的相关性进行选择，然后必须调整该模板，因为要么模板包含无法应用于该组织的内置假设，要么模板明确要求必须做出某些决定。

Red Hat Enterprise Linux 的审计功能基于安全内容自动化协议（SCAP）标准。SCAP 是一组互操作性规范的综合，标准化了软件缺陷和安全配置信息传达的格式和术语，既向

