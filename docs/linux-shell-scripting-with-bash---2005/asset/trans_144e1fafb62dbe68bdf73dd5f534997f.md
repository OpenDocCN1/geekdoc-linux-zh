
## Bash 选项

### 表 C.1 shopt 选项

| 选项 | 默认值 | 描述 |
| :------- | :------- | :------- |
| `-o allelexport` | 关闭 | 所有被修改或创建的变量都会被导出。 |
| `-o braceexpand` | 开启 | Shell 执行花括号展开。 |
| `cdable_vars` | 关闭 | 内置的 `cd` 命令假设未识别的目录是包含目录路径的变量。 |
| `cdspell` | 关闭 | 检查 `cd` 路径中目录部分的拼写错误。 |
| `checkhash` | 关闭 | 在尝试路径搜索以查找要运行的命令之前，验证命令查找表中的命令是否仍然存在。 |
| `checkwinsize` | 关闭 | 确定在每个命令执行后显示窗口是否已调整大小。 |
| `cmdhist` | 开启 | 允许多行历史命令编辑。 |
| `dotglob` | 关闭 | 允许在路径名展开中包含 `.files`。 |
| `-o emacs` | 关闭 | 使用 Emacs 风格的行编辑键。 |
| `-o errexit` | 关闭 | 如果命令以非零状态退出，则立即退出。 |
| `execfail` | 关闭 | 当内置的 `exec` 命令无法执行某个命令时，脚本会失败。 |
| `expand_aliases` | 开启 | 允许使用别名。 |
| `extglob` | 关闭 | 为文件名启用扩展模式匹配功能。 |
| `-o hashall` | 开启 | 记住命令查找时的位置。 |
| `histappend` | 关闭 | 命令历史追加到历史文件，而不是覆盖它。 |
| `histredit` | 关闭 | 允许用户编辑失败的历史替换。 |
| `-o histexpand` | 开启 | 启用 `!` 风格的历史替换。 |
| `-o history` | 开启 | 启用命令历史。 |
| `histverify` | 关闭 | 历史替换可以被进一步编辑。 |
| `hostcomplete` | 开启 | 完成包含 `@` 的主机名。 |
| `huponexit` | 关闭 | 当此脚本退出时，向所有仍在运行的作业发送挂起信号。 |
| `-o ignoreeof` | 关闭 | 确保交互式 shell 在读取文件结束时不会退出。 |
| `interactive-comments` | 开启 | 允许在交互式命令中出现注释。 |
| `-o keyword` | 关闭 | 所有赋值参数都被放入命令的环境中，而不仅仅是那些位于命令名称之前的参数。 |
| `lithist` | 关闭 | 包含多个命令的行会被拆分，并作为单独的命令存储在命令历史中。 |
| `mailwarn` | 关闭 | 当有新材料到达且处于 shell 提示符时，通知用户。 |
| `-o monitor` | 开启 | 启用作业控制。 |
| `no_empty_cmd_completion` | 关闭 | 不允许在空行上进行命令补全。 |
| `nocaseglob` | 关闭 | 在模式匹配文件名时忽略大小写。 |
| `-o noclobber` | 关闭 | 如果已设置，则不允许通过输出重定向覆盖现有的常规文件。 |
| `-o noexec` | 关闭 | 读取命令但不执行它们。 |
| `-o noglob` | 关闭 | 禁用文件名生成（`*globbing*`）。 |
| `-o notify` | 关闭 | 立即通知用户作业终止。 |
| `-o nounset` | 关闭 | 在替换时，将未设置的变量视为错误。 |
| `nullglob` | 关闭 | 不匹配任何内容的模式返回空字符串，而不是其本身。 |
| `-o onecmd` | 关闭 | 读取并执行一条命令后退出。 |
| `-o physical` | 关闭 | 如果已设置，在执行更改当前目录的命令（如 `cd`）时，不跟随符号链接。 |
| `-o posix` | 关闭 | 符合 POSIX 1003.2 标准。 |
| `-o privileged` | 关闭 | 每当实际用户 ID 和有效用户 ID 不匹配时开启。禁用处理 `*$ENV*` 文件和导入 shell 函数。关闭此选项会导致有效 uid 和 gid 被设置为实际 uid 和 gid。 |
| `progcomp` | 开启 | 启用可编程补全。 |
| `shoptvars` | 开启 | 处理提示字符串中的变量和参数。 |
| `restricted_shell` | - | 如果 shell 是受限 shell，则为开启状态。此选项是只读的。 |
| `shift_verbose` | 关闭 | 当没有剩余参数可 shift 时返回错误。 |
| `sourcepath` | 开启 | 使用 `PATH` 变量查找 `.` 或 `source` 命令的脚本。 |
| `-o verbose` | 关闭 | 在读取时打印 shell 输入行。 |
| `-o vi` | 关闭 | 使用 vi 风格的行编辑键。 |
| `xpg_echo` | 关闭 | 内置命令 `echo` 默认处理转义序列。 |
| `-o xtrace` | 关闭 | 在执行时打印命令及其参数。 |

### 表 C.2 Bash set 开关

| 开关 | 描述 |
| :--- | :--- |
| `-a` | 等同于 `allexport` |
| `-b` | 等同于 `notify` |
| `-e` | 等同于 `errexit` |
| `-f` | 等同于 `noglob` |
| `-h` | 等同于 `hashall` |
| `-I` | 强制 shell 为“交互式”。交互式 shell 在启动时始终读取 `~/.bashrc` |
| `-k` | 等同于 `keyword` |
| `-m` | 等同于 `monitor` |
| `-n` | 等同于 `noexec` |
| `-o option` | 修改 shopt 选项（等同于 `shopt -o`） |
| `-p` | 等同于 `privileged` |
| `-t` | 等同于 `oncmd` |
| `-u` | 等同于 `nounset` |
| `-v` | 等同于 `verbose` |
| `-x` | 等同于 `xtrace` |
| `-B` | 等同于 `braceexpand` |
| `-C` | 等同于 `noclobber` |
| `-H` | 等同于 `histexpand` |
| `-P` | 等同于 `physical` |

## 错误代码

以下列表包含错误代码的 C 语言缩写形式、错误代码的数值值以及对该错误的简短描述。

| **C 名称** | **数值** | **描述** |
| --- | --- | --- |
| `EPERM` | 1 | 操作不被允许 |
| `ENOENT` | 2 | 没有那个文件或目录 |
| `ESRCH` | 3 | 没有那个进程 |
| `EINTR` | 4 | 系统调用被中断 |
| `EIO` | 5 | I/O 错误 |
| `ENXIO` | 6 | 没有那个设备或地址 |
| `E2BIG` | 7 | 参数列表过长 |
| `ENOEXEC` | 8 | 执行格式错误 |
| `EBADF` | 9 | 无效的文件描述符 |
| `ECHILD` | 10 | 没有子进程 |
| `EAGAIN` | 11 | 请再试一次 |
| `ENOMEM` | 12 | 内存不足 |
| `EACCES` | 13 | 权限被拒绝 |
| `EFAULT` | 14 | 无效的地址 |
| `ENOTBLK` | 15 | 需要块设备 |
| `EBUSY` | 16 | 设备或资源忙 |
| `EEXIST` | 17 | 文件已存在 |
| `EXDEV` | 18 | 跨设备链接 |
| `ENODEV` | 19 | 没有那个设备 |
| `ENOTDIR` | 20 | 不是目录 |
| `EISDIR` | 21 | 是一个目录 |
| `EINVAL` | 22 | 无效的参数 |
| `ENFILE` | 23 | 文件表溢出 |
| `EMFILE` | 24 | 打开的文件过多 |
| `ENOTTY` | 25 | 不是 tty 设备 |
| `ETXTBSY` | 26 | 文本文件忙 |
| `EFBIG` | 27 | 文件太大 |
| `ENOSPC` | 28 | 设备上没有剩余空间 |
| `ESPIPE` | 29 | 非法的 seek 操作 |
| `EROFS` | 30 | 只读文件系统 |
| `EMLINK` | 31 | 链接过多 |
| `EPIPE` | 32 | 管道破裂 |
| `EDOM` | 33 | 数学参数超出定义域 |
| `ERANGE` | 34 | 数学结果无法表示 |
| `EDEADLK` | 35 | 资源死锁可能会发生 |
| `ENAMETOOLONG` | 36 | 文件名太长 |
| `ENOLCK` | 37 | 没有可用的记录锁 |
| `ENOSYS` | 38 | 功能未实现 |
| `ENOTEMPTY` | 39 | 目录不为空 |
| `ELOOP` | 40 | 遇到了过多的符号链接 |
| `EMOUNTDBLOCK` | - | 等同于 `EAGAIN` |
| `ENMSG` | 42 | 没有所需类型的消息 |
| `EIDRM` | 43 | 标识符已被移除 |
| `ECHRNG` | 44 | 通道号超出范围 |
| `EL2NSYNC` | 45 | 第 2 级未同步 |
| `EL3HLT` | 46 | 第 3 级已停止 |
| `EL3RST` | 47 | 第 3 级已重置 |
| `ELNRNG` | 48 | 链路号超出范围 |
| `EUNATCH` | 49 | 协议驱动未附加 |
| `ENOCSI` | 50 | 没有可用的 CSI 结构 |
| `EL2HKT` | 51 | 第 2 级已停止 |
| `EBADE` | 52 | 无效交换 |
| `EBAAD` | 53 | 无效的请求描述符 |
| `EXFULL` | 54 | 交换已满 |
| `ENOANO` | 55 | 没有 anode |
| `EBADRPC` | 56 | 无效的请求代码 |
| `EBADSLT` | 57 | 无效的槽位 |
| `EDEADLOCK` | - | 等同于 `EDEADLK` |
| `EBFONT` | 59 | 无效的字体文件格式 |
| `ENOSTR` | 60 | 设备不是流 |
| `ENODATA` | 61 | 没有可用数据 |
