
# 附录 C • HP-UX 到 Linux 参考表

| HP aCC 选项 | GNU g++ 选项 | 说明 |
| :--- | :--- | :--- |
| `-C` | `-C` | 防止预处理器剥离注释。 |
| `-Aynamic` | `-Wl,-Bdynamic` | 生成动态链接的可执行文件。 |
| `-Dname=[def]` | `-Dname=def` | 为预处理器定义一个符号名称 `name`，由预处理指令 `#define` 定义。 |
| `+d` | `-fno-default-inline` `接近但不完全相同` `-fno-inline` | 防止内联函数的展开。 |
| `+dryrun` | `-###` | 显示传递的选项，但不执行。 |
| `-ext +e` | None | 启用依赖于平台的 C++ 标准扩展。 |
| `-E` | `-E` | 仅对命名的 C++ 文件运行预处理器，并将其结果发送到标准输出 `stdout`。 |
| `-fast` | None | 选择一组优化选项，以在合理的构建时间内获得最佳执行速度。 |
| `-fpeval=precision` | None | 指定用于浮点表达式求值时使用的最小精度。 |
| `-g[0|1]` | `-g[1|2|3]` | 输出不同层次的调试信息。 |
| `-G` | `-pg` | 编译并创建用于 `gprof` 的经过插桩的可执行文件。 |
| `-Idirs` | `-I` | 指明可选的 `-Idirectory` 目录指定规格列表。 |
| `-mt` | `-D_REENTANT -lpthread` | 编译为多线程程序。 |
| `-n` | `-shared -Bshare` | 使链接器产生的程序文件标记为可共享。 |

## HP-UX 到 Linux 参考表

| HP aCC 选项 | GNU g++ 选项 | 说明 |
| :--- | :--- | :--- |
| `-N` | None | 使链接器产生的程序文件标记为不可共享。 |
| `-o outfile` | `-o outfile` | 将编译输出放在 `outfile` 中。 |
| `-O` | `-O2` | 调用优化器执行 2 级优化。 |
| `-p` | `-p` | 编译并创建用于 `prof` 的经过插桩的可执行文件。 |
| `-P` | None | 仅预处理命令行上命名的文件而不调用后续阶段。将结果留在具有后缀 `.i` 的对应文件中。 |
| `-q` | None | 使链接器的输出文件标记为按需加载。 |
| `-Q` | None | 使链接器的程序文件标记为按需加载。 |
| `-r` | `-r` | 在输出文件中保留重定位信息，以供后续重新链接。 |
| `-s` | `-Wl, -s` | 使链接器创建的可执行程序文件剥离符号表信息。 |
| `-S` | `-S` | 编译命名的程序并将汇编语言输出留在具有 `.s` 后缀的对应文件中。 |
| `-symbol` | `-u undefined=symbol` | `name` 是符号名称，其定义已从预处理器中移除。 |
| `-v` | `-v` | 启用详细模式，将编译过程的逐步描述发送到 `stderr`。 |
| `-V` | `--version` | 显示当前编译器和链接器的版本号，如果执行了链接器。 |
| `-w` | `-w` | 抑制所有警告消息。 |

# HP-UX 和 Linux C++ 编译器选项表

| HP aCC 选项 | GNU g++ 选项 | 说明 |
| :--- | :--- | :--- |
| `-W,-ansi_for_scope, [on] [off]` | `-ffor-scope -fno-for-scope` | 启用或禁用 `for` 语句中初始化声明的标准作用域规则 |
| `-W,-koenig_lookup, [on] [off]` | `-ffor-scope -fno-for-scope` | 启用或禁用标准作用域规则 |
| `-Wx,arg1,[argn]` | `-ffor-scope -fno-for-scope` | 启用或禁用标准作用域规则 |
| `-z` | None | 允许按需加载。 |
| `-Z` | None | 允许按需加载。 |
| `+help` | None | 指定异步 I/O。 |
| `+ild` | None | 指定异步链接。 |
| `+noeh` | None | 禁用异常处理。 |
| `+0[init]` | None | 指定初始化检查。 |
| `+sb` | None | 引用标准头文件和库。 |
| `+ftls={static|dynamic}` | None | 指定异步检查。 |
| `+ub` | None | 指定无。 |
| `+uc` | None | 指定无。 |

# HP-UX 到 Linux 参考表

| HP aCC 选项 | GNU g++ 选项 | 说明 |
| :--- | :--- | :--- |
| `-Warg1,[arg2..argn]` | None | 选择性地处理警告 `arg1` 到 `argn`。 |
| `-We` | None | 解释所有错误。 |
| `-Warg1,[arg2..argn]` | None | 选择选择性地处理警告 `arg1` 到 `argn`。 |
| `-Ww` | None | 抑制所有警告。 |

# HP-UX 和 Linux 系统调用对比表

表格 C-3

HP-UX 和 Linux 系统调用对比

| HP-UX 系统调用 | Linux 等效 | 说明 |
| :--- | :--- | :--- |
| `accept` | `accept` | 在套接上接受连接。 |
| `access` | `access` | 确定文件的访问性。 |
| `acct` | None | 启用或禁用进程统计。 |
| `acl` | None | 设置文件的 ACL 信息。 |
| `adjtime` | `adjtime` | 修正时间以同步系统时。 |
| `aio_cancel` | `aio_cancel, aio_cancel64` | 取消异步 I/O 操作。 |
| `aio_error` | `aio_error, aio_error64` | 返回异步 I/O 操作的状态。 |
| `aio_fsync` |  | 同步异步 I/O 操作。 |
| `aio_read` | `aio_read, aio_read64` | 启动异步读取操作。 |
| `aio_reap` | None | 等待多个异步 I/O 请求。 |
| `aio_return` | `aio_return, aio_return64` | 返回异步 I/O 操作状态。 |
| `aio_suspend` | `aio_suspend, aio_suspend64` | 挂起异步 I/O 操作。 |
| `aio_write` | `aio_write, aio_write64` | 启动异步写入操作。 |
| `alarm` | `alarm` | 设置进程闹钟。 |
| `audctl` | None | 启动或停止审计系统；设置或获取审计文件。 |
| `audswitch` | None | 挂起或恢复当前进程的审计。 |

## HP-UX 系统调用 | Linux 等效调用 | 描述

| HP-UX 系统调用 | Linux 等效调用 | 描述 |
| :--- | :--- | :--- |
| `audwrite` | 无 | 为审计进程写入审计记录。 |
| `bind` | `bind` | 将地址绑定到套。 |
| `brk` | `brk` | 更改数据段空间分配。 |
| `chdir` | `chdir` | 更改工作目录。 |
| `chmod` | `chmod` | 更改文件模式访问权限。 |
| `chown` | `chown` | 更改文件的所有者组。 |
| `chroot` |  | 更改根目录。 |
| `clock_getters` | `clock_gettime` | 时钟操作。 |
| `clock_gettime` | `clock_gettime` | 时钟操作。 |
| `clock_settime` | `clock_gettime` | 时钟操作。 |
| `close` | `close` | 关闭文件描述符。 |
| `connect` | `connect` | 在套上发起连接。 |
| `crashcon` | 无 | 配置系统崩溃转储。 |
| `creat` | `creat` — 根据 SUSv3 指定，可能返回 `ENODEV` 代替 `ENOIO` | 创建新文件或重写现有文件。 |
| `creat64` | `create64` | 支持大文件的非 POSIX 标准 API 接口 `HP-UX`。 |
| `dup` | `dup` | 复制打开的文件描述符。 |
| `dup2` | `dup2` | 将打开的文件描述符复制到特定的槽。 |
| `errno` | `errno` 非 API | 系统调错误指示器。 |
| `exec, execl, execle, execlp` | `exec, execl, execle, execlp` | 执行文件。 |
| `execv, execve, execvp` | `execv, execve, execvp` |  |
| `exit` | `exit` | 终止进程。 |
| `fchdir` | `fchdir` | 更改工作目录。 |

## C.3 HP-UX 与 Linux 系统调用对比表

| HP-UX 系统调用 | Linux 等效调用 | 描述 |
