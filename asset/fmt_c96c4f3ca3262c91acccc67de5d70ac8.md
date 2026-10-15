
## 退出状态

对于 `-d`、`-l` 和 `-s` 选项，会返回退出值。

- `0` 操作成功。
- `1` 错误条件。

对于 `-e` 选项，返回以下退出值。

被执行命令的退出状态。

- `0` 操作成功。
- `1` 无法以指定的优先级执行该命令。

## 属性

请参考 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | CSI SUNWc 已启用 |

## 阅

`nice(1)`, `ps(1)`, `exec(2)`, `fork(2)`, `priocntl(2)`, `rt_dptbl(4)`, `attributes(5)` 
《系统管理指南》，第一卷

## 1074 proc, plags, pcred, pmap, pldd, psig, pstack, pfiles, pwdx, pstop, prun, pwait, pfree, ptime

## 诊断

**未找到进程(进程)**
指定的进程均不存在。

**来自不同类的指定进程**
使用了 `-s` 选项设置参数，但不存在 `-c` 类选项，且指定了来自多个类的进程。

**无效选项或参数**
使用了无法识别或无效的选项或选项参数。

## proc, plags, pcred, pmap, pldd, psig, pstack, pfiles, pwdx, pstop, prun, pwait, ptree, ptime — Proc 工具

### 概要

```
/usr/proc/bin/plags [-r] pid...
/usr/proc/bin/pcred pid...
/usr/proc/bin/imap [-xlF] pid...
/usr/proc/bin/pldd [-F] pid...
/usr/proc/bin/psig [-F] pid...
/usr/proc/bin/pstack [-F] pid...
/usr/proc/bin/pfiles [-F] pid...
/usr/proc/bin/pwdx [-F] pid...
/usr/proc/bin/pstop pid...
/usr/proc/bin/prun pid...
/usr/proc/bin/pwait [-v] pid...
/usr/proc/bin/ptree [-a][ [pid|user]]...
/usr/proc/bin/ptime command [arg...]
```

## 描述

`proc` 工具是使用 `/proc` `proc(4)` 功能的命令。大多数工具接受一个进程 ID (`pid`) 列表；某些工具也接受 `proc/nnn` 作为进程 ID，因此你可以使用 shell 扩展 `/proc/*` 来指定系统中的所有进程。

- `plags` 打印每个进程中每个轻量级进程 (`lwp`) 的 `proc` 跟踪标志、挂起和持有的信号以及其他 `/proc` 状态信息。
- `pcred` 打印每个进程的凭据（有效、实际和保存的 UID 和 GID）。
- `pmap` 打印每个进程的地址空间映射。
- `pldd` 列出链接到每个进程的动态库，包括通过 `dlopen(3X)` 显式附加的共享对象。另请参考 `ldd(1)`。
- `psig` 列出每个进程的信号动作。另请参考 `signal(5)`。
- `pstack` 打印每个进程中 `lwp` 的十六进制-符号堆栈跟踪。
- `pfiles` 报告每个进程中所有打开文件的 `fstat(2)` 和 `fcntl(2)` 信息。
- `pdwx` 打印进程的当前工作目录。
- `pstop` 停止每个进程（`PR_REQUESTED` 停止）。
- `prun` 设置每个进程运行（`pstop` 的反操作）。
- `pwait` 等待所有指定的进程终止。
- `ptree` 打印包含指定 `pid` 或用户的进程树，子进程相对于其相应的父进程缩进。接受全数字参数作为进程 ID；否则，除非是用户登录名。默认是所有进程。
- `ptime` 对命令进行计时（例如 `time(1)` 命令），使用微状态计数以实现可重现的精确性。

`pfiles`, `pldd`, `pmap`, `pstack` 和 `pdwx` 命令在检查它们并报告结果时会停止目标进程。当进程被停止时，它无法执行任何操作。例如，如果你正在检查在 X server 下运行的这些 proc 工具之一。

## 选项

```
/usr/proc/bin/plags [-r] pid...
/usr/proc/bin/pcred pid...
```
