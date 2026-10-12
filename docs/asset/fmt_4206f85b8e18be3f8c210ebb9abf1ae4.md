
该发行版附带几个示例`tigerrc`文件。`tigerrc-all`文件配置为执行所有检查。你应该将其中一个示例`tigerrc`文件复制到构建目录顶层的`tigerrc`中，并根据你的喜好进行编辑。某些检查的运行时间比其他检查长。表 13.6 列出了你可以在`tigerrc`文件中使用的关键字和值列表。

### 表 13.6 `tigerrc` 关键字、值和描述

| 关键字 | 值 | 描述 |
| --- | --- | --- |
| `Tiger_Check_PASSWD` | Y 或 N | 启用或禁用对`passwd`文件的问题检查（`check_passwd`脚本）；通常运行速度很快。 |
| `Tiger_Check_GROUP` | Y 或 N | 启用或禁用对`groups`文件的检查（`check_group`脚本）；通常运行速度很快。 |
| `Tiger_Check_ACCOUNTS` | Y 或 N | 启用或禁用对密码文件和用户账户中文件的异常检查（`check_accounts`脚本）；所需时间取决于用户数量。 |
| `Tiger_Check_RHOSTS` | Y 或 N | 启用或禁用对用户`.rhosts`文件的策略违规检查（`check_rhosts`脚本）；所需时间取决于用户数量。 |
| `Tiger_Check_NETRC` | Y 或 N | 启用或禁用对用户`.netrc`文件的检查（`check_netrc`脚本）；所需时间取决于用户数量。 |
| `Tiger_Check_ALIASES` | Y 或 N | 启用或禁用对系统别名文件的检查（`check_aliases`脚本）；通常运行速度很快。 |
| `Tiger_Check_CRON` | Y 或 N | 启用或禁用对用户`cron`任务的检查（`check_cron`脚本）；通常运行速度很快。 |
| `Tiger_Check_MOTD` | Y 或 N | 启用或禁用对`/etc/motd`文件的策略违规检查（`check_motd`脚本）；通常运行速度很快。 |
| `Tiger_Check_DOS` | Y 或 N | 启用或禁用对目录权限和所有权的检查，以验证其与策略的一致性（`check_dos`脚本）。 |
| `Tiger_Check_FILES` | Y 或 N | 启用或禁用对与其目录所有者相同的全球可读文件的检查，以验证其与策略的一致性（`check_files`脚本）；通常运行速度很快。 |
| `Tiger_Check_LINKS` | Y 或 N | 启用或禁用对符号链接和硬链接的检查，以验证其与策略的一致性（`check_links`脚本）；通常运行速度很快。 |
| `Tiger_Check_LOG` | Y 或 N | 启用或禁用对日志文件的策略违规检查（`check_log`脚本）；通常运行速度很快。 |
| `Tiger_Check_SUIDSGID` | Y 或 N | 启用或禁用对`SUID/SGID`文件的检查，以验证其与策略的一致性（`check_suidsgid`脚本）。 |
| `Tiger_Check_SHELLS` | Y 或 N | 启用或禁用对`/etc/shells`文件的检查，以验证其与策略的一致性（`check_shells`脚本）；通常运行速度很快。 |
| `Tiger_Check_TMP` | Y 或 N | 启用或禁用对`/tmp`, `/var/tmp`和`/usr/tmp`文件的检查，以验证其与策略的一致性（`check_tmp`脚本）；通常运行速度很快。 |
| `Tiger_Check_USERS` | Y 或 N | 启用或禁用对`/etc/passwd`文件的检查，以验证其与策略的一致性（`check_users`脚本）；通常运行速度很快。 |
| `Tiger_Check_VERSION` | Y 或 N | 启用或禁用`Tiger`版本号的显示（`check_version`脚本）；通常运行速度很快。 |
| `Tiger_Check_WARN` | Y 或 N | 启用或禁用警告的显示（`check_warn`脚本）；通常运行速度很快。 |

### 表 13.6 `tigerrc` 关键字、值和描述（续）

| 关键字 | 值 | 描述 |
| --- | --- | --- |
| `Tiger_Check_ANONFTP` | Y 或 N | 启用或禁用对匿名`FTP`配置的检查（`check_anonftp`脚本）；通常运行速度很快。 |
| `Tiger_Check_EXPORTS` | Y 或 N | 启用或禁用对导出文件系统的检查（`check_exports`脚本）；通常运行速度很快。 |
| `Tiger_Check_INETD` | Y 或 N | 启用或禁用对系统`inetd`文件的检查（`check_inetd`脚本）；通常运行速度很快。 |
| `Tiger_Check_KNOWN` | Y 或 N | 启用或禁用对已知漏洞的搜索（`check_known`脚本）；通常运行速度很快。 |
| `Tiger_Check_PERMS` | Y 或 N | 启用或禁用对系统目录和主目录权限的检查（`check_perms`脚本）；速度相当快。 |
| `Tiger_Check_SIGNATURES` | Y 或 N | 启用或禁用系统签名与随`tiger`提供的签名数据库中的签名的比较（`check_signatures`脚本）；运行需几分钟。 |
| `Tiger_Check_FILESYSTEM` | Y 或 N | 启用或禁用`find_files`脚本的执行。 |
| `Tiger_Check_PATH` | Y 或 N | 启用或禁用对用户`PATH`中组件的检查，以查找潜在弱点（`check_path`脚本）；对`root`用户速度很快，对其他用户则视情况而定。 |
| `Tiger_Check_EMBEDDED` | Y 或 N | 启用或禁用对可执行文件中嵌入路径的检查，以查找弱点（`check_embedded`脚本）；需几分钟。 |
| `Tiger_Check_SYSTEM` | Y 或 N | 启用或禁用操作系统特定检查的执行。注意：该关键字在`tigerrc-all`中缺失；如果你希望使用它，请将其添加到你的`tigerrc`中。 |
| `Tiger_Show_INFO_Mgs` | Y 或 N | 配置是否显示`tiger`报告中的`INFORMATION`消息。 |

### 表 13.6 `tigerrc` 关键字、值和描述（续）

| 关键字 | 值 | 描述 |
| --- | --- | --- |
| `Tiger_Run_CRACK` | Y 或 N | 启用或禁用调用`Crack`程序（`run_crack`脚本）；运行时间可能很长。（如果设置此项，还需要编辑`site`文件。） |
| `Tiger_Output_Width` | 0 或期望的行长度 | 报告中行的宽度（以字符数计）。默认为 79；0 表示无限制。 |
| `Tiger_CRON_Output_Width` | 0 或期望的行长度 | 当通过`tigercron`运行时，`tiger`生成的输出行的宽度。只需设置一次，不要更改；否则，输出的差异将因格式不同而显示大量变化；0 表示无限制行长度。 |
| `Tiger_Embed_Max_Depth` | 0, 1, 2, 3, ... | 这指在运行`check_embedded`脚本时要使用的递归深度。如果嵌入路径引用了一个文件，则检查每个引用的文件，直到达到递归深度，或者没有更多文件需要检查。较大的递归深度有时可能需要比可用内存更多的内存；如果`check_embedded`挂起，请尝试使用较小的`Max_Depth`值。 |
| `Tiger_Embed_Check_Exec_Only` | Y 或 N | Y 表示仅搜索可执行文件中的嵌入路径；N 表示搜索所有常规文件（包括可执行文件）中的嵌入路径。 |
| `Tiger_Embed_Check_SUID` | Y 或 N | 启用或禁用对`SUID`文件的嵌入路径检查。这可能会花费稍长的时间；文件系统必须先扫描`SUID`文件。 |
| `Tiger_Embed_Report_Exec_Only` | Y 或 N | 检查报告的嵌入文件是否可写或不由`root`拥有。如果设置为 Y，则仅报告可执行文件。使用 N 以除可执行文件外还报告常规文件和目录。目前不报告设备文件。 |
| `Tiger_Embedded_OK_Owners` | 一个或多个 `\|` 用户名 | 允许拥有系统文件的用户名列表。名称以`\|`分隔，中间无空白。由其他用户拥有的文件将被报告。 |

### 表 13.6 `tigerrc` 关键字、值和描述（续）

| 关键字 | 值 | 描述 |
| --- | --- | --- |
| `Tiger_Embedded_OK_Group_Write` | 无值或一个或多个 `\|` 组名 | 允许对系统文件具有写权限的组名列表。名称以`\|`分隔，中间无空白。如果设置，具有组写权限的其他文件将被报告。无值表示没有组应具有写权限。 |
| `Tiger_Check_PATHALL` | Y 或 N | 启用或禁用对所有用户启动文件中`PATH`的检查。 |
