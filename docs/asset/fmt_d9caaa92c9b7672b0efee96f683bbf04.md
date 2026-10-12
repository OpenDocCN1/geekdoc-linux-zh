
NSD 输出的下一部分是系统上运行的进程（`ps` 输出）。此列表不仅包含 `notes` 用户拥有的进程，还包含了所有进程。

## 示例 4-4 当前进程

| F S UID PID PPID C PRI ANDR SZ ZWCAN STIME TTY TIME CMD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 004 | root | 1 | 0 | 0 | | | 80 | | | 012:05 | tty2 | 00:00:07 | init |
| 002 | root | 2 | 10 | 0 | | | 80 | | | 00:00 | tty2 | 00:00:00 | event |
| 002 | root | 3 | 0 | 0 | | | 80 | | | 00:05 | tty2 | 00:00:00 | nsird |
| 002 | root | 4 | 0 | 0 | | | 80 | | | 00:05 | tty2 | 00:00:00 | kwap |
| 002 | root | 5 | 0 | 0 | | | 62 | | | 00:05 | tty2 | 00:00:00 | flush |
| 002 | root | 6 | 0 | 0 | | | 79 | | | 00:05 | tty2 | 00:00:08 | dat |
| 002 | root | 7 | 0 | 0 | | | 62 | | | 00:05 | tty2 | 00:00:00 | ined |
| 002 | ndmadran | 2061 | 1994 | 0 | | | 80 | | | 11:27 | tty3 | 00:00:00 | http |
| 002 | ndmadran | 2062 | 1994 | 0 | | | 80 | | | 11:27 | tty3 | 00:00:00 | http |
| 002 | ndmadran | 2063 | 1994 | 0 | | | 80 | | | 11:27 | tty3 | 00:00:00 | http |
| 002 | ndmadran | 2064 | 1994 | 0 | | | 80 | | | 11:27 | tty3 | 00:00:00 | http |
| 002 | ndmadran | 2065 | 1994 | 0 | | | 80 | | | 11:27 | tty3 | 00:00:00 | http |
| 002 | ndmadran | 2066 | 1994 | 0 | | | 80 | | | 11:27 | tty3 | 00:00:00 | http |
| 002 | ndmadran | 2067 | 1994 | 0 | | | 80 | | | 11:27 | tty3 | 00:00:00 | http |
| 002 | ndmadran | 2081 | 1971 | 0 | | | 80 | | | 11:27 | tty3 | 00:00:00 | admin |
| 002 | ndmadran | 2082 | 2070 | 0 | | | 80 | | | 11:27 | tty4 | 00:00:00 | java_vm |
| 002 | ndmadran | 2083 | 2070 | 0 | | | 80 | | | 11:27 | tty4 | 00:00:00 | java_vm |
| 002 | ndmadran | 2084 | 2070 | 0 | | | 80 | | | 11:27 | tty4 | 00:00:00 | java_vm |
| 002 | ndmadran | 2085 | 2070 | 0 | | | 80 | | | 11:27 | tty4 | 00:00:00 | java_vm |
| 002 | ndmadran | 2086 | 2070 | 0 | | | 80 | | | 11:27 | tty5 | 00:00:00 | java_vm |
| 002 | ndmadran | 2100 | 1964 | 0 | | | 80 | | | 11:28 | tty3 | 00:00:00 | /lot/notes/latest/linux/replica |
| 002 | ndmadran | 2109 | 1964 | 0 | | | 80 | | | 11:28 | tty5 | 00:00:00 | /lot/notes/latest/linux/update |
| 002 | ndmadran | 2114 | 1961 | 0 | | | 80 | | | 11:29 | tty5 | 00:00:00 | /opt/notes/mozilla-bin |
| 002 | S | 2141 | 2005 | 0 | | | 80 | | | 11:41 | tty4 | 00:00:00 | /opt/notes/mozilla-bin |

服务器进程的第一个实例将是它的子进程，服务器进程会调用其他进程，例如事件或更新。这些进程被称为服务器的子进程。

当一个进程退出时，该进程的子进程将变成“孤儿进程”，这意味着父进程已退出，操作系统恢复到`init`，`init`是 UNIX 操作系统启动的第一个进程。`Init`负责加载所有其他进程，且其进程 ID（`PID`）始终为 `1`。

当发生崩溃且没有捕捉足够的崩溃信息时（例如核心文件被截断时），这些信息有时可以帮助我们判断是哪个进程崩溃了。

示例 4-5 是正常运行服务器的进程树。

## 示例 4-5 NSD 进程树

### 进程树

| 状态: | | |
| --- | --- | --- |
| `R` | -- 进程正在运行 | |
| `D` | -- 进程已死亡 | |
| `T/status` | -- 进程以退出状态终止 | |
| `S/signal` | -- 进程被信号杀死 | |
| `Q` | -- 未知程序 | |

| 用户名 状态 | pid | |
| --- | --- | --- |
| `root` `R` | `1200` `1097` `su - nadmb2` |
| `nadmb2` `R` | `1201` `1200` `-bash` |
| `nadmb2` `R` | `2117` `2046` `/opt/lotus/notes/latest/linux/server` |
| `nadmb2` `R` | `2286` `2127` `/opt/lotus/notes/latest/linux/http` |
| `nadmb2` `R` | `2240` `2127` `/opt/lotus/notes/latest/linux/http` |
| `nadmb2` `R` | `2150` `2127` `/opt/lotus/notes/latest/linux/sched` |
| `nadmb2` `R` | `2149` `2127` `/opt/lotus/notes/latest/linux/calconn` |
| `nadmb2` `R` | `2142` `2127` `/opt/lotus/notes/latest/linux/admin` |
| `nadmb2` `R` | `2141` `2127` `/opt/lotus/notes/latest/linux/amgr -er` |
| `nadmb2` `R` | `2173` `2141` `/opt/lotus/notes/latest/linux/amgr` |
| `nadmb2` `R` | `2140` `2127` `/opt/lotus/notes/latest/linux/router` |
| `nadmb2` `R` | `2135` `2127` `/opt/lotus/notes/latest/linux/replica` |
| `nadmb2` `R` | `2134` `2127` `/opt/lotus/notes/latest/linux/update` |
| `nadmb2` `R` | `2121` `2117` `/opt/lotus/notes/latest/linux/event` |

第二列中的`R`显示进程正处于活跃、运行状态。

第 238 页的示例 4-6 是另一个进程树，这次是一个服务器进程在无痕迹的情况下退出的服务器。

注意，除了一个例外外，这些进程没有显示为彼此的父子关系。`amgr`显示为另一个`amgr`进程的父进程。这是因为服务器加载了`amgr`和初始`amgr`进程，然后加载了后续的`amgr`任务。其他所有进程都是作为服务器进程的子进程加载的。

## 示例 4-6 NSD 子进程

| nadmb2 | R | 2286 | 2127 /opt/lotus/notes/latest/linux/http |
| nadmb2 | R | 2240 | 2127 /opt/lotus/notes/latest/linux/http |
| nadmb2 | R | 2150 | 2127 /opt/lotus/notes/latest/linux/sched |
| nadmb2 | R | 2149 | 2127 /opt/lotus/notes/latest/linux/calconn |
| nadmb2 | R | 2142 | 2127 /opt/lotus/notes/latest/linux/admin |

下一部分包含从调试器获取的堆栈跟踪。除了支持和开发专家以外的人，这些内容可能对其他人没有意义。

你可以检查的唯一一点是一个线程中包含“fatal”（致命）或“panic”（崩溃）一词。

如果问题是服务器崩溃，且没有列出包含任一关键词的线程，那么可能是数据收集过程中出现问题，导致崩溃信息未及时收集。

> 注意：该规则有例外，因此请始终将所有可用数据转发给支持人员，即使这些数据看起来价值有限。

例如，下面的堆栈（示例 4-7）显示了 HTTP 致命错误。

## 示例 4-7 HTTP 致命错误

