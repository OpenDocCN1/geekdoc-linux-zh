
## 1390

# telnet

- `-l user` 当连接到理解 `ENVIRON` 选项的远程系统时，将用户作为 `USER` 变量的值发送到远程系统。
- `-L` 在输出时指定一个 8 位数据路径。这将在输出时协商 `BINARY` 选项。
- `-n tracefile` 打开跟踪文件以记录跟踪信息。请参阅 `set tracefile` 命令。指定一个类似于 `login` 的用户接口。在此模式下，除非被 `-e` 选项修改，否则转义字符为波浪线（`~`）字符。`login` 转义字符仅在位于回车键（Return）之前时才被识别。在此模式下，你必须在 `telnet` 命令之前加上 `telnet` 转义字符（通常为 `^^`）。你也可以像 `login(1)` 那样通过 `.r` 或 `^z` 紧跟在 `login` 转义字符后面关闭或挂起连接。此选项是一个尚未提交的接口，未来可能会发生变化。

### 用法

`telnet` 命令 本节描述的命令在 `telnet` 中可用。此模式需要输入足够的命令来唯一标识它（对于 `mode`、`set`、`toggle`、`unset`、`environ` 和 `display` 命令也是如此）。

+ `close` 关闭任何打开的 `TELNET` 会话并退出 `telnet`。（文件结束 `end-of-file` 模式也会关闭会话并退出。）
+ `display [argument...]` 显示 `set` 和 `toggle` 的所有值（参见 `toggle` 参数）。
+ `environ arguments...` 使用 `environ` 命令处理通过 `ENVIRON` 选项发送的变量。从环境中获取初始变量。默认情况下导出 `DISPLAY` 和 `PRINTER` 变量。`environ` 命令的有效参数如下：
  + `define variable` 定义具有 `value` 的变量。自动由此命令定义的变量。你可以单引号或双引号包含 `value` 以包含制表符和空格。
  + `export variable` 标记要导出到远程侧的变量。列出环境变量。只有显式请求时发送其他变量。
  + `undefined variable` 从环境变量列表中移除变量。导出变量。
  + `unexport variable` 除非被远程侧显式请求。
  + `?` 打印 `environ` 命令的帮助信息。
+ `logout` 将 `telnet logout` 选项发送到远程侧。此命令类似于 `close`。如果远程侧不支持 `logout` 选项，则不会发生任何事情。如果远程侧支持 `logout` 选项，此命令应关闭 `TELNET` 连接。如果远程侧支持挂起用户会话以便稍后重新附加，`logout` 参数指示远程侧立即终止会话。
+ `mode type` 询问远程主机进入请求模式的权限。如果远程主机能够进入该模式，则 `type` 为以下之一：
  + `character` 禁用 `LINEMODE` 选项，或者如果远程侧不支持 `LINEMODE` 选项，进入“逐字符”模式。
  + `edit (-edit)` 尝试启用（禁用）`LINEMODE` 选项的 `EDIT` 模式。必须启用 `LINEMODE`。
  + `isig (-isig)` 尝试启用（禁用）`LINEMODE` 选项的 `TRAPSIG` 模式。必须启用 `LINEMODE`。
  + `line` 启用 `LINEMODE` 选项，或者如果远程侧不支持 `LINEMODE` 选项，进入“逐行”模式。
  + `litecho (-litecho)` 尝试启用（禁用）`LINEMODE` 选项的 `LIT_ECHO` 模式。必须启用 `LINEMODE`。
  + `softtabs (-softtabs)` 尝试启用（禁用）`LINEMODE` 选项的 `SOFT_TAB` 模式。必须启用 `LINEMODE`。
  + `?` 打印 `mode` 命令的帮助信息。

## 1392

# telnet

新！

`open [-l user [!] @hop1[@hop2...]@host [port]` 打开到指定主机连接。如果没有指定端口号，`telnet` 将尝试连接默认端口的 `TELNET` 服务器。你可以指定 `host` 为主机（参见 `hosts(4)`）、点表示法的 Internet 地址（参见 `inet(TP)` 或 `inet6P)`）。如果你指定的 `host` 为 `@hop1@hop2@host`，连接将通过 `hop1` 和 `hop2`，使用松散路由到达 `host`。指定的 `hosts` 之间需要用 `@` 符号作为分隔符。如果你对 `IPv4` 使用 `len !`，连接将遵循严格路由。

`-l` 选项将用户作为 `ENVIRONMENT USER` 的值传递给远程系统。`hop` 参数在 `Solaris 8` 版本中是新的。

`quit` 等于 `close`。

`send arguments` 向远程主机发送一个或多个特殊字符序列。你可以指定以下一个或多个参数：
+ `abort` 发送 `ABORT`（中止进程）序列。
+ `ao` 发送 `AO`（中止输出）序列，将远程系统的所有输出刷新到你的终端。
+ `ayt` 发送 `AYT`（你在吗）序列。远程系统可能响应也可能不响应。
+ `brk` or `break` 发送 `BRK`（中断）序列，该序列对远程侧可能有意义。
+ `do option dont option vont option` 发送指定的协议选项协商。`option` 可以是协议的文本名称或对应选项的选项数字。如果指定的选项协商在当前状态下无效，则会被静默忽略。如果你指定 `help` 选项，将列出选项名称。此命令对于异常调试有用。
+ `ec` 发送 `EC`（删除字符）序列以删除最后一个字符。
+ `el` 发送 `EL`（删除行）序列以删除当前行。
+ `eof` 发送 `EOF`（文件结束）序列。
+ `eor` 发送 `EOF`（记录结束）序列。
+ `escape` 设置 `telnet` 转义字符（初始为 `^`）。
+ `ga` 发送 `GA`（继续）序列，该序列对远程侧可能没有意义。

# telnet 1393

`getstatus` 如果远程侧支持 `STATUS` 命令，`getstatus` 将发送子协商以请求服务器发送其选项状态。
+ `ip` 发送 `IP`（中断进程）序列以中止当前运行的进程。
+ `nop` 发送 `NOP`（无操作）序列。
+ `susp` 发送 `SUSP`（挂起进程）序列。
+ `synch` 发送 `SYNCH` 序列以丢弃远程系统上之前输入但未读取的输入。此序列作为 `TCP` 紧急数据发送，如果远程系统是 `4.2 BSD` 系统，则可能不起。如果不生效，小写的 `r` 可能会在终端回显。
+ `?` 打印 `send` 命令的帮助信息。
+ `set argument [value]` `unset argument` 将 `telnet` 变量之一设置为特定值。特殊值会关闭与该变量关联的功能。你可以用 `display` 命令查询变量的值。如果你省略 `value`，则将值视为 `true` 或开启。如果你使用 `unset` 形式，则将值视为 `false` 或关闭。你可以你可以指定以下变量：
  + `ayt` 在 `localarchs` 模式或 `LINEMODE` 启用时向远程主机发送 `AYT` 序列。`ayt` 的初始值为终端状态字符。
  + `echo` 设置值（初始为 `^`），“逐行”模式用于在本地回显字符进行正常处理和抑制显输入的字符（如密码）之间切换。注意，在某些远程系统中，你必须在“逐行”模式下手动关闭 `echo`。
  + `eof` 当你在行首输入 `eof` 字符时，在“逐行”模式下操作时会将 `eof` 字符发送到远程侧。`eof` 的初始值为终端 `eof` 字符。
  + `erase` 在 `localarchs` 模式下并以“逐字符”模式操作时，向远程系统发送 `ES` 序列。`erase` 的初始值为终端 `erase` 字符。

## 1394

# telnet

- `flushoutput` | 当处于 `localchars` 模式下且你输入 `flushout` 字符时，向远程主机发送一个 `AO` 序列。`flush` 字符的初始值取终端的刷新字符。
- `forwl` | 在运行 `LINEMODE`（或“旧的逐行”模式）的远程系统上，当你输入 `forwl` 或 `for2` 字符时，将部分行转发到该远程系统。转发字符的初始值来自终端的 `eol` 和 `eol2` 字符。
- `interrupt` | 当处于 `localchars` 模式下（参见 `toggle localchars`）并输入中断字符时，设置发送到远程主机的中断序列。中断字符的初始值取终端的 `intr` 字符。
- `kill` | 当 `telnet` 处于 `localchars` 模式并以“逐字符”模式运行时，且你输入 `kill` 序列时，向远程系统发送一个 `EL` 序列。`kill` 字符的初始值取终端的 `kill` 字符。
- `lnext` | 在运行 `LINEMODE` 或“旧的逐行”模式时，假设 `lnext` 字符为终端字符。`lnext` 字符的初始值取终端的 `lnext` 字符。
- `quit` | 当处于 `localchars` 模式下并输入 `quit` 字符时，向远程主机发送一个 `BRK` 序列。`quit` 字符的初始值取终端的 `quit` 字符。
- `reprint` | 在运行 `LINEMODE` 或“旧的逐行”模式时，假设 `reprint` 字符为终端的打印字符。`reprint` 的初始值取终端的 `reprint` 字符。
- `rlogin` | 设置 `rlogin` 转义字符。忽略普通的 `telnet` 转义字符，除非该字符在行开头前面有此字符。当 `rlogin` 字符后跟 `a` 位于行开头时，关闭连接。当后跟 `Z` 时，挂起 `telnet` 命令。初始状态为禁用 `rlogin` 转义字符。
- `start` | 如果启用了 `TOGGLE-FLOW-CONTROL` 选项，则 `start` 字符取终端的 `start` 字符。`kill` 字符的初始值取终端的 `start` 字符。

# telnet 1395

`stop`
如果启用了 `TOGGLE-FLOW-CONTROL` 选项，则 `stop` 字符取终端的 `stop` 字符。`kill` 字符的初始值取终端的 `stop` 字符。

`susp`
当处于 `localchars` 模式或启用了 `LINEMODE` 且你输入 `suspend` 字符时，向远程主机发送一个 `SUSP` 序列。`suspend` 字符的初始值取终端的 `suspend` 字符。

`tracefile`
当 `netdata` 或 `debug` 选项真，将输出写入此文件。如果设置为 `-`，则将追踪信息写入标准输出（默认）。

`worderase`
在运行 `LINEMODE` 或“旧的逐行”模式时，将此字符视为终端的 `worderase` 字符。`worderase` 字符的初始值取终端的 `worderase` 字符。

`?`
显示合法的设置和取消命令。

`slc state` 在启用 `LINEMODE` 选项时，设置或更改特殊字符的状态。特殊字符是映射到 `TELNET` 命令序列（如 `ip` 和 `quit`）或行编辑字符（如 `erase` 和 `kill`）的字符。默认情况下，导出本地特殊字符。

`check`
验证当前特殊字符的设置。请求远程端发送所有当前的特殊字符设置。如果与本地存在任何差异，将本地设置切换为远程值。

`export`
切换到特殊字符的本地默认值。本地默认字符是启动 `telnet` 时本地终端的字符。

`import`
切换到特殊字符的远程默认值。远程默认字符是建立 `TELNET` 连接时远程系统的字符。

`?`
打印 `slc` 命令的帮助信息。

`toggle arguments...`
在控制 `telnet` 如何响应事件的各种标志的 `true` 和 `false` 之间切换。你可以指定多个参数。你可以查询这些标志。

## 1396

# telnet

`autoflush`
当 `autoflush` 和 `localchars` 均为真时，输入 `intr` 或 `quit` 字符时（参见 `set`），将其转换为 `TELNET` 序列，直到远程系统确认其已处理。此切换标志的初始值为 `true`。

`autosynch`
当 `autosynch` 和 `localchars` 均为真时，向远程主机发送 `SYNCH` 序列，直到 `netdata` 选项开启。此切换标志的初始值为 `false`。

`binary`
在输入和输出上启用或禁用 `binary` 选项。

`crlf`
确定如何发送 `Return`。如果值为 `true`，发送 `CRLF`；如果值为 `false`，则发送 `CR`。初始值为 `false`。

`cmod`
切换 `Return` 模式。启用后，从远程主机接收的所有 `Return` 字符将映射为 `Return` 后加换行符。其初始值为 `false`。

`debug`
切换接字级调试（仅限超级用户）。初始值为 `false`。

`inbinary`
在输入上启用或禁用 `binary` 选项。

`localchars`
如果为 `true`，则识别 `flush`、`interrupt`、`quit`、`erase` 和 `kill` 字符（参见 `set`），将其转换为 `ac`、`ip`、`br`、`ek` 和 `el` 序列（在“逐行”模式下为 `true`，在“逐字符”模式下为 `false`）。当启用 `LINEMODE` 时，忽略 `localchars` 的值并假设其始终为 `true`。

`LINEMODE` 启用时，`quit` 作为 `abort` 发送，`eof` 和 `suspend` 作为 `e` 和 `susp` 发送（参见 `send`）。

`netdata`
切换网络数据的显示（十六进制）。

## 1397

# telnet

`outbinary`
在输出上启用或禁用 `binary` 选项。

`prettump`
当 `netdata` 切换开启且 `prettump` 开启时，以更易读的格式格式化 `netdata` 输出。在每个字符之间加上空格。任何 `TELNET` 序列的开头都有星号 `*` 以便定位。

`skiprc`
为 `true` 时，打开连接时跳过读取家目录下的 `.netrc` 文件。初始值为 `false`。

`termdata`
切换终端数据的显示（十六进制）。初始值为 `false`。

`?`
显示合法的切换命令。

`status`
显示 `telnet` 的当前状态，包括连接的端和当前模式。

`z`
挂起 `telnet`。此命令仅在使用支持作业控制的 `shell`（如 `sh(1)`）时有效。

`? [command]` 获取帮助。不带参数时，打印帮助摘要。如果指定命令，则仅打印该命令的帮助信息。

## 1398

### 诊断

未登录：系统将在 `N` 分钟后关闭

系统正在执行关闭程序，登录功能已禁用。

# test — 评估条件

### 概要

```
